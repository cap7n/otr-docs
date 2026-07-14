# World & Story

*Session of 2026-07-14 (voice, on the road). This page exists to fix a specific problem: level design was stuck on "what do I show here?" - a question that's unanswerable without fiction. The world below is the answer key: every room, prop, and enemy should be readable as* what this place is for, and what interrupted it. *Decided items are marked; proposals follow the wiki's one rule and are labeled as such.*

---

## The Prospector *(decided)*

The megastructure is a **prospector**: it samples spaces of planets across time and space. Zones are samples - chunks of worlds cut out and brought inside. The extraction scar in the scrapyard (the road that dead-ends at the wall) is the signature of the cut, and every zone border should show one: sliced buildings, truncated pipes, a river ending in a wall. The cut edge is the cheapest storytelling asset we have.

**Why the crust and not the core:** a core is worthless to something that can cross spacetime. Molten iron is identical everywhere in the universe - infinitely abundant, zero information. The crust is the only layer where matter has been *arranged*: by weather, by life, by civilizations building things and throwing them away. The Prospector doesn't mine material, it mines **arrangement**. (*Arrangement* has a name and a substance: **Pratina** - see [Pratina](pratina.md).) A junkyard is a rich sample, not a trash one - matter arranged twice, once by manufacture, once by a culture deciding what to discard.

**Consequence for the economy:** what the structure values and what players sell are the same thing. Prices are the structure's own appraisals of arrangement. Loot value = information value = **Pratina density** ([Pratina](pratina.md)).

**Zone-writing tool:** every zone gets three stats that write its level design - *where it was cut from, how long it's been inside, what processing stage it's at.* Fresh sample: intact, native ecology panicking. Mid-process: sorted, tagged, machinery active. Late stage: crushed, mounded, half-absorbed into the structure.

## Inhabited, but unknowable *(decided)*

The structure has been lived in for a long time - the scrapyard shelter, the palisade, the garage all prove prior habitation. But it **cannot be understood**, because it samples across time: the shelter people may have fallen in centuries before our chunk was cut, and a newcomer can be from a *later* era than the veterans. Knowledge never accumulates - the zones shift, old maps rot, survivors from different centuries can't compare notes coherently. Established habitation, permanent frontier.

This is why nobody in the world gets to be a mentor, and why the droids can still be **first** - not first to exist here, but first at *methods*: first to hack a salvager, first to really drive the tunnels, first to work the structure instead of merely surviving it.

## The droids' arrival *(decided)*

The droids came in with a **different sampled chunk** - the scrapyard is where they landed, not where they're from. They were moving through a waste chute when it breached mid-transit:

- Wake inside the flow: gray screen, chromatic aberration, battery near zero, trash tumbling alongside, lights strobing past every ~10 m overhead.
- One light goes static - the pipe has broken. They fall (terrain covers half the drop; the fall is survivable *but not clean* - crash damage is the diegetic junker start: you begin near-dead, gray, broken).
- Behind them the garbage backs up and **clogs the pipe**; blinking red status lights mark the breach. The way home is sealed and visibly marked from day one.

**The clogged pipe is a promise:** "follow the pipe to where we came from" is a visible landmark and a later mission (personal / car cosmetics as the reward). The red lights also mean the Prospector *knows* that artery failed - a maintenance response that never quite arrives, or arrives in run three, is free tension.

**The car does not fall with them** *(decided)*. It's already parked in the garage - which means **someone owned it and isn't there anymore**. The garage had an owner. Every scratch on the car is backstory we don't have to write yet.

## The two characters *(decided)*

Personalities live in the **droids**, not the seats. Both characters can do everything; nothing about handling or guns changes. Character is expressed **only through speech** - barks reacting to what's happening:

- **The brains** (default co-pilot temperament): methodical, precise, nervous at speed. Gunning: "Target eliminated. Weak point confirmed." Driving fast: "oh - oh - we're going to crash-"
- **The speed demon**: reckless, gleeful. Driving: *yeehaw*. Gunning: "THERE goes the leg!"

Seat-swapping becomes content: the same corner produces terror or joy depending on who's holding the wheel.

**Barks double as the no-mic coordination layer** *(proposal)*: "target eliminated" tells the driver the rear threat is gone; "too fast, too fast" tells the gunner their aim is about to be ruined. Written with intent, barks absorb much of the callout/ping system's job - with personality on top. See [Co-op Design Principles](../co-op-design.md).

**Voice production** *(proposal)*: because they're droids, synthesized/vocoder voices are diegetically correct, not a compromise. Two synthesis profiles - one jittery and precise, one drawling and loose - instead of voice actors.

## The radio *(decided in direction)*

An unseen voice - other survivors, species unknown (human? alien? droid?) - gives missions and tries to help. They are **peers, not mentors**: they don't understand the structure either (see *Inhabited, but unknowable*). They know a little more about *staying alive*, nothing more about *what this place is*.

The standing player suspicion - never confirmed or denied - is whether the radio voice is connected to **the car's previous owner**. The dangling question is worth more than any answer.

**Guardrail:** the radio must not become the reason runs matter. If the loop's stakes reduce to "because the radio said so," the game is renting motivation instead of owning it. The radio is the diegetic *skin* over the objective system (its transmissions are what call `return_gate.unlock()`), not the source of the stakes.

**Production note:** garbled transmission with subtitles / text-burst radio keeps the species ambiguity *and* avoids voice-acting costs.

## The hub economy: the hacked salvager *(decided in direction)*

The Prospector trains its salvager robots with **micro-credits per sample - a reinforcement/learning signal, not money**. The droids captured one and retrofitted its credit interface into a marketplace ([Economy & Loot](../game/economy.md)):

- **Selling** = feeding loot into the captured salvager's intake; it dutifully credits you.
- **Buying** = placing orders through its **resupply channel**; the structure fulfills them because the salvager "needs" them.
- **The shopkeeper is the salvager itself** - bolted down in the garage, screens ticking in the structure's script, still politely trying to do its job. One asset, lots of character.

**Introduced as a mission, not given at start** *(decided)*: the shop doesn't exist on day one. **The brains invents it in-fiction** - watching salvagers deposit at an interface and receive something back, then proposing: *capture one and rig it to work for us.* Natural fit with the [harpoon/tether tool](../game/weapons-combat.md): capture means disabling without destroying - the archetypal two-seat combo gets its debut as a story beat.

**Consequence to carry in the fiction** *(proposal)*: a hacked reward system should be noticeable. Somewhere an audit can flag one salvager node's anomalous credit flow. Even unbuilt, the *risk* creates a standing co-op argument - sell aggressively vs. stay under the radar - exactly the friction the pillar demands. An exploit with zero risk is just a menu.

## Surveyor drones *(decided in direction)*

Ambient salvager/surveyor drones hover through zones sampling the ground - **red** (nothing) / **green** (find) - with screens of statistics in the structure's script. They are:

- ambient life for the world,
- a **loot telegraph**: they flag what the structure values, which is what players can sell - follow the green,
- a one-shot horror beat waiting to happen: a drone scans the *car* and goes green.

## The seeded language *(parked - after the game is fun)*

Goal: keep discovery personal; make it pointless to look the script up online. Design constraints agreed:

- Seed per **save/lobby** (host's world seed), *not* per player - co-drivers must read the same alphabet and share screenshots.
- **Meanings fixed and shallow** (numbers, warnings, sample grades - learned by association, Tunic-style); **glyph shapes seeded** per save. Generating meanings would only move the spoiler to the decode method.
- Scope: a font generator, not a conlang. A weekend, not a system.

---

## Open threads

- **The driver's signature beat:** the brains got the shop idea; the speed demon needs an equal moment where recklessness is the *right* answer - possibly the capture itself (the plan says tether carefully; the driver floors it and drags the thing home).
- **Who owned the car / built the garage?** Deliberately unanswered. Is the radio voice connected?
- **What does the radio actually want?** Not who they are - what pattern the droids might notice in their requests after ten runs.
- **The salvager audit:** does the structure ever respond to the hacked node, and how does that surface in play?
- **Radio addressing:** personalities are per-droid while seats are fluid - decide consciously who the radio talks to and how barks attribute when seats swap.
