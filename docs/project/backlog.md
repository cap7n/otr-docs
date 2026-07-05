# Backlog

Things we've said **yes** to that aren't built yet. Not to be confused with [Open Questions](open-questions.md) (undecided) or the [Roadmap](roadmap.md) (the big-picture order). This is the working list: pick an item, build it, check it off.

Conventions: `🔨` = in progress · `⛔` = blocked by a decision or another item · unmarked = ready to pick up.

*Statuses verified against code, 2026-07-04. If a doc and the code disagree, the code wins.*

## Quick wins (code exists, one switch away)

- [ ] **Re-enable wall-drive:** controller is complete and wired, but `setup()` is commented out (car.gd:334). Re-enable, test Jolt gravity redirect on a ramp, then build zones in levels
- [ ] **Re-enable drift:** same story, complete controller, `setup()` commented out (car.gd:329)
- [ ] **Wire visual wear to damage:** the wear shader system (scratches/rust/dirt) is built and synced, but nothing increments it during gameplay; hook it to car damage events

## Gameplay systems

- [ ] **First hazards: steam vent + fire patch:** none of the six hazards exist in code ([hazards plan](../systems/hazards.md))
- [ ] **Remaining hazards:** falling rocks, flooded zone, collapsing floor, swinging obstacles
- [ ] **First shortcut: destructible wall + side path:** junk_barricade/locked_gate exist as main-path obstacles; the optional side-path variant doesn't ([plan](../systems/shortcuts.md))
- [ ] **Interactable loot chest:** opens on E, loot table, server-authoritative; no chest entity exists yet
- [ ] **Gate countdown UI:** logic done, TODOs in level_gate.gd and return_gate.gd are display-only
- [ ] **Wire an objective to return_gate.unlock():** the gate already supports "locked until objective complete", nothing calls it yet; this is where the run's goal plugs in
- [ ] **Save file:** user:// ConfigFile autoload for currency + unlocks; confirmed absent, prerequisite for junker and modifier unlocks
- [ ] **Battery leash:** on-foot power timer (~30-60s), gray-screen desaturation as it fails, stumble back to the car to recharge ([World & Structure](../level-design/world-structure.md))
- [ ] **Drone signal tether:** drone limited by signal range from the car, not battery; static/interference as it nears the edge
- [ ] **Diegetic exit signals:** lights on zone walls (or similar in-world tells) showing which exits are open this cycle
- [ ] ⛔ **Junker package:** unlock flags per ability controller (+ peer sync), CAR_MOD items, shop wiring; blocked on the saving/stakes decision ([open question 1](open-questions.md))
- [ ] ⛔ **What death costs (loot loss, repair costs):** blocked on the saving/stakes decision
- [ ] **Flank enemy:** paces alongside the car in bursts, the honest "keeps up" enemy ([threat directions](../game/enemies.md))
- [ ] **Run modifiers:** confirmed absent; after core loop is solid ([plan](../systems/modifiers.md))
- [ ] **Callout/ping system:** confirmed absent; gunner marks shortcuts and threats for the driver
- [ ] **Boss rework:** benched; doesn't feel good yet, needs love before any route depends on it

## Level design

- [ ] **First authored zone (new level):** the garage's neighboring zone, built session-style: opening encounter, complication, fork, climax (set-piece, not boss), exit through a wall gate. round1_a is a tech demo, not the target ([World & Structure](../level-design/world-structure.md), [The Tunnels](../level-design/tunnels.md))
- [ ] **Cavern lighting test:** one gray-box cavern: baked LightmapGI + volumetric fog + light shafts + distant emissives; proves the megalophobia works ([Setting & Scale](../level-design/setting-and-scale.md))
- [ ] **Tunnel kit cross-section profile:** the one profile all modular pieces share; decide before modeling any kit piece
- [ ] **Blockout kit pieces:** straight, curves, squeeze, cavern shell, Y-junction, slope, portal, wall-drive ramp, alcove
- [ ] **Fix square shadows:** smooth the turret meshes; if that's not enough, raise positional shadow atlas size / light softness

## Code health (from the July 2026 audit)

- [ ] 🔨 **RPC sender validation on 4 input handlers:** running as background task; seat-shared controls (handbrake!) must keep working
- [ ] 🔨 **Globals.DEBUG flag + gate 50+ prints:** running as background task
- [ ] **Cache enemy target scans:** 5 enemy scripts call get_nodes_in_group every physics frame; horde_manager already shows the right pattern
- [ ] **Centralize the RPC broadcast pattern:** the `call locally, then rpc_id to every world-ready peer` loop is copy-pasted ~10× across car.gd, door_controller.gd, seat_controller.gd, and most ability controllers. One shared `broadcast(method, args)` helper (autoload or a controller base class) would collapse them all and shrink every controller at once. **Handle with care:** RPC has bitten before — do it in its own session, one call site at a time, host+client test after each. Deliberately skipped during the 2026-07-05 car.gd split to keep that refactor RPC-neutral
- [ ] 🔨 **Split car.gd and player.gd (1072):** car.gd half done 2026-07-05 (1233 → 912; doors/cargo, seats/interact, audio, drone dock extracted to controller nodes — all 17 @rpc functions kept on the Car node so RPC paths are unchanged), pending multiplayer test. player.gd: the 2026-07-05 audit says don't split by size — extract the one misfit system, a **SeatCameraDirector** (seat entry/exit beziers, sway, wall-drive blend, ~300 lines → player lands near 700). When next doing major camera work, not before
- [ ] **Rate-limit inventory drag RPC:** `_rpc_drag_move` fires every render frame while dragging (inventory_controller.gd:242) — 144+ RPCs/s on fast monitors. player.gd already shows the fix three lines from its own position sync: gate on physics frames to ~20 Hz
- [ ] **Polled input bypasses in_ui_mode:** drone_operator polls the mouse in _physics_process so turret fire ignores the UI gate that _unhandled_input respects; driver_controller same shape. Low impact today (UI + seat rarely overlap), fix when it first bites
- [ ] **Characters chores from the 2026-07-05 audit:** dead tail in player.gd `_process_seated` (`if not _is_local: return` with nothing after); `_cubic_bezier`/`_smoothstep` duplicated in player.gd + inventory_controller.gd; hardcoded KEY_I / KEY_O / ESC → input actions
- [ ] **The last arrival-time stream (host-side player jitter):** the client's on-foot position RPC bypasses NTM and the host stamps its snapshots with `local_time` = arrival time (player.gd `_rpc_send_position`) — the exact anti-pattern the tick-time system was built to kill. Predicts: host sees the client's droid slightly jittery at 20 Hz, client sees the host smoothly. Fix: client stamps a sequence number, host maps via a small per-stream baseline (like `get_tick_time` at 1/20 s spacing). **Do this in a live two-machine session with A/B before/after** — it touches the interpolation path
- [ ] 🔨 **NTM keepalive for dropped rest-state packets:** applied 2026-07-05 (clean entities resend once per second so a dropped unreliable final packet self-heals; additive only — no timestamp/interp changes), pending multiplayer test. Once confirmed, car.gd's client-side speed derivation workaround could be simplified
- [ ] **WorldManager run-complete "reset" doesn't reset:** the clears in `request_return_to_hub` are immediately refilled by `_collect_carry_over()` in `_begin_transition` — the victory hub inherits car damage despite the visible intent. Decide: fresh start (add a skip-collect flag) or carry-over (delete the dead clears)
- [ ] **Network spine chores (2026-07-05 audit):** `interp_delay` is @export but `_ready()` overwrites it — Inspector value silently lies; NetId registry accumulates FREED entries across level transitions; crouch flag missing from player sync dict so remote players never play kneel_idle
- [ ] **Fix `:=` typing violations:** mostly road_generator.gd (33) and terrain_conform.gd (15)

## Chores

- [ ] ⛔ **Project stretch mode:** add window/stretch canvas_items + expand to project.godot; waiting until the background code sessions land, then glance over every UI scene once
- [ ] **Rename schop_screen.tscn → shop_screen_panel or similar:** editor rename so references update
- [ ] **Remove level_test_texutures from world.tscn:** editor; drags an 11 MB collision shape with it
- [ ] **External_Carp terrain pack decision:** 49 MB, unknown licence, no references found; verify Terrain3D doesn't need it, then delete
- [ ] **Delete Audio/Recall.mp3 if unused:** verify in editor first

## Parked (someday, after the game is fun)

- [ ] **Rebuild menu visuals:** menu was stripped to bare buttons (2026-07) after the 52 MB embedded 3D showcase broke layout and dragged netcode into the menu. Design a proper look when the game underneath deserves it
- [ ] **Intro sequence:** two droids wake low-battery in a garbage dump, gray screen, stumble to the garage, plug in, world blooms to color ([World & Structure](../level-design/world-structure.md)). Build after the battery leash exists (it reuses the same gray-screen system)

## Done

*(Move checked items here with a date, it feels good and it's useful history.)*

- [x] Already built (confirmed by code audit 2026-07-04): **nitro boost** (3 charges, exhaust VFX), **car jump** (Q, dust VFX), **flamethrower** (fuel system, 50 DPS), **rocket pot** (4-tube launcher), **rocket thrust** (charge-based, phased burn), **stasis cargo lock**, **level/return gates** (incl. objective unlock hook), **horde manager** (ghost promotion/demotion by distance), **wear shader** (visual side), **item behaviors** (armor plate, repair kit, bomb)
- [x] 2026-07: Git history rewrite: 1,078 MB of ghost blobs stripped (old hub/menu/world versions), 1.2 GB → 626 MB, current files bit-identical, full backup bundle in Backups. Verified on both machines after re-clone; commit history reads under dev names only
- [x] 2026-07: Audit branch tested in-game and merged into main (4 commits: junk removal, 170 orphans, menu strip)
- [x] 2026-07: Main menu stripped and rebuilt as clean scene (52 MB → 2 KB); layout bug fixed, car/drone netcode removed from menu
- [x] 2026-07: Design wiki built and live at cap7n.github.io/otr-docs
- [x] 2026-07: Full project audit; 170 dead files removed on `audit/2026-07-cleanup`
- [x] 2026-07: Start/end zone gates confirmed working (A→B→hub loop closed)
