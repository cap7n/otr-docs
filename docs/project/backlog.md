# Backlog

Things we've said **yes** to that aren't built yet. Not to be confused with [Open Questions](open-questions.md) (undecided) or the [Roadmap](roadmap.md) (the big-picture order). This is the working list: pick an item, build it, check it off.

Conventions: `🔨` = in progress · `⛔` = blocked by a decision or another item · unmarked = ready to pick up.

## Gameplay systems

- [ ] **Nitro boost** — first car ability, simplest, enables speed-gated level design ([plan](../systems/car-abilities.md))
- [ ] **Car jump** — grounded-only impulse; input conflict (Space = handbrake) must be resolved first ⛔ [open question](open-questions.md)
- [ ] **Wall-drive prototype** — test Jolt per-body gravity on a simple ramp BEFORE building zones ([plan](../systems/car-abilities.md))
- [ ] **First hazards: steam vent + fire patch** — simplest two from the [hazards plan](../systems/hazards.md)
- [ ] **Remaining hazards** — falling rocks, flooded zone, collapsing floor, swinging obstacles
- [ ] **First shortcut: destructible wall + side path** — reuses barricade system ([plan](../systems/shortcuts.md))
- [ ] **Interactable loot chest** — opens on E, loot table, server-authoritative
- [ ] **Gate countdown UI** — TODOs already in level_gate.gd and return_gate.gd
- [ ] **Save file** — user:// ConfigFile autoload for currency + unlocks; prerequisite for junker and modifier unlocks
- [ ] ⛔ **Junker package** — unlock flags per ability controller (+ peer sync), CAR_MOD items, shop wiring; blocked on the stakes decision ([open question 2](open-questions.md))
- [ ] ⛔ **Loot-dies-with-you + repair costs** — blocked on the same stakes decision
- [ ] **Flank enemy** — paces alongside the car in bursts, the honest "keeps up" enemy ([threat directions](../game/enemies.md))
- [ ] **Run modifiers** — after core loop is solid ([plan](../systems/modifiers.md))
- [ ] **Callout/ping system** — gunner marks shortcuts and threats for the driver
- [ ] **Boss rework** — benched; doesn't feel good yet, needs love before any route depends on it

## Level design

- [ ] **First authored route in round1_a** — session-style beats between the existing start/end gates: opening encounter, complication, fork, climax (horde or set-piece, not boss), exit ([The Tunnels](../level-design/tunnels.md))
- [ ] **Cavern lighting test** — one gray-box cavern: baked LightmapGI + volumetric fog + light shafts + distant emissives; proves the megalophobia works ([Setting & Scale](../level-design/setting-and-scale.md))
- [ ] **Tunnel kit cross-section profile** — the one profile all modular pieces share; decide before modeling any kit piece
- [ ] **Blockout kit pieces** — straight, curves, squeeze, cavern shell, Y-junction, slope, portal, wall-drive ramp, alcove
- [ ] **Fix square shadows** — smooth the turret meshes; if that's not enough, raise positional shadow atlas size / light softness

## Code health (from the July 2026 audit)

- [ ] 🔨 **RPC sender validation on 4 input handlers** — running as background task; seat-shared controls (handbrake!) must keep working
- [ ] 🔨 **Globals.DEBUG flag + gate 50+ prints** — running as background task
- [ ] **Cache enemy target scans** — 5 enemy scripts call get_nodes_in_group every physics frame; horde_manager already shows the right pattern
- [ ] **Split car.gd (1233 lines) and player.gd (1072)** — when next doing major work in them, not before
- [ ] **Fix `:=` typing violations** — mostly road_generator.gd (33) and terrain_conform.gd (15)

## Chores

- [ ] **Main menu layout fix** — reparent SubViewportContainer out of RightLabel, Full Rect anchors (editor, ~5 min; diagnosis in session notes)
- [ ] ⛔ **Project stretch mode** — add window/stretch canvas_items + expand to project.godot; waiting until the background code sessions land, then glance over every UI scene once
- [ ] **Merge `audit/2026-07-cleanup` into main** — after running the game on the branch once
- [ ] **Rename schop_screen.tscn → shop_screen_panel or similar** — editor rename so references update
- [ ] **Remove level_test_texutures from world.tscn** — editor; drags an 11 MB collision shape with it
- [ ] **External_Carp terrain pack decision** — 49 MB, unknown licence, no references found; verify Terrain3D doesn't need it, then delete
- [ ] **Delete Audio/Recall.mp3 if unused** — verify in editor first
- [ ] **.git history rewrite** — 1.2 GB of VoxelGI-era bloat; needs git filter-repo + coordinated re-clone by both devs

## Done

*(Move checked items here with a date, it feels good and it's useful history.)*

- [x] 2026-07: Design wiki built and live at cap7n.github.io/otr-docs
- [x] 2026-07: Full project audit; 170 dead files removed on `audit/2026-07-cleanup`
- [x] 2026-07: Start/end zone gates confirmed working (A→B→hub loop closed)
