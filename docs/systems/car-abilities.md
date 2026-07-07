# Car Abilities, Nitro, Jump & Wall-Drive

*Status (verified against code 2026-07-04): **nitro and jump are BUILT and live**, charges, cooldowns, VFX, inputs all wired. **Wall-drive is fully coded but switched off**: its `setup()` call is commented out in car.gd:334, re-enabling and testing is a [backlog quick win](../project/backlog.md). Also built but never documented here: flamethrower, 4-tube rocket pot, rocket thrust, and drift (also switched off, car.gd:329). This page stays as the design reference.*

## Goals

Give the driver active abilities beyond steering and throttle. These make the driver role more engaging and open up level design possibilities (jumps over gaps, wall-driving sections, speed gates).

Can be unlocked via CAR_MOD items from the shop or available from the start, decide later.

---

## 1. Nitro Boost

**What:** Press a key for a short burst of extra speed. Forward force on top of normal engine power for ~1.5 seconds.

**Why:** An active "go faster" button for dodging, ramming through barricades, clearing gaps, or escaping swarms. Creates "hit nitro and punch through" moments. Enables speed-gated shortcuts.

**Behavior:**

- Charge system: start with 3 charges, each boost costs 1. Slow regen (or refill from pickups).
- Minimum speed required (no boosting from standstill).
- Cooldown between boosts.
- Feedback: FOV increase, speed lines, exhaust flame VFX, boost sound.

**Input:** Left Shift.

---

## 2. Jump

**What:** The car launches upward with an impulse. Works when at least 2 wheels are grounded.

**Why:** Gaps to jump, obstacles to clear, enemies to jump past. Combined with nitro: "boost + jump" moments. Existing suspension handles the landing naturally.

**Behavior:**

- Upward impulse + slight forward bias scaled by current speed.
- Grounded-only (wheel contact check).
- Single charge with cooldown, upgradeable to multiple.
- VFX: dust burst under wheels; landing triggers camera shake.

**Input:** ✅ Resolved — shipped on **Q**. The tap-Space-jump / hold-Space-handbrake idea was dropped in favour of a dedicated key.

---

## 3. Wall Driving (Gravity Shift)

**What:** The car temporarily drives on walls and ceilings. Gravity is redirected to point into whatever surface the car is on.

**Why:** *The coolest level design tool of the three.* Tunnel sections where the road curves up the wall onto the ceiling. Unique visual moments; makes the tunnel feel dynamic. Also a co-op moment, the first time it happens, both players react.

**Why gravity shift (not sticky wheels):** Jolt vehicle wheels only generate force along the body's local down axis. Redirecting gravity so "down" points into the wall makes the wheels work naturally, no custom wheel physics. Fallback if Jolt lacks per-body gravity direction: disable gravity on the car and apply a manual force toward the surface each frame.

**Behavior:**

- Activated by driving onto marked wall-drive zones (triggers in the tunnel), not a button press.
- Surface-tracking rays detect the surface normal; gravity direction rotates smoothly to match.
- Zone-based duration (active while in the zone) or fuel meter.
- Leaving the surface: gravity transitions back to world-down; car launches off with current velocity.
- Camera follows the reorientation, needs smooth up-vector interpolation.

**Risks:**

- Jolt per-body gravity support needs testing.
- Wheel behavior under redirected gravity needs hands-on verification.
- Camera sickness from rapid orientation changes, transition speed needs tuning.
- Wall surfaces must be smooth and wide enough for the car.

---

## Build order

1. Nitro, simplest. Forward force, charge drain, cooldown. VFX after core feel is right.
2. Jump, upward impulse, ground check. Test landings on existing suspension.
3. Nitro + jump VFX/audio.
4. Wall-drive prototype, test gravity redirection on a simple ramp. Verify Jolt compatibility.
5. Wall-drive zones, triggers in the tunnel with ramp geometry.
6. Wall-drive camera, smooth reorientation without motion sickness.
7. Wall-drive VFX, gravity distortion, surface glow.
8. Shop integration, CAR_MOD items that unlock jump and wall-drive.
