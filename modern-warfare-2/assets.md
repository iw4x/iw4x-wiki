<!-- TITLE:Assets -->

Every element in the game is made of one or multiple assets. Each asset has its own type and structure, and certain asset types can or will contain several other assets.
*e.g. : Models, Materials and Images are separate assets, but a Model can reference several Materials which in turn reference several different Images each.*

The structure documented here is the one assets have **in memory** once loaded by the game - this is not necessarily the same structure they appear as on the disk when they do, and it is not the same structure as the source files (map files, sound aliases, etc) from which they were built. Most of everything in IW4 is *baked* in the sense that every asset underwent an irreversible transformation to go from the files the developer were working with (GDT, XMODEL_EXPORT, BSP, ...) to the assets the **game** works with (Material, XModel, GfxWorld, ...).

# Asset types

| Column 1 | Column 2 | Column 3 |
| -------- | -------- | -------- |
| Text     | Text     | Text     |


