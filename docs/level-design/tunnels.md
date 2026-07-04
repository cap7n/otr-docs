# The Tunnels

*The active level-design work. Current level: `round1_a.tscn`. An older prototype (`tunnel_level.tscn`) is archived in the project root.*

## Why tunnels

The setting is a design decision, not just a vibe:

1. **Confinement solves the blank-page problem.** An open zone has 360 degrees of "what goes here?" A tunnel has two directions: ahead and behind. Level design collapses from *fill a world* to *author a sequence*.
2. **A tunnel IS a route.** In a driving game the level isn't a zone, it's what happens between A and B. Tunnel walls enforce the route for free.
3. **Cheap where we're weak, demanding where we're strong.** No terrain, skyboxes, or vistas. What tunnels need instead (lighting, fog, audio, pacing) is exactly what the existing post-processing stack (volumetric fog, SSAO, SDFGI, headlights) is built for.
4. **Confinement amplifies co-op.** The driver can't just swerve away from danger, which makes the gunner and drone matter more.
5. **A tunnel network is a dungeon you drive through.** Level design here maps one-to-one onto D&D session prep: beats, tension and release, decision points, a climax, an exit.

## Room grammar

The failure mode of tunnels is monotony. The fix is varying the space itself, each "room type" creates a different kind of play:

| Space | What it does |
|---|---|
| **Narrow squeeze** | Tension. Precision driving, no room to dodge, hazards hit harder |
| **Cavern opening** | Release. Fights with room to maneuver, ambush potential, flying enemies shine |
| **Junction / fork** | Decision. Risk/reward path choice ([shortcuts](../systems/shortcuts.md)) |
| **Collapsed section** | Pace break. Drone scouts, on-foot beat, or gate weak-point puzzle |
| **Wall-drive section** | Spectacle. Road curves up the wall/ceiling ([car abilities](../systems/car-abilities.md)) |
| **Breather stretch** | Recovery. 1–2 hazards only, no enemies ([hazards](../systems/hazards.md)) |

## Design a route like a session

Not a world, a session. Each run route gets:

1. **Opening beat**, establish mood, easy first encounter
2. **Complication mid-route**, hazard + enemy combination, or a fork
3. **Decision point**, risky shortcut vs. safe long way
4. **Climax**, set-piece: boss, horde in a cavern, collapsing-floor escape
5. **Exit**, depends on the [win-condition decision](../project/open-questions.md)

**The two-seat test for every beat:** what is the driver doing, and what is the co-driver doing? If the answer to either is "nothing," the beat needs work.

## Atmosphere

The target feel: headlights cutting through fog in the dark. Assets on hand: tunnel lights, ceiling lights, billboard fog zones, burning-ash embers, tire smoke, the full post-processing stack.

!!! bug "Known issue: blocky shadows"
    Shadows in the tunnel rendered visibly square. Suspected cause: unsmoothed turret meshes casting faceted shadows. If fixing normals doesn't cure it, check `positional_shadow/atlas_size` in project settings and light softness, near-surface lights in tunnels expose low shadow-map resolution badly.

## Status

- [x] Tunnel level exists (`round1_a.tscn`) with enemies, loot, hub connection
- [ ] Win condition / run ending, **undecided, blocks route design**
- [ ] Hazards placed
- [ ] Shortcuts / forks placed
- [ ] Wall-drive sections
- [ ] Lighting & atmosphere pass
- [ ] First fully-authored 10-minute route, beat by beat
