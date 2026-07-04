# Open Questions

Things not yet decided. When one gets answered, move it to the [Decision Log](decisions.md) with its *why*.

## Blocking level design

### 1. What ends a run? ⭐ *the big one*

There is currently no win condition in the game. Two shapes fit what's already built:

- **Extraction-shaped:** drive in, loot, something turns the screws (time? escalating spawns? a "storm"?), get out or lose what you're carrying. Fits the existing loot/sell/upgrade economy. Leads to loop/branch tunnel networks.
- **Linear gauntlet:** authored corridor, reach the end, beat the boss. Fits the existing boss and hand-placed pacing. Leads to one authored route per level.

The answer shapes the tunnel layout, the economy stakes, and what "pressure" means. **Decide before building more level.**

### 2. What do you lose on death?

Carried loot? Everything since the hub? Nothing? Defines run tension and how much extraction matters.

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
