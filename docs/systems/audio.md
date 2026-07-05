# Sound & Engine Audio

*Status (verified against code 2026-07-05): **engine audio system is BUILT and live** — recorded source set, RPM-band crossfade blender, virtual automatic gearbox with D/S/T drive modes, ignition, neutral revving, rev-limiter bounce, network sync. Interior muffling bus exists but is not yet hooked to seat/camera state. Other game sounds (turret, screech, explosions) predate this system and still use single one-shot players.*

## Goals

The car is the co-op living room — its engine is the soundtrack of every run. The sound should react to what the driver actually does (throttle, gears, revving, ignition) instead of a looped sample pitched by speed, and both players must hear the same engine state.

---

## Source recordings

Recorded from **AngeTheGreat's Engine Simulator CE v0.1.14a** (engine: base GM LS, ~6500 redline) through a Wave Link → ffmpeg capture chain. One session = 33 clips: idle ×2, on-throttle RPM holds 1500–6500, off-throttle holds 1500–6000, sweeps, blips, limiter, startup, shutdown.

- Raw takes + all tooling live in `OTR COWORK/OTR/Tools/EngineRecorder/` (guided recording script, loop processor, click analyzer, game-audio capture).
- Processing: automatic stable-window selection, cycle-aligned seamless loop cuts, crossfaded seams, de-clicking (the sim bakes crackle into quiet takes), peak normalization.
- Game assets: `res://Audio/Engine/` — 23 loops + 3 one-shots, 16-bit 48 kHz mono WAV, imported **PCM with forward loop** (⚠ QOA compression + loop points don't mix — caused periodic clicks).

## How the engine sound works

Two loop stacks (**on-throttle** / **off-throttle**, one loop per RPM band) play continuously; the blender (`engine_sound_blender.gd`, instanced in car.tscn) keeps only the two bands bracketing the current RPM audible, equal-power crossfaded and pitch-bent. Throttle crossfades between the stacks; a natural idle loop owns everything below 1500 RPM. All players route through the **Engine** audio bus (low-pass + reverb ready for interior muffling via `set_interior()`).

RPM itself is **virtual** (`car_audio_controller.gd`) — the car physics has no engine sim, on purpose:

- Virtual automatic gearbox: 5 gears including a tall overdrive; speed maps to RPM through the current gear.
- Shift points follow **aggression**, a slow-attack throttle envelope: keyboard W is binary, so *how long* you hold it stands in for *how far you press* a trigger. Nitro = instant max aggression.
- Kickdown, shift-down on decel, rev-limiter fuel-cut bounce at redline.

### Drive modes & controls

| Key | Action |
|-----|--------|
| **I** | Ignition on/off (car spawns OFF; startup/shutdown one-shots) |
| **G** | Neutral ⇄ Drive — in N, W free-revs with no drive power |
| **M** | Cycle drive mode **D → S → T** (shown as the HUD gear letter) |

- **D (comfort):** short-shifts ~2600, cruises ~3900 RPM at 110 km/h, needs a long W hold to get loud.
- **S (sport):** holds gears to ~3800+, eager kickdown.
- **T (track):** overdrive locked out, shifts at redline, any throttle = attack.

### Networking

Driver input → server-authoritative state → synced to all peers via tick fields `th` (throttle), `eng` (ignition), `ntr` (neutral), `dm` (drive mode). These fields dirty-flag the car in NetworkTickManager so a **parked** car still propagates ignition/revving. Ignition and mode RPCs validate the sender is the seated driver.

## Tuning & debugging

Everything is Inspector-tunable, no code:

- **Car → audio controller node:** gear ratios (`gear_top_speeds_kmh`), per-mode shift maps (*Drive Mode D/S/T* groups), aggression attack/release, limiter bounce feel (*Rev Limiter* group).
- **Car → EngineSoundBlender node:** stack/gain fade speeds, idle fade, pitch clamps, `limiter_rpm`.
- **`show_debug` on EngineSoundBlender:** live overlay — RPM, throttle, run state, every audible loop with gain and pitch. Works via Remote tree while the game runs.
- **`record_game.ps1`** (COWORK tools): captures game audio through the Wave Link chain and auto-runs the click detector — for pinpointing pops/chirps by timestamp.

## Open items

- [ ] Wire `set_interior()` to seat/camera state (bus effects exist, nothing calls it)
- [ ] Recording take 2 — redo `idle` (source crackle; current one is de-clicked but not perfect) and verify the top-band clips actually reached 6500
- [ ] Tune drive-mode shift maps by ear
- [ ] Delete legacy `EngineAudio` node + old sedan ogg from car.tscn (runtime-stopped, editor cleanup pending)
- [ ] Non-engine sounds (turret, screech, UI) still pre-date this system — bus routing / consistency pass someday
