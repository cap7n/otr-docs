# String References Audit

*Swept 2026-07-15, all 115 `.gd` files under `Scripts/` (addons excluded). Line numbers are from that day's `main`; they'll drift, the file names won't.*

A **string reference** is any place code names a node, method, group, animation, property, or resource by a string. GDScript compiles these fine and fails only at runtime — and when you rename a node in the editor, Godot rewrites the `.tscn` files but **never touches `.gd` scripts**. Every string below is a rename away from a silent breakage.

Not everything here is worth fixing. Categories are ordered by risk; the actionable items live in the [Backlog](backlog.md) under Code health.

## 1. Node paths as network identity — HIGH

The one category that causes real multiplayer bugs, not just refactor hazards. Entities are identified **across peers** by their node path string; any divergence in tree order or a dropped packet means the path resolves to nothing (silent no-op via `get_node_or_null`) or to the *wrong node* on the other machine.

| Where | What travels over the wire |
|---|---|
| `NetworkTickManager.gd:185,195` (registry), `:391` (resolve) | sync registry keyed by `str(entity.get_path())`; world state re-resolves via `get_node_or_null(NodePath(path))` |
| `rocket_pot_controller.gd:116` | rockets matched across peers by **deterministic auto-numbering** of same-named nodes — the invariant the comment itself admits; prime suspect in the phantom-rocket-smoke backlog item |
| `turret.gd:295 → 376` | `_rpc_apply_impulse` sends `hit_body.get_path()`, receiver resolves from `get_tree().root` |
| `inventory_controller.gd:196,206,242 → 254,269,286,300,316` | drag/move RPCs ship `str(item.get_path())` |
| `item_pickup_controller.gd:29,40,99,110 → 54,83,124,145,166,182,200` | pickup/drop/throw RPCs ship item paths, seven resolve sites |

**Fix direction:** the `NetId` autoload already exists and already stamps `set_meta("net_id", id)` — migrate these streams to NetId ints and keep paths out of packets. Same medicine as the phantom-rocket item; do them together.

## 2. Hardcoded node paths in scripts — MEDIUM

**130 `$Node` references and 52 `get_node("…")` string literals** across ~40 scripts. Every one breaks at runtime if the node is renamed or moved, with no editor assist.

Worst offenders:

- `turret.gd` — 14 refs in deep chains like `$Base/PitchPivot/Boddy/barrelL` (yes, **the `Boddy` typo is now load-bearing** — fixing the node name means fixing 8 paths)
- `car.gd` — 12 refs (`$DriverSeat`, `$CarHealth`, `$Turret`, …), plus satellites reaching into the car by name: `seat_controller.gd:23-24`, `drone_dock.gd:23-26`, `car_audio_controller.gd:68-80`, `armor_plate_behavior.gd:22`, `repair_kit_behavior.gd:23`, `base_level.gd:98,112`
- `lobby.gd` (10), `main_menu.gd` (5), `car_telemetry.gd`/`prototype_telemetry.gd` (`$Root/VBox/…`)
- `engine_sound_blender.gd:75,79` — builds names **dynamically** (`"OnLoop%d" % int(rpm)`); grep can't even find these, a rename fails only when that RPM band first plays
- 12 files fetch a registered autoload by path: `get_node_or_null(^"/root/DebugManager")` — `DebugManager.…` would be checked at parse time

**Mitigations that exist in-project already:** `visual_damage_controller.gd:189` does it right (`@export var target_mesh_paths: Array[NodePath]` — the editor tracks renames in exported NodePaths). Scene-unique names (`%Node`) are used **zero** times today; they survive re-parenting, though not renames.

## 3. Duck typing by method-name string — MEDIUM

**42 `has_method("…")` sites** plus a handful of `call`/`call_deferred` by string. A typo'd method name doesn't error — the check just returns false and the call silently never happens.

- `"take_damage"` — string-matched at **11 sites**: `turret.gd:296`, `enemy_turret.gd:252`, `enemy.gd:391,409,520`, `enemy_boss.gd:362`, `enemy_projectile.gd:46`, `rocket.gd:209`, `flamethrower_controller.gd:89`, `bomb_behavior.gd:67`, `locked_gate.gd:87`
- `"apply_explosion_force"` — `enemy.gd:540`, `bomb_behavior.gd:85`
- sync interface `"get_sync_state"` / `"apply_sync_state"` / `"get_sync_owner_peer_id"` — `NetworkTickManager.gd:50,233,394`, `debug_hud.gd:173`
- pool interface `"pool_reset"` / `"pre_warm"` / `"acquire"` / `"activate"` — `enemy_pool.gd:70`, `enemy_spawner.gd:18,91,98`
- assorted: `"enter/exit_inventory_mode"` (`cargo_box.gd:128`, `seat_controller.gd:172,177`), `"enter/exit_zone"` (`wall_drive_zone.gd:36,47`), `"set_paint_percent"` (`remote_drone_targeting.gd:47,97`), `"recoil_pulse"` (`turret.gd:307`), `"heal"`/`"add_max_hp"` (item behaviors), `"send_rocket_input"` (`player.gd:414`), `"_weak_point_hit"` (`locked_gate.gd:95`), `call("set_camera")` (`camera_controller.gd:68`)

**Fix direction:** a `Damageable` base class (or `class_name` + `is` checks) for the damage pair kills the two biggest families in one move; the compiler then catches renames. NTM already half-enforces its interface at register time — make it assert.

## 4. Group name strings — MEDIUM-LOW (cheapest fix)

**50 sites, 11 distinct group strings**, every one typed by hand: `enemy` (9), `targetable` (11), `interactable` (6), `players` (4), `car` (5), `enemy_spawn_points` (4), `spawn_zone_triggers` (2), `camera_system` (2), `pickup_items`, `prototype_car`, `skid_marks`.

One typo'd `add_to_group("enemey")` = an enemy the flamethrower can't see, and nothing logs. **Fix:** a `Groups` block of `StringName` constants in Globals (`Groups.ENEMY`), mechanical find-replace, done in an hour.

## 5. Property access by string — LOW-MEDIUM

~40 sites of `object.get("prop")` / `set("prop")` on nodes (Dictionary `.get()` excluded — that's fine). Renaming the property silently turns these into nulls.

- `debug_hud.gd` — the heavy user (~15 reads), including **private** vars: `get("_yaw")`, `get("_target_pitch")`, `get("_state_buffer")`, `get("_vec")`, `get("_current_seat")`. Debug-only blast radius, but it's the readout you trust while debugging something else
- `WorldManager.gd:167-183` — run carry-over reads `car_node.get("drone_lives")`, `get("seats")`, `player_node.get("_current_seat")`, `get("stasis_zone")` — this one is *gameplay state*, a rename means carry-over quietly stops carrying
- `wall_drive_zone.gd:33,44` — `car.get("wall_drive_controller")`
- `rocket.gd:92`, `blood_hit_effect.gd:139`, `enemy.gd:653`, `enemy_boss.gd:591`, `ranged_enemy.gd:339` — `set(...)` on VFX scenes to avoid a preload/typed dependency
- `terrain_flatness.gd:25,59`, `horde_manager.gd:281` — `terrain.get("data")` (unavoidable: Terrain3D is a GDExtension accessed loosely; same story as `get_class() == "Terrain3D"` in `camera_controller.gd:67`)

## 6. Animation, bone & scene-object names — LOW (one known bug)

- `character_animator.gd` — 9 animation-name strings (`pistol_idle`, `pistol_run`, `pistol_strafe_2`, `kneel_idle`, …). `kneel_idle` is the **known-missing** one from the 4.7 aftercare list; the fallback at `:110` warns, which is the right pattern — but only fires when the state is first hit in play
- `character_animator.gd:48` — `find_bone("mixamorig_Hips")`; `:41,46` + `player.gd:265` — `find_child("AnimationPlayer"/"Skeleton3D")` (rig re-export sensitive)
- `hub.gd:18,20` — `get_node("GateLabel")`; `horde_manager.gd:130` — `get_node_or_null("Ghosts")`; `rocket.gd:220` + `enemy_boss.gd:581` — `current_scene.get_node_or_null("VFXPool")` (every level must remember to have one, misspell it and effects just don't spawn)

**Fix direction:** const StringNames for the anim set + a one-loop startup validation (`for a in ANIMS: if not _anim_player.has_animation(a): push_warning(...)`) so a bad re-import reports every missing clip at spawn, not one at a time in play.

## 7. Runtime `load("res://…")` paths — LOW

6 sites where a moved/renamed file fails only when that code path runs (the editor updates `.tscn`/`.import` references on move, but not raw strings in scripts):

- `game_over_menu.gd:17` — `load("res://Scenes/World/hub_v2.tscn")` (a *level path* in a UI script; also duplicates WorldManager's job)
- `bomb_behavior.gd:28` — explosion VFX scene
- `blood_hit_effect.gd:77`, `interact_zone.gd:40`, `enemy_boss.gd:188` — shaders
- `debug_manager.gd:49` — debug window script (debug-only, fine)

**Fix:** `preload` where no cyclic dependency blocks it — fails at parse time instead, i.e. the moment the editor loads the script.

## 8. Shader parameter names — INFORMATIONAL

68 `set_shader_parameter("…")` calls across 11 files. Inherently stringly in Godot — renaming a uniform in a `.gdshader` silently no-ops every setter. Not worth a sweep; **rule of thumb going forward:** when the same uniform is set from more than one script, hoist the name into a shared `const StringName`.

## 9. Input actions & keycodes — already covered

18 `is_action_*("…")` sites — standard Godot practice, project-validated names, leaving alone. The hardcoded `KEY_I` / `KEY_O` / `KEY_ESCAPE` in `player.gd:369,374` and `inventory_controller.gd:149` are already a backlog chore (Characters chores, 2026-07-05 audit).

## The fix menu

| Stringly pattern | Replace with |
|---|---|
| path string over RPC | `NetId` int (autoload exists) |
| `$Deep/Child/Path`, `get_node("…")` | `@export NodePath` / scene-unique `%Node` / `@onready` one-hop |
| `has_method("take_damage")` | `Damageable` base class + `is` check |
| `add_to_group("enemy")` | `Groups.ENEMY` StringName consts |
| `obj.get("_private")` | a real getter, or accept it (debug code) |
| `load("res://…")` at runtime | `preload` |
| anim name literals | const StringNames + startup validation |
