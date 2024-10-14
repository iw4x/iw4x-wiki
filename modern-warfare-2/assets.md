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
| 3 |   XModelSurfaces | A **surface** is how the game calls a mesh, or a continuous mesh. A XModelSurfaces is a group of one or more meshes
| 4 |   XModel | A XModel is an ensemble of surfaces, materials, collisions, skeleton and physical properties that constitute a model for the game - with up to 4 LODs. |
| 5 |   Materials | Materials are sets of textures and parame
| 6 |   PIXELSHADER |
| 7 |   VERTEXSHADER |
| 8 |   VERTEXDECL |
| 9 |   TECHNIQUE_SET |
| 10 |   IMAGE |
| 11 |   SOUND |
| 12 |   SOUND_CURVE |
| 13 |   LOADED_SOUND |
| 14 |   CLIPMAP_SP |
| 15 |   CLIPMAP_MP |
| 16 |   COMWORLD |
| 17 |   GAMEWORLD_SP |
| 18 |   GAMEWORLD_MP |
| 19 |   MAP_ENTS |
| 20 |   FXWORLD |
| 21 |   GFXWORLD |
| 22 |   LIGHT_DEF |
| 23 |   UI_MAP |
| 24 |   FONT |
| 25 |   MENULIST |
| 26 |   MENU |
| 27 |   LOCALIZE_ENTRY |
| 28 |   WEAPON |
| 29 |   SNDDRIVER_GLOBALS |
| 30 |   FX |
| 31 |   IMPACT_FX |
| 32 |   AITYPE |
| 33 |   MPTYPE |
| 34 |   CHARACTER |
| 35 |   XMODELALIAS |
| 36 |   RAWFILE |
| 37 |   STRINGTABLE |
| 38 |   LEADERBOARD |
| 39 |   STRUCTURED_DATA_DEF |
| 40 |   TRACER |
| 41 |   VEHICLE |
| 42 |   ADDON_MAP_ENTS |
| 43 |   COUNT |
| 44 |   STRING |
| 45 |   ASSETLIST |

-->

