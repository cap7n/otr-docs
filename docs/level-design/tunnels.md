# The Tunnels

*The active level-design work. No tunnel level exists yet: `round1_a.tscn` is an outdoor tech demo/testbed (it proved gates, hordes, and terrain), and the old `tunnel_level.tscn` prototype was removed in the July 2026 cleanup (recoverable from git history). The real level starts with the kit profile and blockout.*

## Where tunnels fit (the megastructure model)

Since the [World & Structure](world-structure.md) decision, "the level" is **two layers**, and this page is about the second:

- **Zones** are the authored *destinations* - ~2 km hand-built spaces you drive into, fight and loot through, and exit through one of four wall gates. The full session arc (opening -> complication -> fork -> climax -> exit) is authored *here*; the [first authored zone](../project/backlog.md) is the current headline level-design task.
- **Tunnels** are the *connective tissue* between zones - squeezes, caverns, junctions, wall-drive sections - and double as the diegetic loading screen: a tense 5-10 minute drive during which the old zone unloads and the next streams in, with no loading screen ever shown.

The room grammar below is the shared vocabulary for both, but tunnels own confinement, spectacle (wall-drive), and the between-zone breather, while zones own the encounter-heavy set-pieces. Everything under "Why tunnels" is why confinement is the right *default* shape for OTR's level design.

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
| **Breather stretch** | Recovery. 1-2 hazards only, no enemies ([hazards](../systems/hazards.md)) |

## Design a route like a session

Not a world, a session. This is the arc of an **authored zone** (and it shapes longer tunnel stretches too). Each run route gets:

1. **Opening beat**, establish mood, easy first encounter
2. **Complication mid-route**, hazard + enemy combination, or a fork
3. **Decision point**, risky shortcut vs. safe long way
4. **Climax**, set-piece: boss, horde in a cavern, collapsing-floor escape
5. **Exit**, depends on the [win-condition decision](../project/open-questions.md)

**The two-seat test for every beat:** what is the driver doing, and what is the co-driver doing? If the answer to either is "nothing," the beat needs work. (The full test lives in [Co-op Design Principles](../co-op-design.md).)

## Atmosphere

The target feel: headlights cutting through fog in the dark. Assets on hand: tunnel lights, ceiling lights, billboard fog zones, burning-ash embers, tire smoke, the full post-processing stack.

!!! bug "Known issue: blocky shadows"
    Shadows in the tunnel rendered visibly square. Suspected cause: unsmoothed turret meshes casting faceted shadows. If fixing normals doesn't cure it, check `positional_shadow/atlas_size` in project settings and light softness, near-surface lights in tunnels expose low shadow-map resolution badly.

## Status

- [x] Tech demo level (round1_a) proved the loop: gates, spawns, enemies, loot, hub connection
- [ ] Tunnel level itself, not started
- [ ] Win condition / run ending, **undecided, blocks route design**
- [ ] Hazards placed
- [ ] Shortcuts / forks placed
- [ ] Wall-drive sections
- [ ] Lighting & atmosphere pass
- [ ] First fully-authored zone route (~10 minutes), beat by beat
