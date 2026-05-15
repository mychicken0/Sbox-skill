# Shader Graph Snippets

Use this when editing `.shdrgrph` JSON by hand. Prefer the editor when available, but careful JSON edits are useful for agent work.

## Basic Post-Process Graph Shape

```json
{
  "IsSubgraph": false,
  "Path": "shaders/my_effect.shdrgrph",
  "BlendMode": "Opaque",
  "ShadingModel": "Lit",
  "Domain": "PostProcess",
  "Version": 1,
  "nodes": [
    {
      "_class": "Result",
      "Identifier": "0",
      "Position": "600,0",
      "Albedo": { "Identifier": "2", "Output": "Result" }
    }
  ]
}
```

## Attribute Float

```json
{
  "_class": "Float",
  "Min": 0,
  "Max": 1,
  "Value": 0.16,
  "Name": "DirtStrength",
  "IsAttribute": true,
  "UI": {
    "Type": "Slider",
    "Step": 0.01,
    "Priority": 0,
    "PrimaryGroup": { "Name": "Wear", "Priority": 0 },
    "SecondaryGroup": { "Name": null, "Priority": 0 }
  },
  "Identifier": "7",
  "Position": "0,0",
  "HandleOffsets": {}
}
```

## Attribute Color

```json
{
  "_class": "Float4",
  "Value": "0.1,0.16,0.18,1",
  "Name": "TintColor",
  "IsAttribute": true,
  "UI": { "Type": "Color", "Step": 0, "Priority": 0,
    "PrimaryGroup": { "Name": "Visor", "Priority": 0 },
    "SecondaryGroup": { "Name": null, "Priority": 0 } },
  "Identifier": "3",
  "Position": "0,0",
  "HandleOffsets": {}
}
```

## Useful Node Names And Outputs

- `ScreenCoordinate` -> `Result`
- `SceneColor` -> `Result`, optional `Coords`
- `ValueNoise`, `SimplexNoise`, `FuzzyNoise` -> `Result`, input `Coords`
- `SmoothStep` -> `Result`, inputs `Input`, `Edge1`, `Edge2`
- `Step` -> `Result`, inputs `Input`, `Edge`
- `Lerp` -> `Result`, inputs `A`, `B`, `C`
- `Multiply`, `Add`, `Subtract`, `Divide` -> `Result`, inputs `A`, `B`
- `Length`, `Abs`, `Saturate`, `Frac`, `Floor` -> `Result`, input `Input`
- `SplitVector` -> `X`, `Y`, `Z`, `W`
- `CombineVector` -> `XY`, `XYZ`, `XYZW`
- `TileAndOffset` -> `Result`, inputs `Coords`, `Tile`, `Offset`

## Validation Scriptlet

PowerShell link check:

```powershell
$json = Get-Content -Raw .\Assets\Shaders\effect.shdrgrph | ConvertFrom-Json
$ids = @{}
foreach ($node in $json.nodes) { $ids[$node.Identifier] = $node._class }
$missing = @()
foreach ($node in $json.nodes) {
  foreach ($prop in $node.PSObject.Properties) {
    $v = $prop.Value
    if ($null -ne $v -and $v.PSObject.Properties['Identifier'] -and $v.PSObject.Properties['Output']) {
      if (-not $ids.ContainsKey([string]$v.Identifier)) { $missing += "$($node.Identifier).$($prop.Name)->$($v.Identifier)" }
    }
  }
}
if ($missing.Count) { $missing } else { "node links ok: $($json.nodes.Count) nodes" }
```

## Common Visual Recipes

- Vignette/visor: centered screen UV -> scale with `Float2` -> `Length` -> `SmoothStep`.
- Dirt: mix high-scale `ValueNoise`, low-scale `SimplexNoise`, and sparse `FuzzyNoise` through `Step`.
- Scanlines: split screen Y -> multiply by line count -> `Frac` -> `Step` -> multiply by strength.
