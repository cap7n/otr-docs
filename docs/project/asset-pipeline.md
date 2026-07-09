# Asset Pipeline (Blender -> Godot)

How OTR assets get their look, established 2026-07-06 with the first two shipped assets (the outfall pipe and the zone-shell concrete). **No photo textures** - everything is authored as procedural node graphs in Blender and baked to texture maps. One visual language, no pasted-photo uncanny mismatch, and baked textures get mipmaps (see the giant-surface rule below).

## The loop

1. **Model** in Blender. Separate parts by material. Quick Smart UV Project per material (islands of *different* materials may overlap - each material bakes to its own texture; islands *within* one material may not).
2. **Procedural materials** are scripted as Blender node graphs (`bpy`); all look values live in one `TUNE` dict per script, so a note like "less rust, longer drips" is a two-number change.
3. **Lookdev**: open the asset's blend, `Z -> Rendered`, judge, tune, repeat until it reads right.
4. **Bake** to PBR maps (albedo / roughness / normal, metallic when it varies). Per-object for hero props, seamless tiles for big surfaces.
5. **Godot**: textures land in `textures/<Asset>/`, materials as `.tres`. For `.blend` props, materials are remapped **by material name** in the `.blend.import` - never by node-path overrides in scenes (those broke twice; names survive re-imports).

The authoring workspace (scripts, lookdev blends, baked masters, preview renders) lives outside the game repo in `Desktop/OTR Assets`, with its own notes file holding the technical detail.

## The giant-surface rule (why the 2 km artifact happened)

Per-pixel procedural shader math **cannot be mip-filtered** - at distance, sub-pixel detail aliases into shimmering lines (the 2 km wall artifact, killed 2026-07-06). Baked textures filter for free. So for huge surfaces:

- **High-frequency detail** (grain, seams, streaks, squares) -> **baked** into a seamless tile.
- **Low-frequency / per-instance variation** (per-panel tint + mirror-flip, ~200 m macro patches, floor-line grime) -> stays in a **slim shader**, because a repeating tile physically can't vary per panel.

`mega_concrete_v2.gdshader` is the reference implementation: baked tile + panel hash + macro fbm + grime + close-up detail bump, with live sliders for sheen, relief, panel variety.

## Texture-resolution intuition

A 2048 tile over a 25 m panel ~ 80 px/m - good at driving distance. Close-up "pixelation" is magnification (mipmaps don't help); the detail-bump layer in the shader covers it. Baking a whole 2 km wall in one texture would need a ~160,000 px image - that's why tiles + shader variation, not mega-bakes.
