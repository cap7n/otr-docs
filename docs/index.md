# OTR Design Wiki

**OTR is a 2-player co-op car game.** You are two droids kept alive by the car you drive. One drives; the other operates the turret or pilots a scout drone. Together you take your armed, upgradeable car out of the garage and into the zones of a vast megastructure, fight what lives there, grab what it drops, and make it home to recharge, sell, repair, and upgrade. The world shifts between visits; the way back is never guaranteed ([World & Structure](level-design/world-structure.md)).

Built in **Godot 4.7**. Co-op runs over **Steam** peer-to-peer.

---

## The pitch in one line

*A dungeon crawl you drive through, one pair of hands on the wheel, the other on the trigger, and the dungeon rearranges itself while you sleep.*

## The core idea

Most driving games are solo experiences with passengers. OTR is designed around **two seats that both matter**:

- The **driver** handles the road: hazards, speed checks, jumps, path choices, wall-drive sections.
- The **co-driver** handles everything else: manning the turret, spotting hidden shortcuts, piloting the drone to scout ahead, calling out threats.

Every encounter, hazard, and secret is designed to ask two questions at once: *what is the driver doing, and what is the co-driver doing?*

## Where the game is right now

| Area | Status |
|---|---|
| Car physics (custom wheels, Jolt) | ✅ Working |
| Steam co-op + netcode (StateBuffer sync) | ✅ Working |
| Seats: driver / passenger / turret / drone | ✅ Working |
| Enemies (melee, flying, ranged, boss, turrets) | ✅ Working |
| Hub with shop, loot, cargo stasis | ✅ Working |
| round1_a | 🧪 Tech demo/testbed (outdoor terrain, ~1.4×2.5 km); proved gates, hordes, telemetry |
| The real level (tunnel) | 📋 Not started; begins with kit profile + blockout |
| Run gates (start zone → end zone → hub) | ✅ Working, incl. objective unlock hook |
| Car abilities: nitro, jump, flamethrower, rockets | ✅ Built and live |
| Car abilities: wall-drive, drift | ⚠️ Coded, switched off (setup commented out) |
| Environmental hazards | 📋 Planned |
| Shortcuts & secret paths | 📋 Planned |
| Run modifiers | 📋 Planned |
| Win condition / extraction | ❓ Undecided, see [Open Questions](project/open-questions.md) |

## How to use this wiki

Start with the [Game Loop](game/loop.md) to understand the run structure, then [What Players Can Do](game/player-verbs.md) for the full verb list. The **Systems** section holds the design plans for upcoming features. [The Tunnels](level-design/tunnels.md) is the active level-design work.

!!! note "The one rule of this wiki"
    **This wiki records decisions, it doesn't replace making them.** If you catch yourself writing pages about things that haven't been decided, stop and put it in [Open Questions](project/open-questions.md) instead.
