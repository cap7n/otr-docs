# Sound & Engine Audio

*Status (verified against code 2026-07-05): **engine audio system is BUILT and live** - recorded source set, RPM-band crossfade blender, virtual automatic gearbox with D/S/T drive modes, ignition, neutral revving, rev-limiter bounce, network sync. Interior muffling bus exists but is not yet hooked to seat/camera state. Other game sounds (turret, screech, explosions) predate this system and still use single one-shot players.*

## Goals

The car is the co-op living room - its engine is the soundtrack of every run. The sound should react to what the driver actually does (throttle, gears, revving, ignition) instead of a looped sample pitched by speed, and both players must hear the same engine state.

---

## Source recordings

Recorded from **AngeTheGreat's Engine Simulator CE v0.1.14a** (engine: base GM LS, ~6500 redline) through a Wave Link -> ffmpeg capture chain. One session = 33 clips: idle x2, on-throttle RPM holds 1500-6500, off-throttle holds 1500-6000, sweeps, blips, limiter, startup, shutdown.

- Raw takes + all tooling live in `OTR COWORK/OTR/Tools/EngineRecorder/` (guided recording script, loop processor, click analyzer, game-audio capture).
- Processing: automatic stable-window selection, cycle-aligned seamless loop cuts, crossfaded seams, de-clicking (the sim bakes crackle into quiet takes), peak normalization.
- Game assets: `res://Audio/Engine/` - 23 loops + 3 one-shots, 16-bit 48 kHz mono WAV, imported **PCM with forward loop** (⚠ QOA compression + loop points don't mix - caused periodic clicks).

## How the engine sound works

Two loop stacks (**on-throttle** / **off-throttle**, one loop per RPM band) play continuously; the blender (`engine_sound_blender.gd`, instanced in car.tscn) keeps only the two bands bracketing the current RPM audible, equal-power crossfaded and pitch-bent. Throttle crossfades between the stacks; a natural idle loop owns everything below 1500 RPM. All players route through the **Engine** audio bus (low-pass + reverb ready for interior muffling via `set_interior()`).

RPM itself is **virtual** (`car_audio_controller.gd`) - the car physics has no engine sim, on purpose:

- Virtual automatic gearbox: 5 gears including a tall overdrive; speed maps to RPM through the current gear.
- Each drive mode has a **fixed shift point** - the mode is the player's stated intent, the game never infers "how serious" a W press is (decided 2026-07-05: an earlier throttle-inference envelope felt weird on keyboard and was removed).
- Shift-down on decel, rev-limiter fuel-cut bounce at redline.

### Drive modes & controls

| Key | Action |
|-----|--------|
| **I** | Ignition on/off (car spawns OFF; startup/shutdown one-shots) |
| **G** | Neutral <-> Drive - in N, W free-revs with no drive power |
| **M** | Cycle drive mode **D -> S -> T** (shown as the HUD gear letter) |

Drive modes shape **real physics** (throttle response + top speed in car.gd), not just sound. Pick the tool for the situation:

| Mode | For | Shifts at | Throttle pedal | Top speed |
|------|-----|-----------|----------------|-----------|
| **D** | puzzles, climbing, precision | ~2800 | soft ramp-in (~0.7 s) | 70% |
| **S** | tight streets, quick + civil | ~4800 | quick | 90% |
| **T** | open stretch, flat out | ~6400, no overdrive | instant | 100% |

### Networking

Driver input -> server-authoritative state -> synced to all peers via tick fields `th` (throttle), `eng` (ignition), `ntr` (neutral), `dm` (drive mode). These fields dirty-flag the car in NetworkTickManager so a **parked** car still propagates ignition/revving. Ignition and mode RPCs validate the sender is the seated driver.

## Tuning & debugging

Everything is Inspector-tunable, no code:

- **Car (car.gd):** per-mode throttle response + speed scale (*Drive Modes* group).
- **Car -> audio controller node:** gear ratios (`gear_top_speeds_kmh`), per-mode shift points (*Drive Mode Shift Points* group), limiter bounce feel (*Rev Limiter* group).
- **Car -> EngineSoundBlender node:** stack/gain fade speeds, idle fade, pitch clamps, `limiter_rpm`.
- **`show_debug` on EngineSoundBlender:** live overlay - RPM, throttle, run state, every audible loop with gain and pitch. Works via Remote tree while the game runs.
- **`record_game.ps1`** (COWORK tools): captures game audio through the Wave Link chain and auto-runs the click detector - for pinpointing pops/chirps by timestamp.

## Open items

- [ ] Downshift transitions sound rough (noted 2026-07-05, parked for now - likely needs per-shift RPM drop shaping or crossfade tuning)
- [ ] Wire `set_interior()` to seat/camera state (bus effects exist, nothing calls it)
- [ ] Recording take 2 - redo `idle` (source crackle; current one is de-clicked but not perfect) and verify the top-band clips actually reached 6500
- [ ] Tune drive-mode shift maps by ear
- [ ] Delete legacy `EngineAudio` node + old sedan ogg from car.tscn (runtime-stopped, editor cleanup pending)
- [ ] Non-engine sounds (turret, screech, UI) still pre-date this system - bus routing / consistency pass someday
