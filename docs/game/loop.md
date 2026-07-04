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

- **Shop terminal:** buy upgrades and items with currency earned from runs. Categories: weapons, utility, car mods, loot.
- **Sell platform:** turn loot from the tunnels into currency.
- **Stasis cargo zone:** a cargo box on the trailer where items are locked in place and travel with the car. Loot stored here carries between runs.
- **Modifier terminal** *(planned)*: both players vote on [run modifiers](../systems/modifiers.md) before departing.

## 3. The Run

Drive into the tunnel. While inside:

- **Fight:** enemies attack the car; the gunner shoots, the driver can ram or use the flamethrower.
- **Navigate:** environmental hazards test the driver ([hazards plan](../systems/hazards.md)).
- **Loot:** enemies drop items; pick them up and stash them in the cargo box.
- **Explore:** hidden shortcuts and loot rooms reward the co-driver for paying attention ([shortcuts plan](../systems/shortcuts.md)).

## 4. Run end

- **Lose:** the car is destroyed → death screen → back to the hub. *(What happens to carried loot on death is an [open question](../project/open-questions.md).)*
- **Finish:** ✅ implemented, mechanically. The level has a **start zone** and an **end zone** (level gate / return gate: detect + countdown); reaching the end zone puts you back into the hub. A→B works.
- **Bonus discovery (code audit 2026-07):** the return gate is **locked by default** and exposes `unlock()`, meant to be called "when the level's objective is complete". The mounting point for a run goal already exists in code; nothing calls it yet.
- **Goal:** ❓ **Undecided.** Reaching B doesn't *mean* anything yet, no reward for arriving, no pressure on the way, no reason to hurry or to detour. The skeleton is done; the stakes are the open design question. See [Open Questions](../project/open-questions.md).

## 5. Back in the hub

Sell loot → buy upgrades → repair → pick modifiers → go again. Currency and unlocks persist; the loop is the game.

!!! warning "The missing piece"
    The full loop (hub → run → end zone → hub) exists in the game today. What's missing is the *why*: what makes reaching the end zone matter, and what turns the drive in between into a run worth repeating. That decision (extraction pressure vs. authored gauntlet, see [Open Questions](../project/open-questions.md)) shapes every level-design decision downstream.
