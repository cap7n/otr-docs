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
- [ ] ⛔ **Junker package:** unlock flags per ability controller (+ peer sync), CAR_MOD items, shop wiring; blocked on the stakes decision ([open question 2](open-questions.md))
- [ ] ⛔ **Loot-dies-with-you + repair costs:** blocked on the same stakes decision
- [ ] **Flank enemy:** paces alongside the car in bursts, the honest "keeps up" enemy ([threat directions](../game/enemies.md))
- [ ] **Run modifiers:** confirmed absent; after core loop is solid ([plan](../systems/modifiers.md))
- [ ] **Callout/ping system:** confirmed absent; gunner marks shortcuts and threats for the driver
- [ ] **Boss rework:** benched; doesn't feel good yet, needs love before any route depends on it

## Level design

- [ ] **First authored route in round1_a:** session-style beats between the existing start/end gates: opening encounter, complication, fork, climax (horde or set-piece, not boss), exit ([The Tunnels](../level-design/tunnels.md))
- [ ] **Cavern lighting test:** one gray-box cavern: baked LightmapGI + volumetric fog + light shafts + distant emissives; proves the megalophobia works ([Setting & Scale](../level-design/setting-and-scale.md))
- [ ] **Tunnel kit cross-section profile:** the one profile all modular pieces share; decide before modeling any kit piece
- [ ] **Blockout kit pieces:** straight, curves, squeeze, cavern shell, Y-junction, slope, portal, wall-drive ramp, alcove
- [ ] **Fix square shadows:** smooth the turret meshes; if that's not enough, raise positional shadow atlas size / light softness

## Code health (from the July 2026 audit)

- [ ] 🔨 **RPC sender validation on 4 input handlers:** running as background task; seat-shared controls (handbrake!) must keep working
- [ ] 🔨 **Globals.DEBUG flag + gate 50+ prints:** running as background task
- [ ] **Cache enemy target scans:** 5 enemy scripts call get_nodes_in_group every physics frame; horde_manager already shows the right pattern
- [ ] **Split car.gd (1233 lines) and player.gd (1072):** when next doing major work in them, not before
- [ ] **Fix `:=` typing violations:** mostly road_generator.gd (33) and terrain_conform.gd (15)

## Chores

- [ ] ⛔ **Project stretch mode:** add window/stretch canvas_items + expand to project.godot; waiting until the background code sessions land, then glance over every UI scene once
- [x] 2026-07: Audit branch tested and merged into main (4 commits: junk removal, 170 orphans, menu strip)
- [ ] **Rename schop_screen.tscn → shop_screen_panel or similar:** editor rename so references update
- [ ] **Remove level_test_texutures from world.tscn:** editor; drags an 11 MB collision shape with it
- [ ] **External_Carp terrain pack decision:** 49 MB, unknown licence, no references found; verify Terrain3D doesn't need it, then delete
- [ ] **Delete Audio/Recall.mp3 if unused:** verify in editor first
- [ ] **.git history rewrite:** 1.2 GB of VoxelGI-era bloat (hub.tscn alone: five 52 MB ancestors); needs git filter-repo + coordinated re-clone by both devs

## Parked (someday, after the game is fun)

- [ ] **Rebuild menu visuals:** menu was stripped to bare buttons (2026-07) after the 52 MB embedded 3D showcase broke layout and dragged netcode into the menu. Design a proper look when the game underneath deserves it

## Done

*(Move checked items here with a date, it feels good and it's useful history.)*

- [x] Already built (confirmed by code audit 2026-07-04): **nitro boost** (3 charges, exhaust VFX), **car jump** (Q, dust VFX), **flamethrower** (fuel system, 50 DPS), **rocket pot** (4-tube launcher), **rocket thrust** (charge-based, phased burn), **stasis cargo lock**, **level/return gates** (incl. objective unlock hook), **horde manager** (ghost promotion/demotion by distance), **wear shader** (visual side), **item behaviors** (armor plate, repair kit, bomb)
- [x] 2026-07: Main menu stripped and rebuilt as clean scene (52 MB → 2 KB); layout bug fixed, car/drone netcode removed from menu
- [x] 2026-07: Design wiki built and live at cap7n.github.io/otr-docs
- [x] 2026-07: Full project audit; 170 dead files removed on `audit/2026-07-cleanup`
- [x] 2026-07: Start/end zone gates confirmed working (A→B→hub loop closed)
