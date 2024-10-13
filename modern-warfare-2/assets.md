<!-- TITLE:Assets -->

Every element in the game is made of one or multiple assets. Each asset has its own type and structure, and certain asset types can or will contain several other assets.
*e.g. : Models, Materials and Images are separate assets, but a Model can reference several Materials which in turn reference several different Images each.*

The structure documented here is the one assets have **in memory** once loaded by the game - this is not necessarily the same structure they appear as on the disk when they do, and it is not the same structure as the source files (map files, sound aliases, etc) from which they were built. Most of everything in IW4 is *baked* in the sense that every asset underwent an irreversible transformation to go from the files the developer were working with (GDT, XMODEL_EXPORT, BSP, ...) to the assets the **game** works with (Material, XModel, GfxWorld, ...).

Every asset has a **name**, although it is not unique and not stored in the same manner depending on the asset.

# Asset types
<!--
| Number | Asset type | Description|
| -------- | -------- | -------- |
| 0     | PhysPreset    |   A physical preset is used with XModels to say how a piece of something should behave when fired at or near an explosion, how bouncy it is, etc... Physical properties. |
| 1     | PhysCollmap    |  Describes the shape of a physical object (broken down in a few "geom", geometrical primitives), its mass and size. |
| 2     | XAnimParts | Animations for a set of bones, often used with XModels too. Somewhat esoteric structure with a looot of data, from which the game reconstructs live animations |
| | |

-->

