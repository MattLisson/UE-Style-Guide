# 1. Asset Naming Conventions
[](){ #anc }
[](){ #1 }

Naming conventions should be treated as law. A project that conforms to a naming convention is able to have its assets managed, searched, parsed, and maintained with incredible ease.

Most things are suffixed with suffixes being generally an acronym of the asset type separated by an underscore from the base asset name.

[](){ #base-asset-name }
[](){ #1.1 }
## 1.1 Base Asset Names

All assets should have a _Base Asset Name_. A Base Asset Name represents a logical grouping of related assets. Any asset that is part of this logical group should follow the standard of  `Prefix_BaseAssetName_Variant_Suffix`.

Keeping the pattern `Prefix_BaseAssetName_Variant_Suffix` in mind and using common sense is generally enough to warrant good asset names. Here are some detailed rules regarding each element.

`Prefix` and `Suffix` are to be determined by the asset type through the following [Asset Name Modifier][asset-name-modifiers] tables.

`BaseAssetName` should be determined by a short and easily recognizable name related to the context of this group of assets. For example, if you had a character named Bob, all of Bob's assets would have the `BaseAssetName` of `Bob`.

For unique and specific variations of assets, `Variant` is either a short and easily recognizable name that represents logical grouping of assets that are a subset of an asset's base name. For example, if Bob had multiple skins these skins should still use `Bob` as the `BaseAssetName` but include a recognizable `Variant`. An 'Evil' skin would be referred to as `Bob_Evil` and a 'Retro' skin would be referred to as `Bob_Retro`.

For unique but generic variations of assets, `Variant` is a two digit number starting at `01`. For example, if you have an environment artist generating nondescript rocks, they would be named `Rock_01`, `Rock_02`, `Rock_03`, etc. Except for rare exceptions, you should never require a three digit variant number. If you have more than 100 assets, you should consider organizing them with different base names or using multiple variant names.

Depending on how your asset variants are made, you can chain together variant names. For example, if you are creating flooring assets for an Arch Viz project you should use the base name `Flooring` with chained variants such as `Flooring_Marble_01`, `Flooring_Maple_01`, `Flooring_Tile_Squares_01`.

[](){ #1.1-examples }
### 1.1 Examples

#### 1.1e1 Bob

| Asset Type               | Asset Name                                                 |
| ------------------------ | ---------------------------------------------------------- |
| Skeletal Mesh            | Bob_SK                                                     |
| Material                 | Bob_M                                                      |
| Texture (Base Color)     | T_Bob_BC                                                   |
| Texture (Normal)         | T_Bob_N                                                    |
| Texture (Evil Base Color)| T_Bob_Evil_BC                                              |

#### 1.1e2 Rocks

| Asset Type              | Asset Name                                                 |
| ----------------------- | ---------------------------------------------------------- |
| Static Mesh (01)        | Rock_01_SM                                                 |
| Static Mesh (02)        | Rock_02_SM                                                 |
| Static Mesh (03)        | Rock_03_SM                                                 |
| Material                | Rock_M                                                     |
| Material Instance (Snow)| Rock_Snow_MI                                               |

[](){ #asset-name-modifiers }
[](){ #1.2 }
## 1.2 Asset Name Modifiers

When naming an asset, use these tables to determine the prefix and suffix to use with an asset's [Base Asset Name][base-asset-name].

[](){ #anc-common }
[](){ #1.2.1 }
### 1.2.1 Common

| Asset Type              | Prefix     | Suffix     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Level / Map             |            |            | [Should be in a folder called Maps.][structure-maps] |
| Level (Persistent)      |            | _P         |                                  |
| Level (Audio)           |            | _Audio     |                                  |
| Level (Lighting)        |            | _Lighting  |                                  |
| Level (Geometry)        |            | _Geo       |                                  |
| Level (Gameplay)        |            | _Gameplay  |                                  |
| Blueprint               |            | _BP        |                                  |
| Material                |            | _M         |                                  |
| Static Mesh             |            | _SM        |                                  |
| Skeletal Mesh           |            | _SK        |                                  |
| Texture                 | T_         | _?         | See [Textures][anc-textures]    |
| Widget Blueprint        |            | _WBP       |                                  |

[](){ #anc-animations }
[](){ #1.2.2 }
### 1.2.2 Animations

| Asset Type              | Prefix     | Suffix     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Aim Offset              |            | _AO        |                                  |
| Aim Offset 1D           |            | _AO        |                                  |
| Animation Blueprint     |            | _ABP       |                                  |
| Animation Composite     |            | _AC        |                                  |
| Animation Montage       |            | _AM        |                                  |
| Animation Sequence      |            | _AS        |                                  |
| Blend Space             |            | _BS        |                                  |
| Blend Space 1D          |            | _BS        |                                  |
| Level Sequence          |            | _LS        |                                  |
| Morph Target            |            | _MT        |                                  |
| Paper Flipbook          |            | _PFB       |                                  |
| Rig                     |            | _Rig       |                                  |
| Control Rig             |            | _CR        |                                  |
| Skeletal Mesh           |            | _SK        |                                  |
| Skeleton                |            | _SKEL      |                                  |

[](){ #anc-ai }
[](){ #1.2.3 }
### 1.2.3 Artificial Intelligence

| Asset Type              | Prefix     | Suffix      | Notes                            |
| ----------------------- | ---------- | ----------- | -------------------------------- |
| AI Controller           |            | _AIC        |                                  |
| Behavior Tree           |            | _BT         |                                  |
| Blackboard              |            | _BB         |                                  |
| Decorator               |            | _BTDecorator|                                  |
| Service                 |            | _BTService  |                                  |
| Task                    |            | _BTTask     |                                  |
| Environment Query       |            | _EQS        |                                  |
| EnvQueryContext         |            | _EQSContext |                                  |

[](){ #anc-bp }
[](){ #1.2.4 }
### 1.2.4 Blueprints

| Asset Type                 | Prefix     | Suffix       | Notes                                   |
| -------------------------- | ---------- | ------------ | --------------------------------------- |
| Blueprint                  |            | _BP          |                                         |
| Blueprint Component        |            | Component_BP | e.g. InventoryComponent_BP              |
| Blueprint Function Library |            | _BPFL        |                                         |
| Blueprint Interface        |            | _BPI         |                                         |
| Blueprint Macro Library    |            | _BPML        | Do not use macro libraries if possible. |
| Enumeration                | E          |              | No underscore, e.g. EDirection.         |
| Structure                  | S          |              | No underscore, e.g. SDirection.         |
| Tutorial Blueprint         |            | _TBP         |                                         |
| Widget Blueprint           |            | _WBP         |                                         |

[](){ #anc-materials }
[](){ #1.2.5 }
### 1.2.5 Materials

| Asset Type              | Prefix     | Suffix     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Material                |            | _M         |                                  |
| Material (Post Process) |            | _PP        |                                  |
| Material Function       |            | _MF        |                                  |
| Material Instance       |            | _MI        |                                  |
| Material Parameter Collection |      | _MPC       |                                  |
| Subsurface Profile      |            | _SP        |                                  |
| Physical Materials      |            | _PM        |                                  |
| Decal                   |            | _Decal     |                                  |

[](){ #anc-textures }
[](){ #1.2.6 }
### 1.2.6 Textures

| Asset Type              | Prefix     | Suffix     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Texture                 | T_         |            |                                  |
| Texture (Diffuse/Albedo/Base Color)| T_ | _BC     |                                  |
| Texture (Metallic)      | T_         | _MT        |                                  |
| Texture (Normal)        | T_         | _N         |                                  |
| Texture (Roughness)     | T_         | _R         |                                  |
| Texture (Alpha/Opacity) | T_         | _A         |                                  |
| Texture (Ambient Occlusion) | T_     | _AO         |                                  |
| Texture (Bump)          | T_         | _B         |                                  |
| Texture (Emissive)      | T_         | _E         |                                  |
| Texture (Mask)          | T_         | _M         |                                  |
| Texture (Specular)      | T_         | _S         |                                  |
| Texture (Displacement)  | T_         | _DP        |                                  |
| Texture (Packed)        | T_         | _*         | See notes below about [packing][anc-textures-packing]. |
| Texture Cube            |            | _TC        |                                  |
| Media Texture           |            | _MT        |                                  |
| Render Target           |            | _RT        |                                  |
| Cube Render Target      |            | _RTC       |                                  |
| Texture Light Profile   |            | _TLP       |                                  |

[](){ #anc-textures-packing }
[](){ #1.2.6.1 }
### 1.2.6.1 Texture Packing
It is common practice to pack multiple layers of texture data into one texture. An example of this is packing Emissive, Roughness, Ambient Occlusion together as the Red, Green, and Blue channels of a texture respectively. To determine the suffix, simply stack the given suffix letters from above together, e.g. `_ERO`.

> It is generally acceptable to include an Alpha/Opacity layer in your Diffuse/Albedo's alpha channel and as this is common practice, adding `A` to the `_D` suffix is optional.

Packing 4 channels of data into a texture (RGBA) is not recommended except for an Alpha/Opacity mask in the Diffuse/Albedo's alpha channel as a texture with an alpha channel incurs more overhead than one without.

[](){ #anc-misc }
[](){ #1.2.7 }
### 1.2.7 Miscellaneous

| Asset Type              | Prefix     | Suffix     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Animated Vector Field   |            | _VFA       |                                  |
| Camera Anim             |            | _CA        |                                  |
| Color Curve             | Curve_     | _Color     |                                  |
| Curve Table             | Curve_     | _Table     |                                  |
| Data Asset              |            | _*         | Suffix should be based on class. |
| Data Table              |            | _DT        |                                  |
| Float Curve             | Curve_     | _Float     |                                  |
| Foliage Type            |            | _FT        |                                  |
| Landscape Grass Type    |            | _LG        |                                  |
| Landscape Layer         |            | _LL        |                                  |
| Matinee Data            |            | _Matinee   |                                  |
| Media Player            |            | _MP        |                                  |
| File Media Source       |            | _FMS       |                                  |
| Object Library          |            | _OL        |                                  |
| Redirector              |            |            | These should be fixed up ASAP.   |
| Sprite Sheet            |            | _SS        |                                  |
| Static Vector Field     |            | _VF        |                                  |
| Substance Graph Instance   |         | _SGI       |                                  |
| Substance Instance Factory |         | _SIF       |                                  |
| Touch Interface Setup   |            | _TI        |                                  |
| Vector Curve            | Curve_     | _Vector    |                                  |

[](){ #anc-paper2d }
[](){ #1.2.8 }
### 1.2.8 Paper 2D

| Asset Type              | Prefix     | Suffix     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Paper Flipbook          |            | _PFB       |                                  |
| Sprite                  |            | _SPR       |                                  |
| Sprite Atlas Group      |            | _SPRG      |                                  |
| Tile Map                |            | _TM        |                                  |
| Tile Set                |            | _TS        |                                  |

[](){ #anc-physics }
[](){ #1.2.9 }
### 1.2.9 Physics

| Asset Type              | Prefix     | Suffix     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Physical Material       |            | _PM        |                                  |
| Physics Asset	          |            | _PHYS      |                                  |
| Destructible Mesh       |            | _DM        |                                  |

[](){ #anc-sounds }
[](){ #1.2.10 }
### 1.2.10 Sounds

| Asset Type              | Prefix     | Suffix     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Dialogue Voice          |            | _DV        |                                  |
| Dialogue Wave           |            | _DW        |                                  |
| Media Sound Wave        |            | _MSW       |                                  |
| Reverb Effect           |            | _Reverb    |                                  |
| Sound Attenuation       |            | _ATT       |                                  |
| Sound Class             |            |            | No prefix/suffix. Should be put in a folder called SoundClasses |
| Sound Concurrency       |            | _SC        | Should be named after a SoundClass |
| Sound Cue               |            | _S_Cue     |                                  |
| Sound Mix               |            | _Mix       |                                  |
| Sound Wave              |            | _S         |                                  |
| MetaSound Source        |            | _MSS       |                                  |
| MetaSound Patch         |            | _MSP       |                                  |

[](){ #anc-ui }
[](){ #1.2.11 }
### 1.2.11 User Interface

| Asset Type              | Prefix     | Suffix     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Font                    |            | _Font      |                                  |
| Slate Brush             |            | _Brush     |                                  |
| Slate Widget Style      |            | _Style     |                                  |
| Widget Blueprint        |            | _WBP       |                                  |

[](){ #anc-effects }
[](){ #1.2.12 }
### 1.2.12 Effects

| Asset Type                            | Prefix     | Suffix     | Notes                            |
| ------------------------------------- | ---------- | ---------- | -------------------------------- |
| Material (Post Process)               |            | _PP        |                                  |
| Niagara Emitter                       | FX_        | _E         |                                  |
| Niagara System                        | FX_        | _S         |                                  |
| Niagara Module                        | FX_        | _M         |                                  |
| Niagara Dynamic Input Script          | FX_        | _IS        |                                  |
| Niagara Function Script               | FX_        | _FS        |                                  |
| Niagara Module Script                 | FX_        | _MS        |                                  |
| Niagara Data Channel                  | FX_        | _DC        |                                  |
| Niagara Effect Type                   | FX_        | _ET        |                                  |
| Niagara Parameter Collection          | FX_        | _P         |                                  |
| Niagara Parameter Collection Instance | FX_        | _PI        |                                  |
| Niagara Parameter Definitions         | FX_        | _PD        |                                  |
| Niagara Simulation Cache              | FX_        | _SC        |                                  |
| Niagara Validation Rule Set           | FX_        | _VRS       |                                  |

[](){ #anc-input }
[](){ #1.2.13 }
### 1.2.13 Input

| Asset Type                            | Prefix     | Suffix     | Notes                            |
| ------------------------------------- | ---------- | ---------- | -------------------------------- |
| Input Mapping Context                 |            | _IMC       |                                  |
| Input Action                          |            | _IA        |                                  |
| Force Feedback Attenuation            |            | _FFA       |                                  |
| Force Feedback Effect                 |            | _FFE       |                                  |
