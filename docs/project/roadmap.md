# Roadmap

Rough sequencing. The project runs issue-driven, solve one system, ship it, move on, but this is the intended order of battle.

## Done

- Custom car physics on Jolt (raycast suspension, ported from prototype)
- Steam P2P co-op, lobby, ready-check
- Netcode overhaul: NetworkTickManager + StateBuffer/Hermite interpolation
- Seat system: driver / passenger / turret / drone
- Enemy roster: melee, flying, ranged, boss, stationary turrets, artillery
- Destructibles: barricades, locked gates
- Hub: shop, sell platform, stasis cargo
- Loot & currency loop
- Post-processing stack (fog, SSAO, SDFGI, glow, custom shader)
- Tunnel level `round1_a` (geometry + spawns)

## Now, make one run fun

1. **Decide the run ending** ([open question #1](open-questions.md)), blocks everything below
2. Fix tunnel shadows; first lighting/atmosphere pass
3. Author one 10-minute route beat-by-beat ([The Tunnels](../level-design/tunnels.md))
4. Nitro boost (first car ability, simplest, enables speed-gated design)
5. First hazards: steam vent, fire patch ([hazards](../systems/hazards.md))
6. First shortcut: destructible wall + side path ([shortcuts](../systems/shortcuts.md))

## Next, depth

- Car jump; wall-drive prototype (Jolt gravity test first)
- Remaining hazards; collapsing floor set-pieces
- Loot rooms, timed gates, risk/reward forks
- Boss integration into the route climax
- Callout/ping system for co-op communication

## Later, replayability & polish

- [Run modifiers](../systems/modifiers.md) + voting terminal
- Car cosmetics; wear & tear shader
- Slow-mo impact moments
- Ghost car replay integration
- Second route / round1_b
- Art direction pass (currently undecided)
