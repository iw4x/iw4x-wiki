<!-- TITLE:Assets -->

Every element in the game is made of one or multiple assets. Each asset has its own type and structure, and certain asset types can or will contain several other assets.
*e.g. : Models, Materials and Images are separate assets, but a Model can reference several Materials which in turn reference several different Images each.*

The structure documented here is the one assets have **in memory** once loaded by the game - this is not necessarily the same structure they appear as on the disk when they do, and it is not the same structure as the source files (map files, sound aliases, etc) from which they were built. Most of everything in IW4 is *baked* in the sense that every asset underwent an irreversible transformation to go from the files the developer were working with (GDT, XMODEL_EXPORT, BSP, ...) to the assets the **game** works with (Material, XModel, GfxWorld, ...).

Every asset has a **name**, although it is not unique and not stored in the same manner depending on the asset.

# Asset types
| Number | Asset type | Description|
| -------- | -------- | -------- |
| 0     | PhysPreset    |   A physical preset is used with XModels to say how a piece of something should behave when fired at or near an explosion, how bouncy it is, etc... Physical properties. |
| 1     | PhysCollmap    |  Describes the shape of a physical object (broken down in a few "geom", geometrical primitives), its mass and size. |
| 2     | XAnimParts | Animations for a set of bones, often used with XModels too. Somewhat esoteric structure with a looot of data, from which the game reconstructs live animations |
| 3 |   XModelSurfaces | A **surface** is how the game calls a mesh, or a continuous mesh. A XModelSurfaces is a group of one or more meshes
| 4 |   XModel | A XModel is an ensemble of surfaces, materials, collisions, skeleton and physical properties that constitute a model for the game - with up to 4 LODs. |
| 5 |   [Materials](/modern-warfare-2/assets/materials.md)  | Materials are sets of textures and parameters to apply said textures onto a surface, aswell as reference to a technique set (rendering passes informations) |
| 6 |   [Pixel Shader](/modern-warfare-2/assets/pixel-&-vertex-shaders.md)  | A Pixel Shader is a computer program that is called for each pixel of a drawn object - usually with data passed along from a Vertex Shader. |
| 7 |   [Vertex Shader](/modern-warfare-2/assets/pixel-&-vertex-shaders.md) | Vertex Shaders are computer programs called once for each vertex for a drawn object, then pass the resulting info to a Pixel Shader |
| 8 |   Vertex Declaration | Vertex declarations describe which data from the game should be routed to a vertex shader (vertex position, color, texture coordinates, ...?) |
| 9 |   [Technique Set](/modern-warfare-2/assets/technique-sets.md)  | A technique set is an ensemble of up to 48 techniques (34 for MW1) describing different render passes the game should combine to draw a material. |
| 10 |   [Images](/modern-warfare-2/assets/gfximages.md) | While image data is [streamed](/modern-warfare-2/assets/streamed-files.md), each image has a corresponding GfxImage Asset which contains metadata about the texture |
| 11 |   Sound | "Sounds" are in reality sound alias lists, which mean they contain one or more definitions for sounds that should be played (distance, mixing, pitch, etc) |
| 12 |   Sound Curve | Simple definition files used by sound aliases to define how the game should behave over a distance |
| 13 |   Loaded sound | A wrapper for a sound that was fully loaded in memory by Miles Sound System |
| 14 |   Clipmap (Singleplayer | |
| 15 |   Clipmap (Multiplayer) | A clipmap contains all the collision from the original BSP a level was built from - and then some. It works similarly in MW2 as it does in Q3. |
| 16 |   Comworld | "Common world" contains pretty much only light positions and definitions, for ambient and omnidirectional lights in the level. |
| 17 |   Gameworld (Singleplayer) | |
| 18 |   Gameworld (Multiplayer) | A mostly empty but mandatory preallocated structure to hold the dynamic glass data from FxWorld once the game started - always empty in map files. |
| 19 |   Map entities | "MapEnts" contain a single very long string inherited from Q3 which lists all dynamic and scripted entities of the level, and information about the map triggers for gamemodes. |
| 20 |   FxWorld | The game world contains preallocated glass data for the whole level, for all the glass you can break |
| 21 |   GfxWorld | "Graphics world" contains all the graphical, visual part from the original BSP a level was built from - this data is linked and sometimes reminiscent to the ClipMap data. It contains most of everything that constitutes a level |
| 22 |   Light definition | Parameters that define a light (color, power, direction) |
| 23 |   Ui Map | |
| 24 |   Font | A font contains materials and the glyph table necessary to draw characters on screen |
| 25 |   MenuList | A transient asset that usually doesn't live in memory for too long (?) and contains a list of menus to load, or to unload. E.g. 'ingame menus', 'main menu', etc |
| 26 |   Menu | Each menu displayed in the game exists as a singular Menu asset in memory, which itself can reference other menus or share data with other menus from the same zone. |
| 27 |   Localized Entry | Smallest struct in the game: a localized entry is just a Key and a Translated value. 'MPUI_HIGHRISE' => 'Highrise' - and that's one whole localized entry asset. |
| 28 |   Weapon | Weapons are the biggest structs in the game besides GfxWorld and Clipmap, and contain every single thing a weapon need to work in the game - materials, sounds, animations, ... |
| 29 |   SndDriver Globals | (what is it for? sound globals are registered as a non-asset singleton by IW4...) | 
| 30 |   Fx | Special effects, used on the map and in weapons and everything else - usually references sounds, materials, etc. |
| 31 |   Impact FX | A list of FX |
| 32 |   Ai Type | |
| 33 |   Mp Type | Might be unused in this form - probably references mptype CSVs during building a level, a mptype being a set of characters to build into a map |
| 34 |   Character | Same as Mp Type - usually present as a rawfile (GSC Script) in the final game, this might have been used during level building only |
| 35 |   XModelAlias | Same as above |
| 36 |   [Rawfiles](/modern-warfare-2/assets/rawfiles.md) | Rawfiles are all files the game will do case-by-case parsing for - they can be scripts, vision files, anything that usually involve a form of Com_Parse |
| 37 |   Stringtable |  |
| 38 |   Leaderboard | |
| 39 |   Structured Data Definition | Similar to a struct in a headerfile in C++, a structured data definition outline how some specific data - usually player data - should be stored, so that the game can migrate between different definitions of a same data. |
| 40 |   Tracer | Parameters for special effects when a weapon is fired - usually dependent on a material. |
| 41 |   Vehicle | |
| 42 |   Addon map ents | Might be singleplayer only (spec ops?) |



