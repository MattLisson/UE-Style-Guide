# 4. Static Meshes
[](){ #4 }
[](){ #Static Meshes }
[](){ #s }

This section will focus on Static Mesh assets and their internals.

## Sections

> 4.1 [UVs][s-uvs]
> 4.2 [LODs][s-lods]
> 4.3 [Modular Socketless Snapping][s-modular-snapping]
> 4.4 [Must Have Collision][s-collision]
> 4.5 [Correct Scale][s-scaled]

[](){ #4.1 }
[](){ #s-uvs }
## 4.1 Static Mesh UVs

[](){ #4.1.1 }
[](){ #s-uvs-no-missing }
### 4.1.1 All Meshes Must Have UVs

Pretty simple. All meshes, regardless how they are to be used, should not be missing UVs.

[](){ #4.1.2 }
[](){ #s-uvs-no-overlapping }
### 4.1.2 All Meshes Must Not Have Overlapping UVs for Lightmaps

Pretty simple. All meshes, regardless how they are to be used, should have valid non-overlapping UVs.

[](){ #4.2 }
[](){ #s-lods }
## 4.2 LODs Should Be Set Up Correctly

This is a subjective check on a per-project basis, but as a general rule any mesh that can be seen at varying distances should have proper LODs.

[](){ #4.3 }
[](){ #s-modular-snapping }
## 4.3 Modular Socketless Assets Should Snap To The Grid Cleanly

This is a subjective check on a per-asset basis, however any modular socketless assets should snap together cleanly based on the project's grid settings.

It is up to the project whether to snap based on a power of 2 grid or on a base 10 grid. However if you are authoring modular socketless assets for the marketplace, Epic's requirement is that they snap cleanly when the grid is set to 10 units or bigger.

[](){ #4.4 }
[](){ #s-collision }
## 4.4 All Meshes Must Have Collision

Regardless of whether an asset is going to be used for collision in a level, all meshes should have proper collision defined. This helps the engine with things such as bounds calculations, occlusion, and lighting. Collision should also be well-formed to the asset.

[](){ #4.5 }
[](){ #s-scaled }
## 4.5 All Meshes Should Be Scaled Correctly

This is a subjective check on a per-project basis, however all assets should be scaled correctly to their project. Level designers or blueprint authors should not have to tweak the scale of meshes to get them to confirm in the editor. Scaling meshes in the engine should be treated as a scale override, not a scale correction.
