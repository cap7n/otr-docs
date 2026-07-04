# Shortcut Paths

*Status: planned. Source: `shortcut_paths_plan.md`.*

## What

Hidden side tunnels branching off the main path — behind destructible walls, speed-gated, or dead-ending in treasure rooms. Shortcuts reward exploration and co-op awareness: the driver watches the road while the gunner scans the walls.

## Why

Without shortcuts, the tunnel is a linear corridor and every run feels the same. Shortcuts give players a reason to look around, create risk/reward decisions, reward the non-driving player for paying attention, and add replayability through discovery.

---

## Shortcut types

### 1. Destructible Wall Shortcut

A side tunnel hidden behind a cracked wall. The gunner (or a bomb) shoots it open. **Co-op discovery moment:** gunner spots the cracks, opens it, calls it out; driver commits.

Unlike barricades (which block the *main* path and must be dealt with), these are *optional* and easy to miss. Lower HP — a quick turret burst opens them.

**Cues:** light seeping through cracks, trickling dust, subtly different texture, wind whistling.

### 2. Timed Shortcut (Speed Gate)

A side path whose gate is open for a limited time — a trigger zone ahead starts the timer. Fast enough (nitro helps) and you make it. Rewards maintained speed and split-second commitment.

**Cues:** wall lights flash a "this way" sequence, gate color (green open / red closing), loud mechanical close.

### 3. Hidden Room (Dead End with Loot)

A small chamber off the main tunnel with a chest — the car doesn't fit; someone walks in **on foot**. Camouflaged entrance (waterfall, dark alcove, hanging debris), warm golden glow inside. Creates a "stop the car?" decision while enemies could be catching up. Prime drone-scouting content.

### 4. Risk/Reward Fork

An open fork: main path = enemy encounter, side path = hazard gauntlet. Both reconnect after the same distance. Lets the team pick their challenge type — the hazard path plays to the driver's strengths. Loot chests reward the harder driving route.

**No new systems needed** — it's a level-design pattern using existing spawns and hazards.

---

## Discovery & co-op interaction

- **Gunner:** wider, elevated field of view — naturally scans walls while tracking enemies. Pings discovered shortcuts for the driver.
- **Drone:** flies into spaces the car can't reach, scouts ahead, shows the passenger hidden entrances.
- **Driver:** makes the call — take it or stay on the main path. Timed gates demand instant reaction; wall shortcuts allow discussion while the gunner shoots.

## Placement philosophy

- **Skip shortcuts** branch off *before* an encounter and reconnect *after* — skipping it means less currency but more safety.
- **Loot shortcuts** branch off breather sections and dead-end with treasure.
- **Risk/reward forks** replace an encounter with a choice: fight or hazard run.
- Untriggered spawn zones never spawn — shortcuts genuinely skip content, no wasted resources.

## Build order

1. Destructible wall shortcut (reuse barricade system + cues)
2. Interactable chest (opens on E, loot table, server-authoritative)
3. Loot room
4. Timed shortcut gate
5. Risk/reward fork (level design only, no new code)
6. Discovery cue polish
7. Drone scouting (works via existing camera)
