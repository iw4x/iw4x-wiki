<!-- TITLE:GfxImages -->

Image assets are small assets containing metadata about a texture that the game will then stream from disk.
They are mostly referenced to from other assets via [materials](/modern-warfare-2/assets/materials.md) and are only sometimes directly referenced (by the Skybox for instance, or reflection probes).

## Texture
The texture in the game files is a reference to a `GfxImageLoadDef`, an instruction about how to load the actual texture in memory - once the GfxImage is loaded by the game, this reference is **replaced** by an appropriate DirectX9 loaded texture (IDirect3DTexture9, ...)

The load definition of a texture has various properties:

### Texture flags
| Flag | Meaning |
| -------- | -------- |
| IMG_FLAG_NOMIPMAPS | The texture does contain [mip maps](https://en.wikipedia.org/wiki/Mipmap) - mipmaps are duplicates of the original texture of smaller and smaller size that are used to reduce memory usage when rendering far objects, like a level-of-detail for textures.   |
| IMG_FLAG_NOPICMIP     |   Not sure - might indicate the mipmaps should not change after image data has been loaded? Is it used on PC ?|
| IMG_FLAG_MAPTYPE_CUBE | The texture is a cube map (6 faces) and will be loaded into a IDirect3DCubeTexture9 |
| IMG_FLAG_MAPTYPE_3D | The texture is a volume and should be loaded into a IDirect3DVolumeTexture9 |
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
| IMG_FLAG_RENDER_TARGET | Usage unknown - probably used to play a video or a camera screen? |
| IMG_FLAG_SYSTEMMEM | Usage unknown |
