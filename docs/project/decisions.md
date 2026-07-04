# Decision Log

Decisions that shape the game, newest first. When something gets decided in a design conversation, it gets a line here, with the *why*, so future-us doesn't relitigate it.

| Date | Decision | Why |
|---|---|---|
| 2026-07 | This wiki is the single source of truth for design; old plan .md files archived | Plan docs written before building never get updated after shipping, so they rot into lies (a feature audit found nitro/jump/wall-drive/flamethrower/rockets built while docs said "planned"). Rule: implementation status claims must be verified against code, never docs |
| 2026-07 | Stay in Godot, do not port to Unreal | Unreal has more raw power, but a 2-person team can't operate its complexity. Our scene (bounded static caverns + tunnels) is a Godot-friendly case: bake lighting instead of dynamic GI, fake scale with fog and light shafts. Porting = 6-12 month rewrite of working physics + netcode for no gameplay gain. See [Setting & Vertical Scale](../level-design/setting-and-scale.md) |
| 2026-07 | Setting: an underground industrial civilization, scale as the horror | Tunnels lead to facilities/factories built tight into rock, opening onto vast man-made voids. Tight/vast rhythm drives megalophobia; surface-clean to deep-monstrous doubles as the difficulty curve. See [Setting & Vertical Scale](../level-design/setting-and-scale.md) |
| 2026-07 | Design wiki lives at cap7n.github.io/otr-docs, seeded from existing plan docs | Shared overview for both devs; faster onboarding; records decisions |
| 2026-07 | Tunnels confirmed as the level setting | Confinement solves the blank-page problem; route = level in a driving game; plays to existing strengths (atmosphere stack, co-op seats). See [The Tunnels](../level-design/tunnels.md) |
| 2026-06 | Distributed authority for the drone | Pilot's machine simulates and broadcasts via NetworkTickManager, responsiveness for the operator |
| 2026-04 | Networking overhaul: single NetworkTickManager, StateBuffer + Hermite interpolation, no per-script sync RPCs | Bandwidth control, consistent interpolation, one sync path to debug |
| 2026-04 | Wall-driving via gravity shift, not sticky wheels | Jolt wheels only push along local down; redirecting gravity makes them work unmodified |
| - | Jolt physics instead of Godot default | Better vehicle behavior |
| - | Hand-placed enemy spawns, no procedural waves | Pacing is authored, like encounter design in a session |
| - | Hazards must be readable, driver-focused, non-lethal individually | No unfair surprise damage; danger comes from combinations |

*(Older decisions reconstructed from project docs, add corrections if the why is off.)*
