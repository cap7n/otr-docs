# Enemies & Obstacles

The current roster — all implemented and working.

## Hostiles

### Melee Orb
Sphere-type rusher. Wanders → hunts → charges the car. Explodes on death (full damage inner radius, falloff outer). Can be roadkilled — gets launched with speed-scaled impulse. ~50% loot drop chance.

### Flying Enemy
Aerial. Hovers, orbits, dive-attacks, and fires projectiles from above. Knockback + stagger on hit. Pooled for performance.

### Ranged Enemy
Ground shooter. Keeps distance, fires aimed projectiles. Vulnerable to being rammed.

### Boss
500 HP, phase-based: idle → charging → firing → cooldown, with flinch interrupts (25% on hit). Fires a tracking laser (25 DPS on target, leads the car's movement). **Enrages at 50% HP** — cycles 60% faster. Moves along a path.

### Stationary Turrets (light / heavy)
Fixed emplacements that aim and fire at the car. Destructible.

### Artillery
Stationary cannon firing arcing shells.

## Non-hostile obstacles

### Junk Barricade
Destructible wall on the main path — ram it or shoot it. Shatters into physics chunks.

### Locked Gate
Blocks progress until its **weak point** is shot out. Multi-phase destruction.

## Spawning & pacing

- Spawn points are **hand-placed** in the level editor — pacing is authored, not procedural.
- A horde manager orchestrates waves; enemies are pooled (no instantiate/free churn).
- If the car never enters a spawn zone (e.g. took a shortcut around it), those enemies never spawn.

!!! tip "Design lens"
    Each enemy asks a different question of the two seats. Melee orbs: *ram or shoot?* Flying enemies: *only the gunner can reach them.* Ranged enemies: *close the distance (driver) or outshoot them (gunner)?* Gates: *gunner must hit the weak point while the driver holds position under fire.* Encounters get interesting when types are mixed so both seats are busy.
