# The Car

The car is the real protagonist of OTR. The two droids are just hands; the car is **power, life, and colour** - the moment they plug in, the world blooms from gray to vivid ([World & Structure](../level-design/world-structure.md)). This page is what the car *is* to the player and why it matters. The mechanics-level detail lives in [Car Abilities](../systems/car-abilities.md); the engine/audio internals live in [Sound & Engine Audio](../systems/audio.md).

## What the car is

A walking contradiction, like the world: a 70s-90s American muscle body, a Cobra-style V8, and anachronistic tech bolted on - a railgun on the roof, a scout drone in the trailer. Different eras colliding in one machine, which is the world's whole premise on four wheels - and the reason upgrades can span junkyard scrap to futuristic tech without breaking the fiction.

It's also the co-op living room. Both droids live inside it, both hear the same engine, and outside it they're on a dying [battery leash](../level-design/world-structure.md). The car isn't where the game happens - the car is *why* there's a game.

## Two seats that both matter

The car provides the four positions the whole game is designed around - **Driver, Gun, Drone, Passenger** (plus on-foot). Players switch freely; role fluidity is a core mechanic, not a convenience. The full verb list per seat is in [What Players Can Do](../game/player-verbs.md).

## Drive modes - the car as a tool you pick

The driver cycles a **drive mode** (key **M**), and the choice shapes real handling, not just the sound:

| Mode | The pitch | Feels like |
|------|-----------|------------|
| **D** - Drive | Precision & control | Soft, forgiving throttle; climbs and threads hazards; ~70% top speed |
| **S** - Sport | Quick and civil | Responsive; the everyday tool for tight zones; ~90% top speed |
| **T** - Track | Flat out | Instant throttle, full top speed, no overdrive; open stretches and escapes |

**Why it's a mode, not automatic:** the game never guesses how hard you *meant* to press the throttle - the mode **is** your stated intent. That keeps the car honest on a keyboard and turns "drop to D for this squeeze, kick to T to run" into a real driving decision. (The gearbox and shift feel are virtual; see [audio](../systems/audio.md).)

## What the driver can do

Beyond steer and throttle, the car has active abilities that make driving its own skill game:

- **Nitro** - a burst of speed to punch through barricades, clear gaps, or escape a swarm. ✅ Built
- **Jump** (Q) - launch the car to clear gaps and obstacles; pairs with nitro. ✅ Built
- **Flamethrower** - a close-range fuel-fed cone for enemies in the driver's face. ✅ Built
- **Rocket pot** - a roof launcher the driver fires forward. ✅ Built
- **Rocket thrust** - a phased burn with nose-down force for big air and mid-jump control. ✅ Built
- **Wall-drive** - drive up walls and across ceilings through marked zones. ⚠️ Coded, switched off
- **Drift** - controlled slides through corners. ⚠️ Coded, switched off

*(Status verified against code, 2026-07. Full behaviour and build order in [Car Abilities](../systems/car-abilities.md).)*

!!! note "Combat direction"
    Under the [combat split](../project/decisions.md), the driver deals **no direct damage** - ramming only - and all guns belong to the co-pilot ([Weapons & Combat](../game/weapons-combat.md)). The flamethrower and rocket pot above are built on the driver but predate that rule; where they land is an [open question](../project/open-questions.md). The driver's future kit is mobility plus **space-making** (AoE stun / push-away), not offense.

## The trailer: cargo, drone, and reach

The car tows a **trailer**, and the trailer is the run's whole economy in physical form:

- A **stasis cargo box** locks loot in place so it rides home with you - the "backpack" of the run. What's in the box is what you're hauling ([Economy & Loot](../game/economy.md)).
- The **scout drone** launches from here and extends the crew's reach into spaces the car can't fit, limited by signal range rather than time.

## Health, damage, and repair

The car has HP, takes damage from enemies and hazards, and is repaired back in the hub (repair kits patch it mid-run). The **wear shader** - scratches, rust, and dirt accumulating on the body - is built to *show* this at a glance, though it isn't yet driven by real damage ([backlog](../project/backlog.md)).

!!! warning "Undecided"
    The exact damage model - how much HP, how repair is priced, what a beaten-up car actually costs you - isn't specified yet, and it's tangled up with what death costs. See [Open Questions](../project/open-questions.md).

## Fuel is the leash

Range = fuel. Scavenging isn't only about getting richer; it's **runway** - literally how much further you get to drive before the car is stranded ([World & Structure](../level-design/world-structure.md)). Fuel is meant to be the standing pressure behind the two seats' constant argument: *push on to the next zone, or turn back while we still can?*

!!! warning "Undecided"
    Where fuel actually *comes from* - bought, scavenged, or just a run timer - and what running dry does, isn't settled. See [Open Questions](../project/open-questions.md).

## Making it yours: upgrades

The car is meant to grow. **CAR_MOD** items from the shop upgrade it and can gate abilities (the [junker start](../project/open-questions.md) direction: begin weak and buy your power), and cosmetics plus wear give it history. The rule that governs all of it: **underpowered must never mean unresponsive** - a weak car should still feel good to drive.

!!! tip "Design lens"
    Every question this page raises is really the same one: *does this make both seats matter?* A drive mode the gunner never notices, an ability that doesn't change what the co-driver should do, an upgrade that only helps the driver - those are single-player features wearing a co-op car. The good ones make the other seat react.
