# Enemies & Obstacles

The current roster, all implemented and working.

## Hostiles

### Melee Orb
Sphere-type rusher. Wanders → hunts → charges the car. Explodes on death (full damage inner radius, falloff outer). Can be roadkilled, gets launched with speed-scaled impulse. ~50% loot drop chance.

### Flying Enemy
Aerial. Hovers, orbits, dive-attacks, and fires projectiles from above. Knockback + stagger on hit. Pooled for performance.

### Ranged Enemy
Ground shooter. Keeps distance, fires aimed projectiles. Vulnerable to being rammed.

### Boss (benched, "maybe I'll use it", 2026-07)
500 HP, phase-based: idle → charging → firing → cooldown, with flinch interrupts (25% on hit). Fires a tracking laser (25 DPS on target, leads the car's movement). **Enrages at 50% HP**, cycles 60% faster. Moves along a path.

!!! warning "Status"
    Doesn't feel good yet, needs love before it earns a place in a route. Don't design climaxes that depend on it: use a horde-in-cavern or an escape set-piece instead.

### Stationary Turrets (light / heavy)
Fixed emplacements that aim and fire at the car. Destructible.

### Artillery
Stationary cannon firing arcing shells.

## Non-hostile obstacles

### Junk Barricade
Destructible wall on the main path, ram it or shoot it. Shatters into physics chunks.

### Locked Gate
Blocks progress until its **weak point** is shot out. Multi-phase destruction.

## Spawning & pacing

- Spawn points are **hand-placed** in the level editor, pacing is authored, not procedural.
- A horde manager orchestrates waves; enemies are pooled (no instantiate/free churn).
- If the car never enters a spawn zone (e.g. took a shortcut around it), those enemies never spawn.

!!! tip "Design lens"
    Each enemy asks a different question of the two seats. Melee orbs: *ram or shoot?* Flying enemies: *only the gunner can reach them.* Ranged enemies: *close the distance (driver) or outshoot them (gunner)?* Gates: *gunner must hit the weak point while the driver holds position under fire.* Encounters get interesting when types are mixed so both seats are busy. See [Co-op Design Principles](../co-op-design.md).

## Threat directions (design principles, 2026-07)

The core problem of vehicle combat: enemies end up behind a fast car, and a good driver never needs the gunner. Rules to design around it:

1. **Never rubber-band.** Enemies that magically match car speed punish good driving. Threat comes from *relative* speed, and the level controls the car's speed.
2. **Slow zones are catch-up windows.** Chasers accumulate behind the car and only become dangerous where the level forces a slowdown (flooded section, squeeze, debris, hairpin). A good driver arrives at the slow zone with a smaller pack. Rear threat is a pressure gauge, not a constant chore.
3. **The gunner's main job is forward support, not rear-guard.** The existing roster already provides it: stationary turrets, artillery, ranged enemies along the route, barricades, gate weak points, pre-triggerable stalactites. Gunner clears the path faster than the car arrives.
4. **Roster gap: the flank.** A future enemy that paces alongside the car in short bursts (lunge, cling, fall back, never infinite pursuit) is the honest version of "enemies that keep up". Visible out the side window, actively doing damage, clearly behavioral rather than rubber-banded.
