# World & Structure

The world of OTR, decided 2026-07-04. This page supersedes the earlier "underground civilization" framing; [Setting & Vertical Scale](setting-and-scale.md) still holds the how-it-feels rules (megalophobia, light-based scale reading), this page holds what the world *is*.

## The opening

Two droids wake up with dying batteries in a garbage dump. The screen is gray and desaturated; they stumble, barely functional, toward the only light source: a car inside an abandoned garage (a 1990s American roadside gas station). They climb in, plug into the seats, and the moment they dock, **the screen floods with vivid color**.

That moment is the whole game in miniature: the car is not a vehicle, it is **power, life, and color**. The palette is diegetic, tied to being plugged in.

## The players

Two droids. This is why the game is 2-player co-op, period ([decision](../project/decisions.md)): the droids are a pair, the car has two seats, and every system assumes both.

**The battery leash:** outside the car, a droid runs on residual charge for roughly 30 to 60 seconds. Then the battery starts failing, the screen grays out, and you drag yourself back to the car in the same dying stumble as the opening. Every on-foot excursion (loot rooms, switches, gates) is a timed sortie, and "you go, I'll keep the engine warm" is a real negotiation.

**The drone** is not battery-limited but **signal-limited**: it can fly only within signal strength of the car. Range, not time.

## The structure

The world is a **megastructure**: a lattice of zones, each roughly **2 km across**, separated by monolithic walls that rise into the sky. The sky itself is a slab of concrete or metal. There is no outside in view, no horizon, no sun. Scale is the horror ([Setting & Vertical Scale](setting-and-scale.md)).

- **Zones are fully authored**, not tile-assembled. Each is hand-built and distinct; authored spaces have character.
- **Zone themes are anachronistic, even time is not certain.** The garage sits in a 1990s American gas station. The next zone over might be a cyberpunk factory complex, or an abandoned 21st-century city. The dissonance is the world's texture, any art direction has a home, and car upgrades can span eras (junkyard parts to futuristic tech).
- **Between the zones**, inside and beneath the walls, run tunnels, caves, and megafacility interiors: the connective tissue. This is where the tunnel room-grammar work lives (squeezes, caverns, junctions, wall-drive sections).

**The shell and the cut-out (2026-07-05).** Every zone is the same reusable **shell**: a bare 2 km concrete cube (built once, `hub_v2.tscn` is the first). A zone's content is a **cut-out**: when the structure captures a 2×2 km slice of somewhere, it takes ~1 km of ground with it, so the terrain surface sits roughly **mid-cube**, ceiling 1 km above the surface, shell continuing 1 km below it. Consequences: every room has an underworld beneath its terrain slab (collapses, basements, drainage go there), and the shell's wall shader takes a per-room `ground_y` so grime and weathering anchor to wherever that room's ground line is.

## The shift

The lattice **shifts every so often, never in real time under the player**. An exit that was open last visit may be sealed now; the zone behind a wall may be a different zone than before. In fiction the structure rearranges itself; in the engine, the shift is simply which level loads behind which gate, plus which exits are flagged open, near-zero tech for near-infinite variety.

**Exits are read diegetically**: lights on the walls or similar in-world signals tell you what is open this cycle. No menu, no minimap. Some exits may need to be *opened* rather than found (the locked-gate weak-point and objective-unlock machinery already exists in code).

## The loop

The garage is **home**: the return point, the shop, the save anchor (saving model still [undecided](../project/open-questions.md)). A run leaves the garage into a neighboring zone, explores it by car, and exits through one of its sides.

**Expeditions chain zones.** You can push through a zone's far side into the next zone instead of returning, going deeper on one outing. The way home may have shifted while you were out. The deeper you push, the more you are carrying and the less certain the return, so "push on or head back?" is the standing argument between the two seats.

## The enemies

The structure is inhabited by hostile machines (the current roster: orbs, fliers, ranged, turrets, artillery). Direction going forward: fewer interchangeable mobs, more **one-of-a-kind and bigger enemies that require a *way* to kill them**, a method, a weakness, a sequence, not just shooting until a health bar empties. The existing weak-point system (locked gate) is the seed of this.

## Death

Dying is permanent in fiction. In practice it is handled by the saving model, which is **still under discussion** (save/load vs. a more roguelite structure), see [Open Questions](../project/open-questions.md).

## What this replaces / retires

- The "underground civilization" setting framing (this page is the sharper version; the megalophobia and light-reading rules on [Setting & Vertical Scale](setting-and-scale.md) all still apply).
- The "who built it and what happened" open question: with anachronistic zones, the origin is **deliberately uncertain**. The mystery is a feature, not a gap to fill.
- The tunnels-vs-terrain ambiguity: zones are open authored spaces, tunnels are the between-zone tissue. Both exist, each with its role.
