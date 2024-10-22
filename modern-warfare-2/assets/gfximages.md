<!-- TITLE:GfxImages -->

Image assets are small assets containing metadata about a texture that the game will then stream from disk.
They are mostly referenced to from other assets via [materials](/modern-warfare-2/assets/materials.md) and are only sometimes directly referenced (by the Skybox for instance, or reflection probes).

## Map Type
| Number | Type | Meaning |
| -------- | -------- | -------- |
| 3 | MAPTYPE_2D | A two dimensional texture |
| 4 | MAPTYPE_3D | The texture is a volume and should be loaded into a IDirect3DVolumeTexture9 |
| 5 | MAPTYPE_CUBE | The texture has 6 sides and should be loaded into a IDirect3DCubeTexture9  |


## Texture
The texture in the game files is a reference to a `GfxImageLoadDef`, an instruction about how to load the actual texture in memory - once the GfxImage is loaded by the game, this reference is **replaced** by an appropriate DirectX9 loaded texture (IDirect3DTexture9, ...)

Most images are loaded from [IWI files](/modern-warfare-2/assets/streamed-files.md) but some of them are entirely contained within the image asset instead - the lightmaps, reflection probes are like this for instance.
:::info 
ZoneBuilder stores loaded-images as IW4xImage files, as their own format - other images are usually found as IWI files inside IWD archives the game ships with.
:::

The load definition of a texture has various properties:

### Texture flags
| Flag | Meaning |
| -------- | -------- |
| IMG_FLAG_NOMIPMAPS | The texture does contain [mip maps](https://en.wikipedia.org/wiki/Mipmap) - mipmaps are duplicates of the original texture of smaller and smaller size that are used to reduce memory usage when rendering far objects, like a level-of-detail for textures.   |
| IMG_FLAG_NOPICMIP     |   Not sure - might indicate the mipmaps should not change after image data has been loaded? Is it used on PC ?|
| IMG_FLAG_MAPTYPE_CUBE | Redundant with MAPTYPE_CUBE |
| IMG_FLAG_MAPTYPE_3D | Redundant with MAPTYPE_3D |
| IMG_FLAG_MAPTYPE_1D | The image has a single-dimension (gradient)  |
| IMG_FLAG_STREAMING | The texture can be loaded on demand |
| IMG_FLAG_LEGACY_NORMALS | Usage unknown - already present in CoD4 |
| IMG_FLAG_CLAMP_U & IMG_FLAG_CLAMP_V | When the texture is sampled with texture coordinates (UV) outside of the range 0<>1, the last row of pixels should be repeated instead of the whole texture. U for horizontal and V for vertical - these are probably passed as-is to the sampler state (SAMPLER_CLAMP_U & SAMPLER_CLAMP_V) of DirectX9 before drawing |
| IMG_FLAG_ALPHA_WEIGHTED_COLORS | Usage unknown |
| IMG_FLAG_DXTC_APPROX_WEIGHTS | Usage unknown - probably related to Load_Dxtc and DXT textures |
| IMG_FLAG_GAMMA_NONE | The image has linear RGB |
| IMG_FLAG_GAMMA_SRGB | The image has gamma (SRGB) |
| IMG_FLAG_GAMMA_PWL | Meaning unknown - likely PWL means "power law" |
| IMG_FLAG_GAMMA_2 | Combines both gamma flags SRGB and PWL |
| IMG_FLAG_NORMALMAP | The image is a normal map |
| IMG_FLAG_INTENSITY_TO_ALPHA | Usage unknown |
| IMG_FLAG_DYNAMIC | Usage unknown - maybe related to dynamic images created to sample model lighting and code images |
| IMG_FLAG_RENDER_TARGET | Only available with the 2D texture semantic - render target textures are filled at runtime with data from the rendered scene, to compute reflections and post process effects. |
| IMG_FLAG_SYSTEMMEM | Usage unknown |

### Texture semantic
This property is usually redundant and gives information about which sampler a material is supposed to use it with:

| Number | Semantic | Description |
| -------- | -------- | -------- |
| 0     | 2D     | Used for images drawn on screen (menus, HUD, etc) |
| 1     | Function     | This image is a lookup table for a shader or a material to use |
| 2     | Color     | Used for images drawn on screen (menus, HUD, etc) |
| 3     | Detail     | A detail map is a second color map drawn ontop of the color map to add some noise and grain to the render - usually it's repeated and drawn over the color map many times. |
| 5     | Normal    | Normal maps change the way lighting interacts with the surface to create the impression of volume |
| 8     | Specular    | Speculars are used to intensify lighting depending on the angle between the view and the model and create a reflection effect |
| 11     | Water    | User for water textures which are a very special kind of runtime-computed surface |

## Image category
**This is a very important information that tells the game how to recover the image when the Direct3D device is lost or recovered **- whenever the game goes in background and loses its render, or is brought back from background and has to render again, it uses the image category of each loaded texture to decide what to do about it.

If the image category is wrong, the engine will accept it, but as soon as it needs to recover it after a device change it will trip and fall with a DirectX error.

|  Number |Category | Meaning |
| -------- | -------- | -------- |
| 1     | Autogenerated     |      |
| 2     | Lightmap  | self-explanatory    |
| 3     | LoadFromFile  | This image data is expected to be read from the `images/` folder in an IWD, with the \*.iwi extension. The vast majority of IW4 images have this category. |
| 4 | Raw | Not sure - might be used for reflection probes and other memory-loaded kind of images? |
| 5 | Water | Not sure - A texture generated from water data? Redundant from Texture Semantic? |
| 6 | Render Target | Not sure - Redundant from Texture Semantic? |

## Picmip
GfXImages that use mipmaps have two indices for the "best" mipmap to pick - one for the usual scenario (the first one) and one for the min-spec worst case scenario (the second one). This information can be globally overwritten on load depending on the `r_picmip` dvars values.

## Other properties
- `track` is used for debugging and might be unused in the release version of IW4
- `cardMemory` is a runtime information related to PicMips - not exactly sure about what
- `delayLoadPixels` is used in conjunction with streaming to tell the image can load-on-demand, but not sure exactly what that implies
