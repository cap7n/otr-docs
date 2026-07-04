# Game Loop

The run structure, from boot to repeat.

```
Main Menu → Lobby (Steam) → Hub → Run (tunnel) → back to Hub → Run again…
                                      ↓
                              Car destroyed → Death screen → Hub
```

## 1. Lobby

Players connect over Steam P2P. Both players ready-check before the world loads.

## 2. Hub

The safe zone between runs. What's here:

- **Shop terminal** — buy upgrades and items with currency earned from runs. Categories: weapons, utility, car mods, loot.
- **Sell platform** — turn loot from the tunnels into currency.
- **Stasis cargo zone** — a cargo box on the trailer where items are locked in place and travel with the car. Loot stored here carries between runs.
- **Modifier terminal** *(planned)* — both players vote on [run modifiers](../systems/modifiers.md) before departing.

## 3. The Run

Drive into the tunnel. While inside:

- **Fight** — enemies attack the car; the gunner shoots, the driver can ram or use the flamethrower.
- **Navigate** — environmental hazards test the driver ([hazards plan](../systems/hazards.md)).
- **Loot** — enemies drop items; pick them up and stash them in the cargo box.
- **Explore** — hidden shortcuts and loot rooms reward the co-driver for paying attention ([shortcuts plan](../systems/shortcuts.md)).

## 4. Run end

- **Lose:** the car is destroyed → death screen → back to the hub. *(What happens to carried loot on death is an [open question](../project/open-questions.md).)*
- **Win:** ❓ **Undecided.** There is currently no win condition implemented — no extraction point, no "run complete" state. This is the single biggest open design question. See [Open Questions](../project/open-questions.md).

## 5. Back in the hub

Sell loot → buy upgrades → repair → pick modifiers → go again. Currency and unlocks persist; the loop is the game.

!!! warning "The missing piece"
    Everything above the "Run end" section exists in the game today. The loop currently has no *ending* — you can enter, fight, loot, and die, but not finish. Deciding what ends a run (extraction pressure? reaching the far end? boss kill?) shapes every level-design decision downstream.
