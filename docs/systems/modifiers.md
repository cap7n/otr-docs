# Run Modifiers

*Status: planned, lower priority — build after the core loop is solid. Source: `run_modifiers_plan.md`.*

## What

Before a run, players pick modifiers that change the rules: harder for better rewards, different playstyles, or pure chaos. Think Hades' Pact of Punishment or Risk of Rain 2's artifacts. Both players vote in the hub before departing — a pre-run negotiation moment ("do we take the hard modifier for double loot?") that reinforces the co-op dynamic.

## Why

Without modifiers, every run plays the same. Risk/reward trade-offs give skilled players a reason to push themselves; the voting creates co-op discussion before the run even starts.

---

## Difficulty modifiers (risk/reward)

| Modifier | Effect | Currency bonus |
|---|---|---|
| **Tough Horde** | Enemies +50% HP | +30% |
| **Swarm** | 50% more enemies per spawn | +40% |
| **Fragile Ride** | Car −30% max HP | +25% |
| **No Brakes** | Minimum speed enforced (auto-accelerate to 30 km/h) | +20% |
| **Dark Tunnels** | More fog, fewer lights | +25% |
| **Aggro** | 2× detection range, more frequent attacks | +35% |

## Playstyle modifiers

| Modifier | Effect |
|---|---|
| **Speed Demon** | Top speed +40%, braking −50% |
| **Glass Cannon** | Turret damage ×2, car damage taken ×1.5 |
| **Scavenger** | No shop this run, loot drops ×3 |
| **Lone Wolf** | Turret auto-aims (weaker); one player controls everything |
| **Bomber Run** | Start with 5 bombs; enemies drop bombs instead of loot |
| **Heavyweight** | Car mass ×2 — tankier, slower, devastating rams |

## Fun / chaos modifiers

| Modifier | Effect |
|---|---|
| **Low Gravity** | Gravity 60% — car floats on bumps, enemies bounce |
| **Big Head Mode** | Enemy meshes ×2 — easier to hit, looks ridiculous |
| **Turbo Fuse** | All explosions ×3 radius (theirs AND yours) |
| **Ricochet** | Turret bullets bounce off walls once |
| **Earthquake** | Random shake + physics impulses every 10–20s |

---

## Design principles

- **Modifiers are data flags, not code injections.** Each is a resource file with an ID; game systems check the flag and adjust their own behavior. No central "apply all modifiers" function.
- Adding a modifier = one resource file + one check in the affected system.
- **Conflicts** declared per modifier (e.g. Speed Demon × No Brakes) — selecting one greys out the other.
- **Progressive unlock:** some modifiers appear only after N completed runs; chaos modifiers after the first boss kill.

## Selection flow

Terminal in the hub. Grid of modifier cards by category. Either player toggles; both see changes live (server-authoritative). Total currency multiplier shown. Both must press **Ready** to depart — no forced consensus, just communication.

## Persistence

Unlock state saves to disk. Active modifiers reset every run — set in hub, synced to peers, cleared at run end.

## Build order

1. RunModifier resource + ModifierManager autoload
2. One modifier end-to-end (Tough Horde)
3. Currency multiplier
4. Selection UI
5. Voting/ready system
6. Remaining difficulty modifiers → playstyle → fun
7. Unlock progression
8. Combo rewards (cosmetics for hard combos)
