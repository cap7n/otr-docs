# Open Questions

Things not yet decided. When one gets answered, move it to the [Decision Log](decisions.md) with its *why*.

## Blocking level design

### 1. What makes a run matter? ⭐ *the big one*

The mechanical loop is done: start zone → end zone → back to hub (A→B works). But reaching B means nothing yet, no reward for arriving, no pressure on the way, no goal. Two shapes fit what's already built:

- **Extraction-shaped:** drive in, loot, something turns the screws (time? escalating spawns? a "storm"?), get out through the end zone or lose what you're carrying. Fits the existing loot/sell/upgrade economy. Leads to loop/branch tunnel networks.
- **Linear gauntlet:** authored corridor, reach the end, beat the boss. Fits the existing boss and hand-placed pacing. Leads to one authored route per level.

Either way the existing end-zone gate is the finish line; the question is what gives the drive to it stakes. The answer shapes the tunnel layout, the economy stakes, and what "pressure" means. **Decide before building more level.**

### 2. Stakes: what do you have to lose? (proposal on the table, 2026-07)

First playtests confirmed it: without something to lose, the game doesn't grip, even its own devs. Proposed package, built entirely from existing systems, awaiting both devs' sign-off:

1. **Loot dies with you.** Cargo in the stasis box only becomes yours at the hub. Makes the final stretch with a full box tense, and detours a real decision.
2. **Repairs cost currency.** Car health already persists between runs; price the damage.
3. **Start with a junker.** Weak engine, no nitro/flamethrower, basic turret. Abilities and power are bought as CAR_MOD items (this would answer the "unlocked vs bought" question below: bought). Rule: underpowered must never mean unresponsive, weak stats with good feel.

Together: earn it, risk it, lose it. That is the engagement loop.

## Setting (see [Setting & Vertical Scale](../level-design/setting-and-scale.md))

- **Who built the underground world and what happened to them?** Mining colony that dug too deep / wartime bunker-city / failed corporate arcology. Each implies different signage, machine types, and what the enemies are. Pick enough to keep props consistent, no novel required.
- **Is the vastness beautiful or hostile?** Sublime-eerie (Subnautica) vs. grim-industrial (Metro). Both evoke megalophobia; the choice sets the lighting palette.

## Design

- **Are car abilities (jump, wall-drive) unlocked from the start or bought as CAR_MODs?**
- **Is cargo space limited?** If yes, "what do we keep" becomes a co-op negotiation.
- **Jump input:** Space conflicts with handbrake. Tap/hold split, or separate key (Q)?
- **`R` key conflict:** wall-drive vs. fire rocket, one has to move.
- **Art style:** post-processing is in place, but the overall art direction is undecided. Discuss before implementing.

## Technical (needs testing, not discussion)

- Jolt per-body gravity direction support (wall-drive prerequisite)
- Square shadows in the tunnel, mesh normals fix, else shadow atlas size / light softness
