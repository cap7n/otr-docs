# What Players Can Do

The full verb list, per seat. This is the toolbox every level beat gets designed against.

## Seats

Seat state lives on the car: **Driver / Passenger / Gun / Drone** (plus on-foot). Players switch seats freely, `E` to enter driver/passenger, `1` for the drone, `2` for the gun.

## Driver

| Verb | Input | Notes |
|---|---|---|
| Steer | A / D | |
| Accelerate / brake | W / S | Auto-shifts between drive and reverse at standstill |
| Handbrake | Space | Also available to the passenger (seat-shared) |
| Nitro boost | Shift | ✅ Built: 3 charges, 1.5s burst, exhaust VFX |
| Car jump | Q | ✅ Built: grounded-only impulse, dust VFX |
| Rocket pot | R | ✅ Built: 4-tube launcher, cyclic fire, per-tube cooldown |
| Rocket thrust | N | ✅ Built: charge-based phased burn, nose-down force |
| Flamethrower | F | ✅ Built: fuel system (100 max, regen), 50 DPS cone |
| Wall-drive | R (toggle) | ⚠️ Coded but switched off: setup() commented out (car.gd:334). Input conflicts with rocket pot |
| Drift | via handbrake | ⚠️ Coded but switched off: setup() commented out (car.gd:329) |

## Gunner (turret)

| Verb | Input | Notes |
|---|---|---|
| Aim turret | Mouse | Yaw ±90°, pitch ±30° |
| Fire rockets | Fire button | |
| Scan surroundings | - | Elevated view; spots shortcut cues the driver can't see |

## Drone pilot

| Verb | Input | Notes |
|---|---|---|
| Fly | WASD + mouse | Full 3D flight |
| Ascend / descend | Space / Ctrl | |
| Rotate | Q / E | |
| Lock-on targeting | - | Target reticle |
| Scout | - | Fits where the car can't; finds hidden rooms |

The drone has limited lives per run.

## On foot

| Verb | Input | Notes |
|---|---|---|
| Walk / crouch / jump | WASD, Ctrl, Space | |
| Interact | E | Gaze-based, ~1.5 m range |
| Pick up items | automatic | In pickup zone |
| Charge-throw | hold E | Bombs and throwable items, ~1s charge |

## Shared / meta

- Switch seats at will (co-op role fluidity is a core mechanic)
- Shop terminal interaction in the hub
- Stasis cargo: stash loot in the trailer's cargo box

!!! tip "Design lens"
    A beat that only uses **driver** verbs is single-player content. The good stuff uses at least one verb from each column at the same time, driver threads a hazard *while* the gunner shoots open a shortcut wall *while* deciding whether to stop for the loot room the drone just found. See [Co-op Design Principles](../co-op-design.md).

!!! note "Input overlaps (intentional, context-sensitive)"
    Space = jump + handbrake · S = walk back + brake · E = interact + drone rotate · Ctrl = crouch + drone down · R = wall-drive + fire rocket (conflict, unresolved). Check existing bindings before adding new ones.
