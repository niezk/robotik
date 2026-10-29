# Bridging¶

"Bridging" is a 3D printing technique that allows you to print structures across gaps or voids without direct support underneath. OrcaSlicer provides several parameters to optimize bridge quality, minimizing filament sag and improving the appearance of top layers.

* [Flow ratio](bridging.md#flow-ratio)
* [Bridge density](bridging.md#bridge-density)
* [Thick bridges](bridging.md#thick-bridges)
* [Extra bridge layers](bridging.md#extra-bridge-layers)
* [Filter out small internal bridges](bridging.md#filter-out-small-internal-bridges)
* [Bridge Counterbore hole](bridging.md#bridge-counterbore-hole)

## Flow ratio[¶](bridging.md#flow-ratio) <a href="#flow-ratio" id="flow-ratio"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variables](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `bridge_flow`, `internal_bridge_flow`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--bridge-flow=1` (same pattern for the other variables above).\
This value governs the thickness of the bridge layer.

For external bridges, when material tends to sag, reducing the flow ratio can help improve appearance.\
For internal bridges, increasing the flow ratio can enhance strength and upper layer quality.

* Values above 1.0: Increase the amount of material while maintaining line spacing. This can improve line contact and strength.
* Values below 1.0: Reduce the amount of material while adjusting line spacing to maintain contact. This can reduce sagging.

The actual bridge flow used is calculated by multiplying this value with the [filament flow ratio](/broken/pages/4da0e8a2d1390e2f4166da4f6cca2f83837a3bb6#flow-ratio), and if set, the object's flow ratio.\
For internal bridges, the internal bridge flow ratio is also multiplied by the bridge flow ratio.

## Bridge density[¶](bridging.md#bridge-density) <a href="#bridge-density" id="bridge-density"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variables](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `bridge_density`, `internal_bridge_density`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Percentage`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--bridge-density=20%` (same pattern for the other variables above).\
Controls the density (spacing) of external and internal bridge lines. Default is 100%.\
Theoretically, 100% means a solid bridge, but due to the tendency of bridge extrusions to sag, 100% may not be sufficient.

* Higher than 100% density (**Recommended**, max 125%):
  * Pros: Produces smoother bridge surfaces, as overlapping lines provide additional support during printing.
  * Cons: Can cause overextrusion, decreasing lower and upper surface quality.
* Lower than 100% density (min 10%):
  * Pros: Can create a string-like first layer. Faster and with better cooling, as there is more space for air to circulate around the extruded bridge.
  * Cons: May lead to sagging and poor surface finish.

The density changes the spacing between bridge lines, not the [flow ratio](bridging.md#flow-ratio) of each line.

## Thick bridges[¶](bridging.md#thick-bridges) <a href="#thick-bridges" id="thick-bridges"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variables](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `thick_bridges`, `thick_internal_bridges`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--thick-bridges=1` (same pattern for the other variables above).

When enabled, bridge extrusion uses a line height equal to the nozzle diameter.\
![thick-bridges](<../../../.gitbook/assets/thick bridges.png>)\
This improves the strength and reliability of bridges, allowing you to span longer distances; however, it may produce a rougher surface finish.\
Disabling this option can improve bridge appearance, but it is recommended only for shorter spans or when using large nozzles.\
It's recommended to enable this option for internal bridges, as it increases their reliability when printed over sparse infill.

## Extra bridge layers[¶](bridging.md#extra-bridge-layers) <a href="#extra-bridge-layers" id="extra-bridge-layers"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `enable_extra_bridge_layer`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `Choice`.\
[Options](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `disabled, external_bridge_only, internal_bridge_only, apply_to_all`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--enable-extra-bridge-layer=disabled`.\
This option enables the generation of an extra bridge layer over bridges.

Extra bridge layers help improve bridge appearance and reliability, as the solid infill is better supported. This is especially useful in fast printers, where the bridge and solid infill speeds vary greatly. The extra bridge layer results in reduced pillowing on top surfaces, as well as reduced separation of the external bridge layer from its surrounding perimeters.

It is generally recommended to set this to at least **External bridge only**, unless specific issues with the sliced model are found.

**Options:**

* **Disabled** - does not generate second bridge layers. This is the default and is set for compatibility purposes.
* **External bridge only** - generates second bridge layers for external-facing bridges only. Please note that small bridges that are shorter or narrower than the set number of perimeters will be skipped as they would not benefit from a second bridge layer. If generated, the second bridge layer will be extruded parallel to the first bridge layer to reinforce the bridge strength.
* **Internal bridge only** - generates second bridge layers for internal bridges over sparse infill only. Please note that the internal bridges count towards the top shell layer count of your model. The second internal bridge layer will be extruded as close to perpendicular to the first as possible. If multiple regions in the same island, with varying bridge angles are present, the last region of that island will be selected as the angle reference.
* **Apply to all** - generates second bridge layers for both internal and external-facing bridges.

## Filter out small internal bridges[¶](bridging.md#filter-out-small-internal-bridges) <a href="#filter-out-small-internal-bridges" id="filter-out-small-internal-bridges"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `dont_filter_internal_bridges`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `Choice`.\
[Options](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `disabled, limited, nofilter`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--dont-filter-internal-bridges=disabled`.\
This option can help reduce pillowing on top surfaces in heavily slanted or curved models.

By default, small internal bridges are filtered out and the internal solid infill is printed directly over the sparse infill. This works well in most cases, speeding up printing without too much compromise on top surface quality.

However, in heavily slanted or curved models, especially where too low a sparse infill density is used, this may result in curling of the unsupported solid infill, causing pillowing.

Enabling limited filtering or no filtering will print an internal bridge layer over slightly unsupported internal solid infill. The options below control the sensitivity of the filtering, i.e. they control where internal bridges are created:

* **Filter:** enables this option. This is the default behavior and works well in most cases.
* **Limited filtering:** creates internal bridges on heavily slanted surfaces while avoiding unnecessary bridges. This works well for most difficult models.
* **No filtering:** creates internal bridges on every potential internal overhang. This option is useful for heavily slanted top surface models; however, in most cases, it creates too many unnecessary bridges.

## Bridge Counterbore hole[¶](bridging.md#bridge-counterbore-hole) <a href="#bridge-counterbore-hole" id="bridge-counterbore-hole"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `counterbore_hole_bridging`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `Choice`.\
[Options](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `none, partiallybridge, sacrificiallayer`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--counterbore-hole-bridging=none`.\
When printing counterbore holes, the unsupported area can lead to sagging or poor surface quality. Also, the perimeters of the counterbore hole may not be printed correctly, leading to gaps or weak points in the structure.

This option creates bridges for counterbore holes, allowing them to be printed without support.\
Available modes include:

* **None:** No bridge is created.\
  ![bridge-counterbore-none](<../../../.gitbook/assets/bridge counterbore none.png>)
* **Partially bridged:** Only a part of the unsupported area will be bridged, creating a supporting layer for the next layer.\
  ![bridge-counterbore-partially](<../../../.gitbook/assets/bridge counterbore partially.gif>)
* **Sacrificial layer:** A full sacrificial bridge layer is created. This will close the counterbore hole, allowing the next layer to be printed without sagging. The sacrificial layer must be broken through after printing.\
  ![bridge-counterbore-sacrificial](<../../../.gitbook/assets/bridge counterbore sacrificial.png>)
