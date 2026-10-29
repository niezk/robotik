# Layer Height¶

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Simple`.\
[Variables](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `layer_height`, `initial_layer_print_height`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--layer-height=1` (same pattern for the other variables above).\
Layer height defines the vertical thickness of each printed layer, playing a crucial role in both print quality and printing speed.

Note

You can use a variable layer height with the [Variable Layer Height](/broken/pages/284adfcde232b086faa6fd3565f63590e885838e) feature.

Using smaller layer heights increases print time but results in:

* Smoother surface finishes
* Less noticeable layer lines
* Enhanced detail on curves
* [Better performance on overhangs](layer-height.md#layer-height-overhangs-impacts)

![layer-height-spheres](<../../../.gitbook/assets/layer height spheres.png>)

* [Quick Reference](layer-height.md#quick-reference)
* [Layer Height Guidelines](layer-height.md#layer-height-guidelines)
* [First Layer Height](layer-height.md#first-layer-height)
* [Layer Height Overhangs Impacts](layer-height.md#layer-height-overhangs-impacts)

## Quick Reference[¶](layer-height.md#quick-reference) <a href="#quick-reference" id="quick-reference"></a>

| Nozzle Size | Min    | Max    | [First Layer Height](layer-height.md#first-layer-height) |
| ----------- | ------ | ------ | -------------------------------------------------------- |
| 0.2mm       | 0.04mm | 0.16mm | 0.12mm                                                   |
| 0.3mm       | 0.06mm | 0.24mm | 0.18mm                                                   |
| 0.4mm       | 0.08mm | 0.32mm | 0.25mm                                                   |
| 0.5mm       | 0.10mm | 0.40mm | 0.30mm                                                   |
| 0.6mm       | 0.12mm | 0.48mm | 0.35mm                                                   |
| 0.8mm       | 0.16mm | 0.64mm | 0.45mm                                                   |
| 1.0mm       | 0.20mm | 0.80mm | 0.55mm                                                   |

## Layer Height Guidelines[¶](layer-height.md#layer-height-guidelines) <a href="#layer-height-guidelines" id="layer-height-guidelines"></a>

Usually, the optimal range for layer height is between 20% and 80% of the nozzle diameter.

* **Below 20%:** Flow inconsistencies and "fish scale" patterns may occur, especially at high speeds.
* **Over 80%:** Increased risk of layer adhesion issues and reduced print quality.

## First Layer Height[¶](layer-height.md#first-layer-height) <a href="#first-layer-height" id="first-layer-height"></a>

Controls the thickness of the initial layer.\
A thicker first layer improves bed adhesion and compensates for build surface imperfections.

**Recommended:** 0.25mm for 0.4mm nozzle (62.5% of nozzle diameter)\
**Recommended maximum:** 65% of nozzle diameter

## Layer Height Overhangs Impacts[¶](layer-height.md#layer-height-overhangs-impacts) <a href="#layer-height-overhangs-impacts" id="layer-height-overhangs-impacts"></a>

Layer height directly affects [overhang angle](/broken/pages/21eba2f54a17a4877cb2b14599233756a824a377#maximum-angle) capability and quality.

![layer-height](https://www.orcaslicer.com/wiki/images/Precision/layer-height.svg?raw=true)

**Smaller layer heights** enable steeper overhangs by reducing the unsupported distance between layers, while **larger layer heights** increase this gap, leading to more sagging and requiring support material at shallower angles.
