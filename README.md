# Kruty1918 Sprite Grounding

Reusable runtime API for alpha-carded sprites and quad-card meshes:

## Install (Unity Package Manager)

Package Manager → **+** → **Add package from git URL**:

```
https://github.com/kruty1918dev-ai/com.kruty1918.sprite-grounding.git
```

or in `Packages/manifest.json`:

```json
"com.kruty1918.sprite-grounding": "https://github.com/kruty1918dev-ai/com.kruty1918.sprite-grounding.git#v0.1.0"
```

The repository is private — Git credentials (PAT / Git Credential Manager)
are required on every machine that resolves the package.

## Features

- **Visible bounds** — `AlphaBoundsAnalyzer` scans alpha and returns the
  opaque pixel/UV rect (alpha-clip threshold semantics).
- **Support point** — `SupportPointResolver` locates the ground-contact
  point (bottom-centre or lowest-band centroid) in UV space.
- **Card projection** — `QuadCardProjector` maps UV-space results onto
  quad-card meshes (cross/clump cards) via bilinear UV→local mapping.
- **Trimmed representation** — `TrimmedSpriteFactory` (sprite rect/pivot)
  and `CardMeshTrimmer` (bounds-refit or UV-trimmed mesh copies; source
  assets are never mutated).
- **Grounded pose** — `GroundPlacementSolver` turns sprite metrics into a
  world-space position relative to a caller-supplied ground surface.

Pixel input is abstracted behind `IPixelSource` (`ArrayPixelSource`,
`TexturePixelSource`, `SpritePixelSource`, `RenderTexturePixelSource` for
non-readable textures). Results are pure functions of pixels + profile;
`SpriteGroundingCache` and `SpriteGroundingBatch` provide keying,
dedup and budgeted pre-pass processing.

The package has no dependencies on Zenject, TileWorldCreator or any
game-domain types.
