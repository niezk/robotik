# Multimaterial Advanced¶

* [Interlocking Beam](multimaterial-advanced.md#interlocking-beam)
* [Toolchange Ordering](multimaterial-advanced.md#toolchange-ordering)
  * [Toolchange Order](multimaterial-advanced.md#toolchange-order)
* [Interface Shells](multimaterial-advanced.md#interface-shells)
* [Maximum Width of Segmented Region](multimaterial-advanced.md#maximum-width-of-segmented-region)
* [Interlocking depth of Segmented Region](multimaterial-advanced.md#interlocking-depth-of-segmented-region)
* [Interlocking Beam Width](multimaterial-advanced.md#interlocking-beam-width)
* [Interlocking Direction](multimaterial-advanced.md#interlocking-direction)
* [Interlocking Beam Layers](multimaterial-advanced.md#interlocking-beam-layers)
* [Interlocking Depth](multimaterial-advanced.md#interlocking-depth)
* [Interlocking Boundary Avoidance](multimaterial-advanced.md#interlocking-boundary-avoidance)

## Interlocking Beam[¶](multimaterial-advanced.md#interlocking-beam) <a href="#interlocking-beam" id="interlocking-beam"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `interlocking_beam`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--interlocking-beam=1`.\
Generates an interlocking beam structure at the locations where different filaments touch. This improves the adhesion between filaments, especially for models printed in different materials.

## Toolchange Ordering[¶](multimaterial-advanced.md#toolchange-ordering) <a href="#toolchange-ordering" id="toolchange-ordering"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `toolchange_ordering`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `Choice`.\
[Options](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `default, cyclic`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--toolchange-ordering=default`.

Important

NEW FEATURE: **Toolchange ordering**\
Available in: [Nightly builds](https://github.com/OrcaSlicer/OrcaSlicer/releases/tag/nightly-builds) or Releases greater than **2.4.2**.

Determines the order of tool changes on each layer:

* **Default:** starts with the last used extruder to minimize tool changes.
* **Cyclic:** uses a fixed tool sequence each layer. This sacrifices speed for better surface quality, as the extra tool changes allow layers more time to cool.

### Toolchange Order[¶](multimaterial-advanced.md#toolchange-order) <a href="#toolchange-order" id="toolchange-order"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Expert`.\
[Variables](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `toolchange_cyclic_order`, `toolchange_cyclic_first_layer`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb): `toolchange_cyclic_order` (Text), `toolchange_cyclic_first_layer` (Boolean).\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--toolchange-cyclic-order=value` (`toolchange_cyclic_order` shown; other variables above follow their own type).

Important

NEW FEATURE: **Custom cyclic toolchange sequence**\
Available in: [Nightly builds](https://github.com/OrcaSlicer/OrcaSlicer/releases/tag/nightly-builds) or Releases greater than **2.4.2**.

Only available when [Toolchange Ordering](multimaterial-advanced.md#toolchange-ordering) is set to `Cyclic`.

**Cyclic order** sets the filament sequence the cyclic ordering follows, written as filament numbers separated by commas (e.g. `3,2,1,4`). Each layer prints its filaments in that order, and filaments left out of the sequence are printed last, in ascending order. Leave it empty to cycle through all filaments in ascending order.

Entries that cannot be used are dropped and the rest of the sequence still applies:

* Numbers outside the range of your filaments, such as `0` or a number higher than your filament count.
* Repeated numbers, where only the first occurrence counts.
* Anything that is not a plain number, such as `abc` or `2x`.

**Apply cyclic order to first layer** extends that sequence to the first layer as well. It is disabled by default, because the first layer is instead ordered for the best bed adhesion: filaments that print small, fragile first-layer features are printed last, so the following tool changes and travel moves are less likely to knock those weakly anchored parts loose. This adhesion order also honors a custom first layer filament sequence when one is set. The cooling benefit of the cyclic order does not apply to the first layer anyway, since it is printed slowly and hot for adhesion.

Tip

Enable it only if you need the exact same tool sequence on every layer, including the first, at the cost of that adhesion optimization.

## Interface Shells[¶](multimaterial-advanced.md#interface-shells) <a href="#interface-shells" id="interface-shells"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `interface_shells`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--interface-shells=1`.\
Forces the generation of solid shells between adjacent materials/volumes. Useful for multi-extruder prints with translucent materials or manual soluble support material.

## Maximum Width of Segmented Region[¶](multimaterial-advanced.md#maximum-width-of-segmented-region) <a href="#maximum-width-of-segmented-region" id="maximum-width-of-segmented-region"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `mmu_segmented_region_max_width`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--mmu-segmented-region-max-width=1`.\
Maximum width of a segmented region. Zero disables this feature. Ignored when [Interlocking Beam](multimaterial-advanced.md#interlocking-beam) is enabled.

## Interlocking depth of Segmented Region[¶](multimaterial-advanced.md#interlocking-depth-of-segmented-region) <a href="#interlocking-depth-of-segmented-region" id="interlocking-depth-of-segmented-region"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `mmu_segmented_region_interlocking_depth`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--mmu-segmented-region-interlocking-depth=1`.\
Interlocking depth of a segmented region. On every other layer, the painted region reaches only this deep into the model instead of the [Maximum Width of Segmented Region](multimaterial-advanced.md#maximum-width-of-segmented-region), so consecutive layers interlock. Zero disables this feature. Hidden and ignored when [Interlocking Beam](multimaterial-advanced.md#interlocking-beam) is enabled.

## Interlocking Beam Width[¶](multimaterial-advanced.md#interlocking-beam-width) <a href="#interlocking-beam-width" id="interlocking-beam-width"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `interlocking_beam_width`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--interlocking-beam-width=1`.\
The width of the interlocking structure beams.

## Interlocking Direction[¶](multimaterial-advanced.md#interlocking-direction) <a href="#interlocking-direction" id="interlocking-direction"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `interlocking_orientation`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--interlocking-orientation=1`.\
Orientation of the interlocking beams.

## Interlocking Beam Layers[¶](multimaterial-advanced.md#interlocking-beam-layers) <a href="#interlocking-beam-layers" id="interlocking-beam-layers"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `interlocking_beam_layer_count`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Integer`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--interlocking-beam-layer-count=1`.\
The height of the beams of the interlocking structure, measured in number of layers. Fewer layers are stronger, but more prone to defects.

## Interlocking Depth[¶](multimaterial-advanced.md#interlocking-depth) <a href="#interlocking-depth" id="interlocking-depth"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `interlocking_depth`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Integer`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--interlocking-depth=1`.\
The distance from the boundary between filaments to generate interlocking structure, measured in cells. Too few cells will result in poor adhesion.

## Interlocking Boundary Avoidance[¶](multimaterial-advanced.md#interlocking-boundary-avoidance) <a href="#interlocking-boundary-avoidance" id="interlocking-boundary-avoidance"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `interlocking_boundary_avoidance`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Integer`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--interlocking-boundary-avoidance=1`.\
The distance from the outside of a model where interlocking structures will not be generated, measured in cells.
