# Decision Log

Decisions that shape the game, newest first. When something gets decided in a design conversation, it gets a line here, with the *why*, so future-us doesn't relitigate it.

| Date | Decision | Why |
|---|---|---|
| 2026-07-04 | World: a megastructure lattice of ~2 km walled zones under a concrete sky; players are two droids powered by the car; garage = home; the lattice shifts between visits; expeditions can chain zones | One fiction that explains the co-op pair, the seats, run variety, and authored chunks. Shifting = which level loads behind which gate, near-zero tech. See [World & Structure](../level-design/world-structure.md) |
| 2026-07-04 | Zones are fully authored (no tile assembly) and anachronistic in theme, even time is uncertain | Authored spaces have character; era-mixing means any art idea has a home, upgrades can span junkyard-to-futuristic, and the world's origin stays deliberately mysterious (retires the "who built it" question) |
| 2026-07-04 | Battery leash: droids survive ~30-60s outside the car before gray-screen failure; the drone is limited by signal range, not battery | Makes the car life itself (mirrors the intro), turns every on-foot excursion into a timed sortie and a two-player negotiation |
| 2026-07-04 | Enemy direction: fewer interchangeable mobs, more one-of-a-kind bigger enemies that need a *method* to kill, not just bullets | Landmark encounters fit authored zones; the weak-point machinery (locked gate) is the seed |
| 2026-07 | OTR is 2-player co-op, period. No solo mode, no features that let one player run everything | Every system is designed around two seats mattering; a solo fallback would quietly erode that. Removed the "Lone Wolf" modifier from the plans |
| 2026-07 | This wiki is the single source of truth for design; old plan .md files archived | Plan docs written before building never get updated after shipping, so they rot into lies (a feature audit found nitro/jump/wall-drive/flamethrower/rockets built while docs said "planned"). Rule: implementation status claims must be verified against code, never docs |
| 2026-07 | Stay in Godot, do not port to Unreal | Unreal has more raw power, but a 2-person team can't operate its complexity. Our scene (bounded static caverns + tunnels) is a Godot-friendly case: bake lighting instead of dynamic GI, fake scale with fog and light shafts. Porting = 6-12 month rewrite of working physics + netcode for no gameplay gain. See [Setting & Vertical Scale](../level-design/setting-and-scale.md) |
| 2026-07 | ~~Setting: an underground industrial civilization~~ superseded 2026-07-04 by the megastructure decision above | The scale-as-horror rules survive unchanged on [Setting & Vertical Scale](../level-design/setting-and-scale.md); only the framing (underground rock) was replaced (walled zones + concrete sky) |
| 2026-07 | Design wiki lives at cap7n.github.io/otr-docs, seeded from existing plan docs | Shared overview for both devs; faster onboarding; records decisions |
| 2026-07 | Tunnels confirmed as the level setting | Confinement solves the blank-page problem; route = level in a driving game; plays to existing strengths (atmosphere stack, co-op seats). See [The Tunnels](../level-design/tunnels.md) |
| 2026-06 | Distributed authority for the drone | Pilot's machine simulates and broadcasts via NetworkTickManager, responsiveness for the operator |
| 2026-04 | Networking overhaul: single NetworkTickManager, StateBuffer + Hermite interpolation, no per-script sync RPCs | Bandwidth control, consistent interpolation, one sync path to debug |
| 2026-04 | Wall-driving via gravity shift, not sticky wheels | Jolt wheels only push along local down; redirecting gravity makes them work unmodified |
| - | Jolt physics instead of Godot default | Better vehicle behavior |
| - | Hand-placed enemy spawns, no procedural waves | Pacing is authored, like encounter design in a session |
| - | Hazards must be readable, driver-focused, non-lethal individually | No unfair surprise damage; danger comes from combinations |

*(Older decisions reconstructed from project docs, add corrections if the why is off.)*
