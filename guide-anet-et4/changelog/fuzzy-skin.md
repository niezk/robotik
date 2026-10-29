# Fuzzy Skin¶

Fuzzy skin randomly perturbs the wall path to produce a deliberately rough, matte appearance on the model surface.\
These settings control where the effect is applied, how the noise is generated, and how aggressive the displacement or extrusion modulation is.

Useful for creating textures or hiding surface imperfections, but it increases print time and affects dimensional accuracy.

* [Fuzzy Skin Mode](fuzzy-skin.md#fuzzy-skin-mode)
  * [Contour](fuzzy-skin.md#contour)
  * [Hole](fuzzy-skin.md#hole)
  * [Contour and Hole](fuzzy-skin.md#contour-and-hole)
  * [Painted Only](fuzzy-skin.md#painted-only)
  * [All Walls](fuzzy-skin.md#all-walls)
  * [Disabled](fuzzy-skin.md#disabled)
* [Fuzzy Skin Generator Mode](fuzzy-skin.md#fuzzy-skin-generator-mode)
  * [Displacement](fuzzy-skin.md#displacement)
  * [Extrusion](fuzzy-skin.md#extrusion)
  * [Combined](fuzzy-skin.md#combined)
* [Noise Type](fuzzy-skin.md#noise-type)
  * [Classic](fuzzy-skin.md#classic)
  * [Perlin](fuzzy-skin.md#perlin)
  * [Billow](fuzzy-skin.md#billow)
  * [Ridged Multifractal](fuzzy-skin.md#ridged-multifractal)
  * [Voronoi](fuzzy-skin.md#voronoi)
  * [Ripple](fuzzy-skin.md#ripple)
    * [Ripples per layer](fuzzy-skin.md#ripples-per-layer)
    * [Ripple offset](fuzzy-skin.md#ripple-offset)
    * [Layers between ripple offset](fuzzy-skin.md#layers-between-ripple-offset)
* [Point distance](fuzzy-skin.md#point-distance)
* [Skin thickness](fuzzy-skin.md#skin-thickness)
* [Skin feature size](fuzzy-skin.md#skin-feature-size)
* [Skin Noise Octaves](fuzzy-skin.md#skin-noise-octaves)
* [Skin Noise Persistence](fuzzy-skin.md#skin-noise-persistence)
* [Apply fuzzy skin to first layer](fuzzy-skin.md#apply-fuzzy-skin-to-first-layer)
* [Credits](fuzzy-skin.md#credits)

## Fuzzy Skin Mode[¶](fuzzy-skin.md#fuzzy-skin-mode) <a href="#fuzzy-skin-mode" id="fuzzy-skin-mode"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Simple`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `fuzzy_skin`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `Choice`.\
[Options](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `none, external, hole, all, allwalls, disabled_fuzzy`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--fuzzy-skin=none`.\
Choose which parts of the model receive the fuzzy-skin effect.

### Contour[¶](fuzzy-skin.md#contour) <a href="#contour" id="contour"></a>

Apply fuzzy skin only to the outermost contour (external perimeter) of the model.\
Useful for creating a textured edge while keeping the inner surfaces smooth.

### Hole[¶](fuzzy-skin.md#hole) <a href="#hole" id="hole"></a>

Apply fuzzy skin only to interior holes and cutouts. This can add grip or visual interest to negative features without affecting the outer surface.

### Contour and Hole[¶](fuzzy-skin.md#contour-and-hole) <a href="#contour-and-hole" id="contour-and-hole"></a>

Apply fuzzy skin to both the outer contour and interior holes. Useful when you want the rough texture to appear on negative features as well.

### Painted Only[¶](fuzzy-skin.md#painted-only) <a href="#painted-only" id="painted-only"></a>

Apply fuzzy skin only to areas that have been manually painted with the [Fuzzy Skin Paint Tool](/broken/pages/d8d0341929abdb0d17007e2fa7d9f15256221cf7).\
This allows for precise control over where the texture is applied, ideal for adding grip to specific areas or creating custom patterns.

### All Walls[¶](fuzzy-skin.md#all-walls) <a href="#all-walls" id="all-walls"></a>

Apply fuzzy skin to every wall (external and internal). This gives the strongest overall textured appearance but will increase slicing and print time considerably.

### Disabled[¶](fuzzy-skin.md#disabled) <a href="#disabled" id="disabled"></a>

The default. No fuzzy skin is applied, not even on areas painted with the [Fuzzy Skin Paint Tool](/broken/pages/d8d0341929abdb0d17007e2fa7d9f15256221cf7), and the other fuzzy skin settings are hidden.\
This is what sets it apart from [Painted Only](fuzzy-skin.md#painted-only), which applies fuzzy skin to the painted areas only. If you paint an object while fuzzy skin is disabled, the paint tool warns that the painting won't take effect and offers to switch that object to Painted Only.

## Fuzzy Skin Generator Mode[¶](fuzzy-skin.md#fuzzy-skin-generator-mode) <a href="#fuzzy-skin-generator-mode" id="fuzzy-skin-generator-mode"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Simple`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `fuzzy_skin_mode`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `Choice`.\
[Options](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `displacement, extrusion, combined`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--fuzzy-skin-mode=displacement`.\
Select the underlying method used to produce the fuzzy effect. Each mode has different trade-offs for strength, speed and mechanical load.

### Displacement[¶](fuzzy-skin.md#displacement) <a href="#displacement" id="displacement"></a>

![Fuzzy-skin-Displacement-mode](<.gitbook/assets/Fuzzy skin Displacement mode.png>)

The classic method, where the pattern on the walls is created by shifting the print head perpendicular to the wall.\
It gives a predictable result, but it reduces the strength of the whole shell and opens pores inside the walls. It also increases the mechanical stress on the printer's kinematics and slows down printing overall.

### Extrusion[¶](fuzzy-skin.md#extrusion) <a href="#extrusion" id="extrusion"></a>

![Fuzzy-skin-Extrusion-mode](<.gitbook/assets/Fuzzy skin Extrusion mode.png>)

The fuzzy skin effect is created by varying the amount of extruded plastic while the print head follows the original path. There is no extra load on the kinematics, no decrease in print speed, and no pores open, but the pattern is about half as pronounced. It is suitable for creating "loose" walls that reduce internal stress in the extruded plastic, or for masking print defects on the side walls with a matte effect.

Caution

In this mode, **Fuzzy skin thickness** sets how much the line width varies. A line can't be extruded thinner than about 23% of the layer height, so Orca clamps the thinnest parts to that minimum. Once the thickness exceeds the wall line width, higher values only make the wide parts wider.\
The [Arachne](/broken/pages/54a6fe288c2767d758a6868ebef10f327f69163c#arachne) wall generator must also be enabled.

### Combined[¶](fuzzy-skin.md#combined) <a href="#combined" id="combined"></a>

![Fuzzy-skin-Combined-mode](<.gitbook/assets/Fuzzy skin Combined mode.png>)

This is a combination of the Displacement and Extrusion modes. The pattern is as sharp as in Displacement mode, but the walls remain strong and tight. The load on the kinematics is halved. Printing is faster than in Displacement mode, but still slower than in Extrusion mode.

Warning

The limits on line thickness and the Arachne requirement are the same as in the Extrusion mode.

## Noise Type[¶](fuzzy-skin.md#noise-type) <a href="#noise-type" id="noise-type"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Simple`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `fuzzy_skin_noise_type`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `Choice`.\
[Options](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `classic, perlin, billow, ridgedmulti, voronoi, ripple`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--fuzzy-skin-noise-type=classic`.\
Select the noise algorithm used to generate the random offsets. Different noise types produce distinct visual textures.

### Classic[¶](fuzzy-skin.md#classic) <a href="#classic" id="classic"></a>

Simple uniform random noise. Produces a coarse, irregular texture.

![Fuzzy-skin-classic](<.gitbook/assets/Fuzzy skin classic.png>)

### Perlin[¶](fuzzy-skin.md#perlin) <a href="#perlin" id="perlin"></a>

[Perlin noise](https://en.wikipedia.org/wiki/Perlin_noise) generates smooth, natural-looking variations with coherent structure.

![Fuzzy-skin-perlin](<.gitbook/assets/Fuzzy skin perlin.png>)

### Billow[¶](fuzzy-skin.md#billow) <a href="#billow" id="billow"></a>

Billow noise is similar to Perlin noise, but has a clumpier appearance. It can create more pronounced features and is often used for natural textures.

![Fuzzy-skin-billow](<.gitbook/assets/Fuzzy skin billow.png>)

### Ridged Multifractal[¶](fuzzy-skin.md#ridged-multifractal) <a href="#ridged-multifractal" id="ridged-multifractal"></a>

Creates sharp, jagged features and high-contrast detail. Useful for stone- or marble-like textures.

![Fuzzy-skin-ridged-multifractal](<.gitbook/assets/Fuzzy skin ridged multifractal.png>)

### Voronoi[¶](fuzzy-skin.md#voronoi) <a href="#voronoi" id="voronoi"></a>

[Voronoi noise](https://en.wikipedia.org/wiki/Worley_noise) divides the surface into Voronoi cells and displaces each cell independently, creating a patchwork or cellular texture.

![Fuzzy-skin-voronoi](<.gitbook/assets/Fuzzy skin voronoi.png>)

### Ripple[¶](fuzzy-skin.md#ripple) <a href="#ripple" id="ripple"></a>

The Ripple noise type creates a regular, wave-like pattern of ripples across the surface.\
This is useful for decorative purposes on models that do not have abrupt changes in geometry or holes that create multiple print islands (closed loops), since the number of ripples is applied to each closed loop and can cause discontinuities between layers.

A clear example is a 3DBenchy, whose windows create small print islands that get the same number of ripples as the hull of the boat, where there is much more space for them.

![Fuzzy-skin-ripple](<.gitbook/assets/Fuzzy skin ripple.png>) ![Fuzzy-skin-ripple-example](<.gitbook/assets/Fuzzy skin ripple example.jpg>)

#### Ripples per layer[¶](fuzzy-skin.md#ripples-per-layer) <a href="#ripples-per-layer" id="ripples-per-layer"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `fuzzy_skin_ripples_per_layer`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Integer`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--fuzzy-skin-ripples-per-layer=1`.\
Controls how many full cycles of ripples will be added per layer.

#### Ripple offset[¶](fuzzy-skin.md#ripple-offset) <a href="#ripple-offset" id="ripple-offset"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `fuzzy_skin_ripple_offset`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Percentage`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--fuzzy-skin-ripple-offset=20%`.\
Shifts the ripple phase forward along the print path by the specified percentage of a wavelength each layer period. Values are specified between 0% and 100% (0% = no shift, 100% = a full-wavelength shift).

* 0% keeps every layer identical.
* 50% shifts the pattern by half a wavelength, effectively inverting the phase.
* 100% shifts the pattern by a full wavelength, returning to the original phase.

The shift is applied once every number of layers set by [Layers between ripple offset](fuzzy-skin.md#layers-between-ripple-offset), so layers within the same group are printed identically.

#### Layers between ripple offset[¶](fuzzy-skin.md#layers-between-ripple-offset) <a href="#layers-between-ripple-offset" id="layers-between-ripple-offset"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `fuzzy_skin_layers_between_ripple_offset`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Integer`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--fuzzy-skin-layers-between-ripple-offset=1`.\
Specifies how many consecutive layers share the same ripple phase before the offset is applied.\
For example, with the default 50% [Ripple offset](fuzzy-skin.md#ripple-offset):

* 1 = Layer 1 is printed with the base ripple pattern, then layer 2 is shifted by the configured offset, then layer 3 returns to the base pattern, and so on.
* 3 = Layers 1 to 3 are printed with the base ripple pattern, then layers 4 to 6 are shifted by the configured offset, then layers 7 to 9 return to the base pattern, etc.

## Point distance[¶](fuzzy-skin.md#point-distance) <a href="#point-distance" id="point-distance"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Simple`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `fuzzy_skin_point_distance`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--fuzzy-skin-point-distance=1`.\
Average distance between random sample points along each line segment.\
Smaller values add more detail and increase computation; larger values produce coarser, faster results.

## Skin thickness[¶](fuzzy-skin.md#skin-thickness) <a href="#skin-thickness" id="skin-thickness"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Simple`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `fuzzy_skin_thickness`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--fuzzy-skin-thickness=1`.\
Maximum lateral width (in mm) over which points can be displaced. This defines how far the wall can be jittered.\
Keep this below or near your outer wall line width and within nozzle/flow limits for reliable prints.

## Skin feature size[¶](fuzzy-skin.md#skin-feature-size) <a href="#skin-feature-size" id="skin-feature-size"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `fuzzy_skin_scale`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--fuzzy-skin-scale=1`.\
Base size of coherent noise features, in mm. Larger values yield bigger, more prominent structures; smaller values give fine-grained texture.

## Skin Noise Octaves[¶](fuzzy-skin.md#skin-noise-octaves) <a href="#skin-noise-octaves" id="skin-noise-octaves"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `fuzzy_skin_octaves`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Integer`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--fuzzy-skin-octaves=1`.\
The number of octaves of coherent noise to use. Higher values increase the detail of the noise, but also increase computation time.

## Skin Noise Persistence[¶](fuzzy-skin.md#skin-noise-persistence) <a href="#skin-noise-persistence" id="skin-noise-persistence"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `fuzzy_skin_persistence`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--fuzzy-skin-persistence=1`.\
Controls how amplitude decays across octaves. Lower persistence results in smoother noise; higher persistence keeps finer-scale detail stronger.

## Apply fuzzy skin to first layer[¶](fuzzy-skin.md#apply-fuzzy-skin-to-first-layer) <a href="#apply-fuzzy-skin-to-first-layer" id="apply-fuzzy-skin-to-first-layer"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Simple`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `fuzzy_skin_first_layer`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--fuzzy-skin-first-layer=1`.\
Enable to apply fuzzy skin to the first layer.

Caution

Can impact bed adhesion and surface contact.

## Credits[¶](fuzzy-skin.md#credits) <a href="#credits" id="credits"></a>

* **Generator Mode author:** [@pi-squared-studio](https://github.com/pi-squared-studio).
