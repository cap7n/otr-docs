# Open Questions

Things not yet decided. When one gets answered, move it to the [Decision Log](decisions.md) with its *why*.

## Blocking level design

### 1. Saving & stakes model ⭐ *the big one, actively in discussion*

The [world structure](../level-design/world-structure.md) answered the run's *shape* (expeditions through shifting zones, exits as finish lines, battery as pressure). What's left is what death and saving mean, and that defines every stake in the game:

- **Save/load:** dying reloads the last save; everything since is gone. Simple, but "going back in time" sits oddly with a world that shifts forward.
- **Roguelite-ish:** no rewinding, death has forward-moving consequences (lose the cargo, lose the zone, wake somewhere else, something is different). Fits the fiction better; needs more design.

Sub-questions that hang on this: when does saving happen (garage-only? rare in-world docks?), what exactly is lost on death, and when loot becomes "banked". **The junker proposal below survives either answer.**

### 2. The junker start (proposal, survives any saving model)

Start with a weak car; abilities and power are bought as CAR_MOD items. Rule: underpowered must never mean unresponsive, weak stats with good feel.

**Implementation readiness (checked 2026-07):** the ability architecture is already modular; ~a day of work: (1) `unlocked` flag + early-return per controller, peer-synced; (2) actual CAR_MOD items (category exists as enum only); (3) a save file (nothing persists to disk yet, needed regardless of the saving model chosen).

**Onboarding refinement (2026-07-07, on the table, not decided):** instead of opening on a weak car, open on a *good* one and then break it — the intro car's engine fails and the crew installs a junker engine — so the player's first taste is good driving, not a bad one. Car-tuning presets may be saved per engine so a swap isn't a full re-tune. Direction only.

## Design

- **Long-term direction:** expeditions go out and come home, but where does it all *go*? Escape the structure? Reach an edge? Ever-deeper mastery with no promised outside? Undefined for now, and fine to leave until the core loop grips.
- **Is the vastness beautiful or hostile?** The gray-to-color intro suggests the answer trends vivid-when-powered; the palette question is now really "how vivid, and does it vary per zone theme?"
- **Is cargo space limited?** If yes, "what do we keep" becomes a co-op negotiation.
- **Where does fuel come from?** Range = fuel is decided ([World & Structure](../level-design/world-structure.md)), but the [economy](../game/economy.md) never sources it: do you buy fuel, scavenge it, or is it just a run timer? And does running dry strand you mid-zone or end the run? ([The Car](../game/the-car.md) flags this too.)
- **Car damage & repair model:** the car has HP, takes damage, and is repaired in the hub, and the wear shader is built to show it — but the actual numbers (how much HP, how repair is priced, what a beaten car costs) aren't specified anywhere, and they're tangled with what death costs.
- **In-game comms vs. coordination-by-action:** we don't assume voice chat, so co-op is meant to read through coupled actions and diegetic tells ([Co-op Design Principles](../co-op-design.md)). Open: does the game still ship explicit tools (the [callout/ping system](backlog.md), a shared marker) as a safety net, or lean fully on action + world-reading?
- **Driver's built damage tools vs. the no-damage rule:** the flamethrower (50 DPS) and 4-tube rocket pot are built on the *driver*, but the [combat split](decisions.md) puts all damage on the co-pilot. Reconcile: move them to the co-pilot, reframe the flamethrower as a non-damage push / area-denial tool, or cut them ([Weapons & Combat](../game/weapons-combat.md)).
- **Rebar/harpoon launcher — firing mechanism:** crossbow, gunpowder, air-pressure off the car, or railgun. Undecided; it drives the sound, the reload feel, and the fiction ([Weapons & Combat](../game/weapons-combat.md)).
- **`R` key conflict:** wall-drive toggle vs. rocket pot fire, both on R, one has to move before wall-drive is re-enabled. *(Jump input resolved: it shipped on Q.)*

## Technical (needs testing, not discussion)

- Jolt per-body gravity direction support (wall-drive prerequisite)
- Square shadows in the tunnel, mesh normals fix, else shadow atlas size / light softness

## Retired

- ~~Who built the world and what happened to them?~~ Deliberately uncertain by design: zones are anachronistic, the mystery is a feature ([decision](decisions.md), 2026-07-04).
- ~~What ends a run?~~ Answered by the world structure: exit through a zone side, chain or return. The *stakes* half lives on as question 1.
- ~~Jump input~~ (shipped on Q) and ~~art abilities unlocked vs bought~~ (folded into the junker proposal).
