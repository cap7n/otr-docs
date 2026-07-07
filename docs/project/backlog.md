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
- [ ] **Harpoon / tether tool (co-op combo enabler):** co-pilot latches an enemy, the driver's cornering slings it into a wall or other enemies — the archetypal two-seat combo ([Co-op Design Principles](../co-op-design.md)). Proposed 2026-07; no tether exists in code
- [ ] **Terrain-impact deflection (car feel):** hitting a banked slope should bump the car and push it to turn away; today the stability assists eat the natural Jolt deflection (yaw-damp kills the "unwanted" yaw, slide-align pulls the nose back, anti-roll flattens the body kick) so the car plows on-rails. Fix direction: reuse the existing `recoil_pulse()` relief pattern — when `vertical_jolt` (already computed for camera shake) or a lateral load spike crosses a threshold, open a short relief window on yaw-damp + slide-align + anti-roll so the physics deflection reads through, then fade assists back. No fake forces; only add an explicit contact-normal torque if relief alone is too subtle. Proposed 2026-07-05
- [ ] **Run modifiers:** confirmed absent; after core loop is solid ([plan](../systems/modifiers.md))
- [ ] **Callout/ping system:** confirmed absent; gunner marks shortcuts and threats for the driver
- [ ] **Boss rework:** benched; doesn't feel good yet, needs love before any route depends on it
- [ ] **First landmark enemy (method-to-kill):** a one-of-a-kind, zone-specific encounter beaten by a *method*, not a health bar — e.g. harpoon-trip a tall quadruped then hit the exposed head, or lure it into a hazard ([Landmark Enemies & Bosses](../game/landmark-enemies.md)). Rides with the first authored zone

## Level design

- [ ] **First authored zone (new level):** the garage's neighboring zone, built session-style: opening encounter, complication, fork, climax (set-piece, not boss), exit through a wall gate. round1_a is a tech demo, not the target ([World & Structure](../level-design/world-structure.md), [The Tunnels](../level-design/tunnels.md))
- [ ] **Cavern lighting test:** one gray-box cavern: baked LightmapGI + volumetric fog + light shafts + distant emissives; proves the megalophobia works ([Setting & Scale](../level-design/setting-and-scale.md))
- [ ] **Tunnel kit cross-section profile:** the one profile all modular pieces share; decide before modeling any kit piece
- [ ] **Blockout kit pieces:** straight, curves, squeeze, cavern shell, Y-junction, slope, portal, wall-drive ramp, alcove
- [ ] **Fix square shadows:** smooth the turret meshes; if that's not enough, raise positional shadow atlas size / light softness

### Scrapyard zone (in build — hub_v2 is the test bed; plan lives in the zone map, terrain/blockout/mounds/materials landed 2026-07-07, see Done)

- [ ] 🔨 **Junk blocks (nondescript compacted-metal bricks):** modeling now; deliberately not car-shaped — it's what a compactor actually spits out. Replaces the steel-cube placeholders in the block yard
- [ ] **Crushed car cube + paint variants:** ~2.2×1.7×1.1 m crumpled box, one material slot named `CarCube` (name = the import-remap socket); faded red/blue/yellow/white paint over rust variants
- [ ] **Row-builder tool:** give it a start/end line → MultiMesh wall of stacked cubes with random variant/rotation/jitter; builds the graveyard rows and the shelter palisade
- [ ] **Scatter tool:** "sprinkle N of prop X in this region / along this lane edge, seeded" → MultiMesh; prerequisite for every dressing pass
- [ ] **Lane-edge hero props, one at a time through the pipeline:** tire (single + stack) → barrel/drum → washing machine → dumpster/container → fridge. Free prototype models may stand in as scatter placeholders meanwhile; finals go through the pipeline (no photo textures)
- [ ] **Landmarks:** compactor building + crane (possibly still running — sound + slow motion), weighbridge + booth at the plaza, shelter builds (shack, watchtower; palisade reuses car cubes)
- [ ] **Gate module — build once, use 4× in every zone:** door slab, frame, and the open/closed light fixtures (the diegetic exit signal). In the scrapyard: N/E open, W barricaded by the shelter, S standing in raw ground with no road (never seen open)
- [ ] **Dedicated dirt ground tile:** zone ground currently borrows the concrete roughness map for grain; bake a real dirt tile (pebbles, tire ruts on lanes)
- [ ] **Zone-map channels G + B:** G = human footpaths (albedo wear only — feet don't compact terrain), B = burn-zone scorch tint. Mask generator writes RGB, ground shader reads them (hooks already documented in the shader)
- [ ] **Burn zone dressing:** smoke columns, ember glow at the pits; ties into the fire-patch hazard when it exists
- [ ] **Extraction scar at the dead-end road:** the old intake road runs into the N wall mid-route; one hero object at the cut (sliced sign, half a truck) makes the story land
- [ ] **Puddles in the low spots** (existing puddle shader)
- [ ] **Zone footprint rework:** 2×2 km of pure yard reads too big. Direction: fenced yard core (~600–800 m, dense) + the extracted surroundings (access road, wasteland, shelter outside the fence) — fits the sampling fiction and gives a sparse→dense intensity gradient. Reshaping in progress
- [ ] **Bake the pile scale factor into the mound prep tool** once in-game testing locks it (current read: canyon piles ~20–25 m, sprinkles 8–12 m; proximity to the lane matters as much as height)

## Code health (from the July 2026 audit)

- [ ] 🔨 **RPC sender validation on 4 input handlers:** running as background task; seat-shared controls (handbrake!) must keep working
- [ ] 🔨 **Globals.DEBUG flag + gate 50+ prints:** running as background task
- [ ] **Cache enemy target scans:** 5 enemy scripts call get_nodes_in_group every physics frame; horde_manager already shows the right pattern
- [ ] **Centralize the RPC broadcast pattern:** the `call locally, then rpc_id to every world-ready peer` loop is copy-pasted ~10× across car.gd, door_controller.gd, seat_controller.gd, and most ability controllers. One shared `broadcast(method, args)` helper (autoload or a controller base class) would collapse them all and shrink every controller at once. **Handle with care:** RPC has bitten before — do it in its own session, one call site at a time, host+client test after each. Deliberately skipped during the 2026-07-05 car.gd split to keep that refactor RPC-neutral
- [ ] **Split player.gd (car.gd half done + tested):** car.gd 1233 → 912 landed 2026-07-05, multiplayer-tested same day. player.gd: the audit says don't split by size — extract the one misfit system, a **SeatCameraDirector** (seat entry/exit beziers, sway, wall-drive blend, ~300 lines → player lands near 700). When next doing major camera work, not before
- [ ] **Rate-limit inventory drag RPC:** `_rpc_drag_move` fires every render frame while dragging (inventory_controller.gd:242) — 144+ RPCs/s on fast monitors. player.gd already shows the fix three lines from its own position sync: gate on physics frames to ~20 Hz
- [ ] **Polled input bypasses in_ui_mode:** drone_operator polls the mouse in _physics_process so turret fire ignores the UI gate that _unhandled_input respects; driver_controller same shape. Low impact today (UI + seat rarely overlap), fix when it first bites
- [ ] **Characters chores from the 2026-07-05 audit:** dead tail in player.gd `_process_seated` (`if not _is_local: return` with nothing after); `_cubic_bezier`/`_smoothstep` duplicated in player.gd + inventory_controller.gd; hardcoded KEY_I / KEY_O / ESC → input actions
- [ ] **The last arrival-time stream (host-side player jitter):** the client's on-foot position RPC bypasses NTM and the host stamps its snapshots with `local_time` = arrival time (player.gd `_rpc_send_position`) — the exact anti-pattern the tick-time system was built to kill. Predicts: host sees the client's droid slightly jittery at 20 Hz, client sees the host smoothly. Fix: client stamps a sequence number, host maps via a small per-stream baseline (like `get_tick_time` at 1/20 s spacing). **Do this in a live two-machine session with A/B before/after** — it touches the interpolation path
- [ ] **Simplify car.gd's client-side speed derivation:** now that the NTM keepalive is in and tested (see Done), the stale-sync workaround it was built for can likely be retired
- [ ] **WorldManager run-complete "reset" doesn't reset:** the clears in `request_return_to_hub` are immediately refilled by `_collect_carry_over()` in `_begin_transition` — the victory hub inherits car damage despite the visible intent. Decide: fresh start (add a skip-collect flag) or carry-over (delete the dead clears)
- [ ] **Network spine chores (2026-07-05 audit):** `interp_delay` is @export but `_ready()` overwrites it — Inspector value silently lies; NetId registry accumulates FREED entries across level transitions; crouch flag missing from player sync dict so remote players never play kneel_idle
- [ ] **Phantom rocket smoke on the client (no rockets in flight):** seen 2026-07-05 after a session with turret + rocket fire; smoke hangs at the launcher on the client only. Prime suspects exonerated by scene-file evidence (thrust/nitro/flames/muzzle all default-off or self-terminating). Leading hypothesis: ghost rocket — rockets are identified across peers by auto-numbered node path (rocket_pot_controller.gd:116 admits the invariant), but tracers/impact dust spawn into the same parent via UNRELIABLE `_rpc_fire_effects`; one dropped effects packet desyncs the auto-number counter, after which `_rpc_explode` + NTM sync target a path the client doesn't have → its rocket is never freed and lingers with VFX. Diagnostic next repro: client's Remote scene tree → look for a stray `Rocket`/`@Rocket@N` node the host doesn't have. Fix direction: identify rockets via NetId (autoload already exists) instead of path determinism, and/or stop spawning one-shot effects into the same auto-number namespace
- [ ] **Turret aim RPC is per-mouse-event unreliable:** minor smell left over from the (fixed) turret jitter — gunner input deltas fire one unreliable RPC per InputEventMouseMotion, which can burst at mouse polling rate; batch per physics tick when convenient
- [ ] **lobby.gd is binary to git:** 72 trailing null bytes (torn-write artifact) make git classify it as binary — no readable diffs for lobby.gd ever. Strip the padding (byte-truncate, zero logic change), commit, diffs come back. Drone audit 2026-07-05 verdict otherwise: distributed authority implemented properly (velocity-inheriting handoff, transfer-race guard, disconnect reverts to host); only chore is the vestigial gimbal_yaw sync field + dead Edge Yaw export group in drone2.gd
- [ ] **Fix `:=` typing violations:** mostly road_generator.gd (33) and terrain_conform.gd (15)

## Godot 4.7 aftercare (migration succeeded 2026-07-05 — log clean, extensions loaded, full session ran)

- [ ] **Re-save car.tscn:** 4.7 reimport of Car.blend triggers a scene "recovery process" on every load; also check the orphaned `Car mesh/Vent` override ("modified from inside an instance, but it has vanished")
- [ ] **NTM burst overflows MTU (1524 > 1392 bytes unreliable):** all entities go dirty on the same tick (level spawn; the keepalive repeats the burst each second) and the 80-byte-per-entity estimate undershoots. Stagger keepalive phase per entity (hash of path) + raise estimate to ~110
- [ ] **kneel_idle animation not found:** crouch falls back to pistol_idle. Check the Ybot AnimationPlayer list — the 4.7 reimport may have renamed it; else it never existed and crouch was never animated
- [ ] **`reset_physics_interpolation()` deprecated in 4.7:** works but warns; look up the blessed replacement in the 4.7 docs, then mechanical rename across player/drone/turret/rocket/car call sites

## Chores

- [ ] **Finish the hub_v2 shell material swap:** point floor and ceiling at their mega_concrete_v2 .tres (wall done 2026-07-06); clear the leftover v1-shader `next_pass` on the wall material if still present
- [ ] **Delete old pipe assets** once the pipe_outfall instance in hub_v2 is replaced by mega_pipe_v2: `pipe_outfall.tscn`, `BigPipeWithWater.blend` (+.import), `pipe_outer/pipe_inside.tres`, `textures/PipeOutfall/` (pre-texture backup lives in Desktop/OTR/Backups)
- [ ] **Retire mega_concrete.gdshader (v1)** when no surface references it — the comparison reference wall still uses it today
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

- [x] 2026-07-07: **Scrapyard zone build started (hub_v2 as test bed).** Zone plan map: workflow-worn roads (truck arterial, service loop, desire-path corner cuts, filleted junctions) in two generations — the yard's historical network dead-ends at the N wall where the extraction cut it, plus straight bulldozed connectors to the megastructure gates. Built: heightfield floor generator (2 m grid, one HeightMapShape3D collider, seeded noise, road flatten-mask so terrain and roads can never disagree), mask rasterizer from the plan, colored per-section blockout, six sculpted trash mounds through a prep tool (decimate + collision twin + canonical height) placed as the scrap mountains, scrap-mass tileable material (junk cells, rare paint chips, world-triplanar so instance scaling is safe) with a macro-mottle detail layer against tiling repetition, and a zone ground shader blending packed road dirt vs yard dirt from the same mask that shapes the terrain

- [x] 2026-07-06: **Blender→Godot asset pipeline built and proven** (`Desktop/OTR Assets`: procedural material scripts, lookdev blends with preview renders, tileable + per-object bakers). Two assets shipped same day: **MegaPipeV2** (weathered metal + rust, flowing-water shader untouched, materials remapped by name in .import) and **shell concrete v2** (baked tile + slim hybrid shader: per-panel tint/mirror-flip, macro patches, floor grime, close-up detail bump). Killed the 2 km shimmering-lines wall artifact (procedural math can't be mip-filtered) and the inverted wall lighting (RGTC-compressed normal maps drop the blue channel — shader now reconstructs it)

- [x] 2026-07-05: **"Phantom .blend rewrites" investigated → no phantom.** Every blend change was the partner's genuine Blender work (autosmooth etc.) arriving via pull; the "I pushed a file I didn't touch" impression was GitHub Desktop showing pulled commits + pull-merge commits alongside your own push. Lesson: check the AUTHOR column before assuming a commit is yours — `git log --format="%h %an %s"` settles it in seconds

- [x] 2026-07-05: **Session sweep, all multiplayer-tested same day:** car.gd split (1233 → 912; doors/cargo, seats/interact, audio, drone dock → controller nodes, RPC paths unchanged) · two player.gd multiplayer bugs (remote collision shape stuck disabled after seat exit; shared crouch capsule — also retro-solved the old "player sunk in the ground after crouch" mystery) · NTM keepalive for dropped rest-state packets · turret jitter on host (raw vs interpolated pivot mix in barrels/convergence — diagnosed, predicted, confirmed in-session, fixed)

- [x] Already built (confirmed by code audit 2026-07-04): **nitro boost** (3 charges, exhaust VFX), **car jump** (Q, dust VFX), **flamethrower** (fuel system, 50 DPS), **rocket pot** (4-tube launcher), **rocket thrust** (charge-based, phased burn), **stasis cargo lock**, **level/return gates** (incl. objective unlock hook), **horde manager** (ghost promotion/demotion by distance), **wear shader** (visual side), **item behaviors** (armor plate, repair kit, bomb)
- [x] 2026-07: Git history rewrite: 1,078 MB of ghost blobs stripped (old hub/menu/world versions), 1.2 GB → 626 MB, current files bit-identical, full backup bundle in Backups. Verified on both machines after re-clone; commit history reads under dev names only
- [x] 2026-07: Audit branch tested in-game and merged into main (4 commits: junk removal, 170 orphans, menu strip)
- [x] 2026-07: Main menu stripped and rebuilt as clean scene (52 MB → 2 KB); layout bug fixed, car/drone netcode removed from menu
- [x] 2026-07: Design wiki built and live at cap7n.github.io/otr-docs
- [x] 2026-07: Full project audit; 170 dead files removed on `audit/2026-07-cleanup`
- [x] 2026-07: Start/end zone gates confirmed working (A→B→hub loop closed)
