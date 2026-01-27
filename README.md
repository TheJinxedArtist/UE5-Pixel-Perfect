# UE5-Pixel-Perfect
A material post processing effect for Unreal Engine 5 for pixel-based games.

## How To Use

![An image of the material editor within Unreal Engine 5.](images/material-editing.png)

It's pretty simple to use, and most values are self-explanitory. "Dual Colour Toning", "HSV Blending" and "Fast Linear to sRGB" act as booleans, though we cannot use boolean values as shader properties, so they are shown as 0-1 floats.

> [!WARNING]
> I would advise against using any floating-point value on any of the "booleans", just stick to 0 or 1.

Basically, to use it, open your Unreal Engine project in the file explorer (make sure Unreal Engine is closed). Under Content, create a "Graphics" folder (including capital G) and copy the UEPixelPerfect folder into this Graphics folder.

The reason for this specific layout is because Unreal Engine throws a bit of a hissy fit if you don't copy things and paste them with the *exact* same path, I tend to put all generic effects into a Graphics folder, and so you're forced to do it too.

To then actually see it, create a Post Process Volume, go down to Rendering Features, add a new Post Process Material and set the material to one of the examples, found in UEPixelPerfect/Examples. Alternatively, create your own material instance of M_PixelPerfect and change the settings yourself.

## About

Unreal Engine is primarily designed for developing realistic 3D games, and while its built-in post processing effects and tonemapper work well, they completely destroy any attempt at NPR (non-photorealistic) visuals. More specifically, the built-in (and force-enabled) ACES-based tonemapper tends to warp and shift colours, which works great in a photorealistic game, but not so much in a pixel-based game, just for example.

UE Pixel Perfect aims to solve this issue, and adds some artistic utilities, so that people can see your game in the way you intended.

At it's core, UEPP replaces the tonemapper with a simple Linear -> sRGB conversion, immediately restoring the original and artist-intended colours. But realistically, too many things are made separate these days (cough cough Maya, Photoshop, Substance Painter cough cough), and so the material includes plenty of other effects, as listed here:

- Linear -> sRGB conversion (duh)
- Image resolution scaling
- Colour quantization
- Dithering (with dither textures, 4x4 bayer matrix & blue noise included)
- Dual colour toning

### Image Resolution Scaling
It's as simple as it sounds: scale the resolution of the screen. Use a 0-1 value to control the scaling, with 0 being no resolution, 0.5 being 50% of the original resolution, and 1 (default) being the source resolution.

### Colour Quantization
Despite the scary big word, it basically means "reduce the number of colours on screen". Default is 1024, but realistically for any effect use 8, 16, 32, etc...

### Dithering
Dithering works right beside colour quantization to smooth out the harsh steps using a dither pattern, with a 4x4 bayer matrix & blue noise pattern included by default.

### Dual Colour Toning
Blend between two colours based on the image's luminance. You can optionally use HSV blending for a more colourful result, and it already works with colour quantization and dithering.
