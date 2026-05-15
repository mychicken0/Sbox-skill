# Shaders, Shader Graph, And Post-Processing

Prefer the workflow that gives the user a working asset with the least compiler risk.

## Choosing The Format

- For shader/post-process requests, first look for existing `.shdrgrph`, `.shader`, `.vmat`, material, and C# post-process files.
- Prefer editing or creating `.shdrgrph` when node-based work can express the effect. This is usually safer for tuning, attributes, noise, masks, color blends, and post-process composition.
- Use hand-written `.shader` only when the graph cannot express the required effect or the project already uses a stable custom shader pattern.
- Do not hand-edit generated compiled outputs such as `.shader_c`.

## Shader Graph Rules

- Preserve C# attribute names expected by `RenderAttributes` or material UI, such as `DirtStrength`, `TintColor`, `Intensity`, or project-specific names.
- Use graph parameter nodes marked as attributes when C# sets values dynamically.
- For post-process graphs, use `Domain: PostProcess`, `ScreenCoordinate`, `SceneColor`, and a `Result` albedo output.
- Common useful nodes: `ValueNoise`, `SimplexNoise`, `FuzzyNoise`, `SmoothStep`, `Step`, `Lerp`, `Length`, `TileAndOffset`, `Saturate`, `Float`, `Float2`, `Float4`, `SplitVector`, and `CombineVector`.
- After editing `.shdrgrph`, validate that it is valid JSON and all node input identifiers point to existing nodes.

## Post-Process Code

- Use `BasePostProcess<T>` or the local project's established post-process manager.
- Pass values through `Attributes.Set( "Name", value )` with names matching shader graph attributes.
- Load materials by stable resource path and early-return if invalid.
- Attach/enable post-process objects through public GameObject lifecycle patterns. If an effect needs toggling, prefer enabling/disabling the object or component rather than private engine calls.

## Visual Quality

- Avoid blocky screen-space masks unless the request explicitly wants pixel art.
- For visor/vignette/fog masks, prefer distance or ellipse/superellipse style masks over rectangular `max(abs(x), abs(y))` masks.
- For dirt, scratches, glass, dust, and scanlines, layer subtle noise at different scales instead of one harsh threshold.
- Keep strength attributes useful across a sensible range so designers can tune in the inspector.

## Validation Notes

- s&box Editor may be required to save/generate final shader outputs. Say this clearly.
- If CLI resource compilation fails without a useful shader error, do not claim the shader was fully verified.
- Include exact file paths and the attributes the user should check in the editor.
