# Weapons & Combat

The player's side of a fight - the mirror to [Enemies & Obstacles](enemies.md). The short version: **the car is the weapon, the crew isn't**, and the two seats do two completely different jobs that only add up together.

## The one combat rule

**On foot, the droids have no gun - ever.** Tools and throwables only. Some tools *can* do damage (a bomb still kills), but there is no infantry firefight, no aimed firearm in a droid's hands. Combat is something you do *from the car* - which is what makes combat something you do *together* ([Co-op Design Principles](../co-op-design.md)).

## Two jobs, one kill

The split between the seats is hard and deliberate:

- **Driver - no direct damage.** The only damage the driver deals is **ramming**. Everything else in the driver's kit is about moving the car, buying space, or setting the co-pilot up: nitro, jump, rocket thrust, wall-drive, drift, and **space-making** abilities - AoE stun and push-away tools that peel enemies off the car and open a firing line. The driver's job in a fight is position and disruption, never the killing blow.
- **Co-pilot - all the damage.** Every gun belongs to this seat. A car with an empty co-pilot seat can ram and shove, but it **cannot kill** - the driver is left exposed and half-blind, which is the feeling we want when nobody's on the guns.

!!! note "Design direction vs. current code"
    The driver currently has a flamethrower (50 DPS) and a 4-tube rocket pot in code - both direct-damage tools, both predating this rule. Where they land (move to the co-pilot, reframe the flamethrower as a non-damage push / area-denial tool, or cut) is an [open question](../project/open-questions.md). This page describes the target, not today's build.

## The co-pilot's arsenal

### Primary ballistic mount - default: rapid 50 cal
- **Role:** sustained anti-swarm DPS - the answer to numbers.
- **Swappable slot:** the 50 cal is one option in a mount that also takes a shotgun, a burst-fire gun, or RPM/handling tuning. This is the co-pilot's "build" choice.
- **Limit:** heat or ammo keeps it from being held down forever.

### Rebar / harpoon launcher - the signature
One launcher, two ammo modes:

- **Rebar:** big single hits - impale a heavy, pin a target in place, crack open destructibles and gate weak-points. Slow, heavy, punchy.
- **Harpoon:** the same launcher, cabled - latch an enemy so the driver can sling it into a wall or another enemy. This is the [north-star co-op combo](../co-op-design.md): the harpoon does almost no damage itself; the *driver's corner* is what kills.

It's near-irreplaceable, so instead of swapping the whole weapon it upgrades by **rebar material** - iron -> titanium - for more penetration and impale force. **Limit:** cooldown, one tether at a time. **Firing mechanism** (crossbow / gunpowder / air-pressure off the car / railgun) is [undecided](../project/open-questions.md).

### Rockets - burst & area
- **Role:** burst damage and AoE - clear a clump, or dump a lot of damage into a weak point.
- **Limit:** tube-based with per-tube cooldown. *(Currently wired as the driver's rocket pot - see the reconciliation note above.)*

## Ramming - the driver's only weapon

Mass x speed. Roadkill the small stuff (speed-scaled launch impulse), shove the big stuff into hazards or into each other. **Bumper and plow upgrades** are the driver's damage identity - they make ramming hit harder without ever handing the driver a trigger. Heavyweight-style mass upgrades lean all the way into it ([Economy & Loot](economy.md), [The Car](the-car.md)).

## On foot: tools, not guns

The unarmed rule with teeth. What the droids carry instead:

- **Repair** - patch the car mid-run.
- **Target designation** - a laser pointer that marks a target for the car's turret / 50 cal, so an on-foot droid becomes a **spotter** feeding the co-pilot. Pure co-op utility, no trigger.
- **Throwables / bombs** - can damage (a bomb kills), but they're thrown tools, not firearms.
- **Objective tools** - quest, switch, and gate interaction.

On foot you *enable*; you don't out-shoot.

!!! tip "Design lens"
    Every weapon question routes back to the pillar: *does it make the two seats multiply?* The 50 cal clears the swarm so the driver can commit to the corner; the harpoon only means anything because the driver finishes it. A weapon that lets one seat win a fight alone is off-design. See [Co-op Design Principles](../co-op-design.md).
