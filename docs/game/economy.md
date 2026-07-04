# Economy & Loot

The material loop that makes runs worth repeating.

## The flow

```
Enemies drop loot → pick up → stash in cargo box → survive → sell in hub → buy upgrades → stronger runs
```

## Loot

- Enemies have a drop chance (melee orbs ~50%) pulling from loot tables.
- Items are physical objects in the world, picked up on foot or collected near the car.
- Items are defined as **ItemData resources**: display name, price, icon, behavior script, throwable flag, special action. Behaviors hook `on_pickup`, `on_throw_impact`, `on_special_action`, `on_held_process`.

## Cargo stasis

The trailer carries a **cargo box with a stasis field**, items placed inside are locked in place and travel with the vehicle. This is the "backpack" of the run: what's in the box is what you're hauling home.

Loot stored in stasis persists between runs.

## Shop

Terminal in the hub. Buy and sell. Item categories:

- **WEAPON:** offense
- **UTILITY:** bombs, repair kits, armor plates
- **CAR_MOD:** car upgrades; planned to gate abilities like jump and wall-drive
- **LOOT:** sellable valuables

## Currency

Earned by selling loot. [Run modifiers](../systems/modifiers.md) will scale currency income (harder run = bigger multiplier).

## Open economic questions

- **What do you lose on death?** Carried loot? Everything since the last hub visit? Nothing? This defines how much tension the run has. → [Open Questions](../project/open-questions.md)
- **Is hauling a choice?** If the cargo box has limited space, "what do we keep" becomes a co-op negotiation. Undecided.
