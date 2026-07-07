# Roadmap

Rough sequencing. The project runs issue-driven — solve one system, ship it, move on — but this is the intended order of battle. It builds toward the [megastructure model](../level-design/world-structure.md): a run leaves the garage into an authored neighbouring zone and exits through one of its four wall gates.

## Done

- Custom car physics on Jolt (raycast suspension, ported from prototype)
- Steam P2P co-op, lobby, ready-check
- Netcode overhaul: NetworkTickManager + StateBuffer/Hermite interpolation
- Seat system: driver / passenger / turret / drone
- Enemy roster: melee, flying, ranged, boss, stationary turrets, artillery
- Destructibles: barricades, locked gates (incl. objective-unlock hook)
- Hub: shop, sell platform, stasis cargo
- Loot & currency loop
- Start/end zone gates (A→B→hub loop closed)
- **Car abilities: nitro, jump (Q), flamethrower, rocket pot, rocket thrust** — all built and live
- Engine audio system (recorded source, RPM-band crossfade blender, virtual gearbox, D/S/T drive modes)
- Post-processing stack (fog, SSAO, SDFGI, glow, custom shader)
- Tunnel testbed `round1_a` (geometry + spawns) — a tech demo, not the target level

## Now — make one run fun

1. **Decide the run ending & stakes** ([open question #1](open-questions.md)) — blocks everything below
2. Fix tunnel shadows; first lighting/atmosphere pass
3. **Author the first zone** beat-by-beat: opening encounter → complication → fork → climax → exit gate ([World & Structure](../level-design/world-structure.md), [The Tunnels](../level-design/tunnels.md))
4. First hazards: steam vent, fire patch ([hazards](../systems/hazards.md))
5. First shortcut: destructible wall + side path ([shortcuts](../systems/shortcuts.md))

## Next — depth

- Re-enable wall-drive (Jolt gravity test first) and drift — both coded, currently switched off
- Remaining hazards; collapsing-floor set-pieces
- Loot rooms, timed gates, risk/reward forks
- Battery leash + drone signal tether (on-foot and scouting pressure)
- Boss rework (benched 2026-07: doesn't feel good yet); route climaxes use hordes/set-pieces meanwhile
- Callout/ping system for co-op communication

## Later — replayability & polish

- [Run modifiers](../systems/modifiers.md) + voting terminal
- Save file + junker start / CAR_MOD progression (gated on the saving decision)
- Car cosmetics; wear & tear shader wired to real damage
- Slow-mo impact moments
- Ghost car replay integration
- Second authored zone
- Art direction pass (currently undecided)
