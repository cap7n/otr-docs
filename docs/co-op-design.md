# Co-op Design Principles

The pillar the whole game rests on. OTR is 2-player co-op, period ([decision](project/decisions.md)) - this page is the *why*, and the rules every beat, enemy, and system gets designed against. Before you add anything, test it here first.

## The pillar

**OTR works when both players feel they contributed to one shared task.**

Not "I did my job and you did yours" - *we* did that, together. The size of the contribution doesn't matter: a well-timed handbrake counts as much as the killing shot. What matters is that the outcome was **single and shared**, and neither player can point at it and say "that was all me." Every rule below exists to protect that feeling.

## Hard asymmetry, coupled actions

Inside the car the seats are **hard-separated**: you cannot drive and gun at the same time. Role fluidity means you *switch* seats, not multitask them ([player verbs](game/player-verbs.md)). One player is never doing two jobs at once.

But the seats are not two solo games sharing a screen. **Each player's actions reshape what the other can and should do.** The driver's line decides the gunner's shot; the gunner's shot decides whether the driver's line was safe. Neither is a passenger to the other - they are two inputs into one result.

That coupling is the real design target, deeper than "keep both players busy." Two players who are each busy but *independent* are playing solo next to each other. Two players whose actions bend each other's decisions are playing OTR.

**Made concrete in combat:** the driver deals no direct damage - every gun belongs to the co-pilot ([combat split](project/decisions.md), [Weapons & Combat](game/weapons-combat.md)). A driver with an empty co-pilot seat can move and ram but cannot *kill*: exposed, half-blind, reacting to threats they can't answer. When that seat is empty the driver should feel **panic, almost disorientation** - and that's not a punishment bolted on, it's the plainest proof that the co-pilot was never just a passenger.

## The moment we're building toward

> The co-pilot fires a harpoon and latches an enemy. The driver reads the line, throws the car into a sharp corner, and slings the thing into a wall - or into the enemy behind it.

Neither player did that. It's **one action made of two**, and it only exists because the harpoon changed what the corner *meant*. That's the north star: not "you shoot while I drive," but combos where the two seats **multiply**.

!!! note "Status"
    The harpoon/tether is a **proposed** mechanic, not built - it's on the [backlog](project/backlog.md) as the archetype of a two-seat combo tool. It lives here because it defines the *shape* of the co-op we want, whatever specific verbs end up delivering it.

## Friction is a feature

Co-op in OTR is allowed to be an argument. **Design the forks that make players disagree; don't smooth them away.**

- *Push on to the next zone, or turn back while we still can?* - the standing argument, powered by fuel and the shifting way home ([World & Structure](level-design/world-structure.md)).
- *Stop the car for that loot room while enemies close in?*
- *Who goes on foot?* - one droid leaves the car and the [battery leash](level-design/world-structure.md) starts ticking; "you go, I'll keep the engine warm" is a real negotiation.
- *Limited cargo:* if the box is small, "what do we keep" is a fight worth having ([open question](project/open-questions.md)).

A run with no moment where the two players want different things is a run that could have been single-player.

## Coordination without a mic

We don't assume players are on voice chat (whether the game ships any in-engine comms is an [open question](project/open-questions.md)). So the coupling has to **read through the actions and the world itself**, not through talking:

- The harpoon line *is* the callout - the driver sees where it's anchored and instantly knows what the corner is for.
- The gunner's tracers, the drone's scouting, the exit lights on the walls, a hazard's tell - the game speaks diegetically, so a silent duo can still coordinate.
- If a beat only works when players describe it out loud, it's leaning on a crutch the game might not provide.

## Role fluidity is itself a choice

Players switch seats at will ([verbs](game/player-verbs.md)) - but because the seats are hard-asymmetric, *who sits where* is a live co-op decision. Who drives this stretch, who takes the gun for the boss, who's the one who steps out on foot. The game should keep making that choice matter, not let the team settle into fixed roles and forget the other seat exists.

## No single-player content

The [decided rule](project/decisions.md): no solo mode, and no beat one player can run alone. A beat that uses only **driver** verbs is single-player content wearing a co-op car ([player verbs](game/player-verbs.md)). The [enemy roster](game/enemies.md) already follows this - each type asks a different question of the two seats - and every new encounter, hazard, and secret should too.

## The two-seat test

Run every beat - every encounter, hazard, shortcut, set-piece - through this:

1. **Busy:** is each seat doing something? (If either is "nothing," the beat is broken.)
2. **Coupled:** does each player's action change the *other's* decision? (This is the real bar - busy-but-independent isn't enough.)
3. **Inseparable:** could one player pull this off alone? (If yes, it isn't co-op yet.)
4. **A fork worth arguing about:** is there a choice the two might disagree on? (Friction is content.)
5. **Readable without a mic:** does the coordination come through actions and world-tells, not required chatter?

!!! tip "The one-line version"
    Not *"what is the driver doing, and what is the co-driver doing?"* - the sharper question is **"how does what one player just did change what the other should do next?"** If the answer is "it doesn't," you've designed two solo games side by side.
