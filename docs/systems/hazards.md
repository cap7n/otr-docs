# Environmental Hazards

*Status: planned. Source: `environmental_hazards_plan.md`.*

## What

The tunnel itself is dangerous, not just the enemies. Falling rocks, steam vents, flooded sections, fire patches, collapsing floors, swinging obstacles. Hand-placed in the level editor at specific points.

## Why

Without hazards, the breather sections between encounters are just empty road. Hazards give the driver something meaningful to do when no enemies are around, and they **combine** with enemies during combat: fighting chasers while crawling through a flooded section is more interesting than either challenge alone. The tunnel feels alive instead of being a static backdrop.

## Design principles

- **Readable**, every hazard telegraphs BEFORE it hits. No unfair surprise damage.
- **Driver-focused**, hazards test reactions and path choice. The gunner can sometimes help (shoot a stalactite early), but driving skill is the main defense.
- **Non-lethal individually**, one hazard does moderate damage or disrupts movement. Danger comes from combinations.

---

## Hazard roster

| Hazard | Challenge type | Tell |
|---|---|---|
| **Falling rocks** | Speed rewards, outrun the drop. Gunner can pre-trigger stalactites. | Falling dust, pebbles ~0.5s early, cracking sound |
| **Steam vents** | Pattern reading, 2s on / 3s off cycle; push force + light damage | Hiss + glow 1s before blast |
| **Flooded section** | Momentum, drag and traction loss; deep water stalls the engine. Rewards commitment, punishes hesitation | Visible water, shallow → deep |
| **Fire patches** | Path choice, fires don't cover the full width; pick a line. Tick damage | Fire + orange wall glow, crackling |
| **Collapsing floor** | Speed check, fast clears the gap, slow falls in. "Hit nitro NOW" moments | Floor cracks, cracking audio, crumbles edge-in |
| **Swinging obstacles** | Timing, pendulums across the tunnel; blast through between swings or wait | Always visible + creaking metal |

## Placement philosophy

- **Breather sections:** 1–2 hazards as the only challenge. Driver-focused, no enemies.
- **During encounters:** lighter hazards (one vent, one fire patch) combined with enemies.
- **Boss fight:** the boss can trigger hazards as attack patterns (laser ignites fuel barrels; slams collapse floor).

## Build order

1. Steam vent, simplest (timer cycle, push, tick damage)
2. Fire patch
3. Falling rocks
4. Flooded zone (drag/friction modifiers)
5. Collapsing floor
6. Swinging obstacles
7. Combine with enemy spawns in the tunnel
8. Boss hazard integration
