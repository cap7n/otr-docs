# Setting & Vertical Scale

The world OTR takes place in, and how its spaces are used to create dread. This page is design intent, not lore for its own sake, it exists to keep the props, lighting, and level grammar consistent.

## The setting

**An underground industrial civilization.** Tunnels lead to facilities and factories built into the rock, sometimes tight and cramped, sometimes opening onto vast man-made voids. You are always underground. There is no sky.

The tone is industrial and dangerous, not pristine. Near the surface the tunnels are maintained, lit, and human-scaled. The deeper you go, the bigger, more abandoned, and less clearly-built-for-people the spaces become.

## Scale is the horror

The goal is **megalophobia**, the dread of enormous objects and spaces. Key design rules:

### 1. Dread lives in the transition, not the volume

A big room isn't scary on its own. It's scary when the body just came from a small one. **Compress before you release:** run the player through a genuine claustrophobic squeeze, then open onto the void. The smaller and longer the squeeze, the bigger the gut-drop. This makes the tight/vast room rhythm the horror engine, not just pacing.

### 2. Hide the far side

Megalophobia needs the space to exceed perception. If the player sees the opposite wall, it's a warehouse. If the far wall dissolves into fog with a few distant lights, the brain fills in "unknowably large." **Fog is the primary fear tool.** Make the space feel bigger than it is.

### 3. Give scale a human ruler

A void is abstract until something person-sized sits in it for comparison: a catwalk that reads as tiny against the far wall, a gantry crane the size of the whole car hanging 200m up, a staircase zigzagging up a rock face. The horror is the math the player does automatically.

### 4. Man-made vastness beats natural vastness

A natural cavern is awe. A cavern someone *carved* and filled with infrastructure implies dread about who did this and where they are. Lean industrial:

- Support structures bigger than they should need to be (the load-bearing implication is its own pressure)
- Suspended everything, pipes, chains, cables, walkways crossing overhead and vanishing upward
- Dead industry, silent factory blocks in the far wall, a few lit windows, most dark
- Scale-breaking machines, a drill head the size of the cavern mouth

## Scale as the difficulty curve

Surface-clean to deep-monstrous runs on the same axis as difficulty. Early tunnels: lit, tight, human. Deeper: bigger, darker, less human, more dangerous. Scale is the dread curve and the difficulty curve at once.

## How it's built (see also [The Tunnels](tunnels.md))

- Large caverns are **real static mesh, not skybox**, a skybox has no parallax and no light/fog response, and the drone would fly right up to it. See the reasoning in the build notes.
- Caverns are mostly static → **bake the lighting** (LightmapGI) instead of dynamic GI. Cheap at runtime, looks great, this is why Godot handles the scope (see [Decision Log](../project/decisions.md)).
- Read scale through **light, not geometry:** volumetric light shafts through fog, sparse points of light at height, a fog gradient that dissolves the ceiling. The shell mesh can be low-detail because it's always far and dark.
- New kit tiers this setting adds: **cavern shell** pieces, a **megastructure prop set** (crane, pillars, facility facade, catwalks, mostly silhouette + normal map), and a reusable **light-shaft prefab** (hole mesh + spotlight + fog volume).

## Open questions (see [Open Questions](../project/open-questions.md))

- Who built this and what happened to them? (mining colony dug too deep / wartime bunker-city / failed corporate arcology, each implies different signage, machines, and enemies)
- Is the vastness beautiful or hostile? (sublime-eerie vs. grim-industrial, sets the lighting palette)
