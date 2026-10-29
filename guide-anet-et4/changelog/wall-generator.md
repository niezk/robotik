# Wall Generator¶

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `wall_generator`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `Choice`.\
[Options](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `classic, arachne`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--wall-generator=classic`.\
The Wall Generator defines how the outer and inner walls (perimeters) of the model are printed.

* [Classic](wall-generator.md#classic)
* [Arachne](wall-generator.md#arachne)
  * [Wall transitioning threshold angle](wall-generator.md#wall-transitioning-threshold-angle)
  * [Wall transitioning filter margin](wall-generator.md#wall-transitioning-filter-margin)
  * [Wall transitioning length](wall-generator.md#wall-transitioning-length)
  * [Wall distribution count](wall-generator.md#wall-distribution-count)
  * [Minimum wall width](wall-generator.md#minimum-wall-width)
    * [First layer minimum wall width](wall-generator.md#first-layer-minimum-wall-width)
  * [Minimum feature size](wall-generator.md#minimum-feature-size)
  * [Minimum wall length](wall-generator.md#minimum-wall-length)
  * [Maximum wall resolution](wall-generator.md#maximum-wall-resolution)
  * [Maximum wall deviation](wall-generator.md#maximum-wall-deviation)

## Classic[¶](wall-generator.md#classic) <a href="#classic" id="classic"></a>

The Classic wall generator is a simple and reliable method used in many slicers. It creates as many walls as possible (limited by [Wall Loops](/broken/pages/9c18c604dcea802bce8c6264ba1f60829f4f8ed5#wall-loops)) by extruding along the model’s perimeter using the defined [Line Width](/broken/pages/071d8306b1e38aa4aa5bb68076bb78ad0e540b0f). This method does not vary extrusion width and is ideal for fast, predictable slicing.

![wallgenerator-classic](<.gitbook/assets/wallgenerator classic.png>)

## Arachne[¶](wall-generator.md#arachne) <a href="#arachne" id="arachne"></a>

The Arachne wall generator dynamically adjusts extrusion width to follow the shape of the model more closely. This allows better handling of thin features and smooth transitions between wall counts.

![wallgenerator-arachne](<.gitbook/assets/wallgenerator arachne.png>)

Note

[A Framework for Adaptive Width Control of Dense Contour-Parallel Toolpaths in Fused Deposition Modeling](https://www.sciencedirect.com/science/article/pii/S0010448520301007?via%3Dihub)

### Wall transitioning threshold angle[¶](wall-generator.md#wall-transitioning-threshold-angle) <a href="#wall-transitioning-threshold-angle" id="wall-transitioning-threshold-angle"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `wall_transition_angle`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--wall-transition-angle=1`.\
Defines the maximum wedge angle (in degrees) at which the algorithm creates a transition between an even and odd number of walls. If a wedge shape exceeds this angle, no extra center wall will be added. Lowering this value reduces the number and length of center walls but may leave gaps or over-extrude.

### Wall transitioning filter margin[¶](wall-generator.md#wall-transitioning-filter-margin) <a href="#wall-transitioning-filter-margin" id="wall-transitioning-filter-margin"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `wall_transition_filter_deviation`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Percentage`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--wall-transition-filter-deviation=20%`.\
Prevents rapid switching between more or fewer walls by defining a tolerance range around the minimum wall width. The extrusion width will stay within the range:

\[Minimum Wall Width−Margin, 2×Minimum Wall Width+Margin] \left\[ \text{Minimum Wall Width} - \text{Margin},\ 2 \times \text{Minimum Wall Width} + \text{Margin} \right]

Higher values reduce transitions, travel moves, and extrusion starts/stops, but may increase extrusion variability and introduce print quality issues. Expressed as a percentage of nozzle diameter.

### Wall transitioning length[¶](wall-generator.md#wall-transitioning-length) <a href="#wall-transitioning-length" id="wall-transitioning-length"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `wall_transition_length`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Percentage`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--wall-transition-length=20%`.\
When the number of walls changes as the part becomes thinner, this sets the length allotted to split or join the wall segments. Expressed as a percentage of nozzle diameter.

### Wall distribution count[¶](wall-generator.md#wall-distribution-count) <a href="#wall-distribution-count" id="wall-distribution-count"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `wall_distribution_count`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Integer`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--wall-distribution-count=1`.\
Sets how many walls (counted from the center) the width variation is spread over. Lower values constrain variation to the innermost walls, keeping outer walls consistent for best surface quality.

### Minimum wall width[¶](wall-generator.md#minimum-wall-width) <a href="#minimum-wall-width" id="minimum-wall-width"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `min_bead_width`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Percentage`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--min-bead-width=20%`.\
Defines the width of the wall that replaces thin features (those above the [Minimum feature size](wall-generator.md#minimum-feature-size)). If the feature is thicker than this value, the wall will match its width. Expressed as a percentage of nozzle diameter.

#### First layer minimum wall width[¶](wall-generator.md#first-layer-minimum-wall-width) <a href="#first-layer-minimum-wall-width" id="first-layer-minimum-wall-width"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `initial_layer_min_bead_width`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Percentage`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--initial-layer-min-bead-width=20%`.\
Specifies the minimum wall width for the first layer. It is recommended to match the nozzle diameter to improve adhesion and ensure stable base walls.

### Minimum feature size[¶](wall-generator.md#minimum-feature-size) <a href="#minimum-feature-size" id="minimum-feature-size"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `min_feature_size`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Percentage`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--min-feature-size=20%`.\
Minimum width required for a model feature to be printed. Features below this value are skipped; features above it but thinner than the [Minimum Wall Width](wall-generator.md#minimum-wall-width) are widened to match it. Expressed as a percentage of nozzle diameter.

### Minimum wall length[¶](wall-generator.md#minimum-wall-length) <a href="#minimum-wall-length" id="minimum-wall-length"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `min_length_factor`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--min-length-factor=1`.\
Avoids very short or isolated wall segments that add unnecessary time.\
Increasing this value removes short unconnected walls, **improving efficiency**.

Note

Top and bottom surfaces are not affected by this setting to avoid visual artifacts. Use the [One wall threshold](/broken/pages/8737adce37259a727713a40d86d1257eda155156#threshold) to adjust how aggressively OrcaSlicer considers a region a top surface. That option only appears when this setting exceeds 0.5, or if single-wall top surfaces are enabled.

### Maximum wall resolution[¶](wall-generator.md#maximum-wall-resolution) <a href="#maximum-wall-resolution" id="maximum-wall-resolution"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Expert`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `wall_maximum_resolution`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--wall-maximum-resolution=1`.\
Controls the smallest wall segment length (in mm) that Arachne keeps during wall path simplification. Lower values preserve more small segments and curved detail, which can improve surface quality, but increase G-code size and motion complexity. Higher values simplify paths more aggressively, producing cleaner and smaller G-code at the cost of geometric fidelity.

### Maximum wall deviation[¶](wall-generator.md#maximum-wall-deviation) <a href="#maximum-wall-deviation" id="maximum-wall-deviation"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Expert`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `wall_maximum_deviation`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--wall-maximum-deviation=1`.\
Defines the maximum allowed geometric error (in mm) when simplifying wall paths. Increasing this value allows stronger simplification (smaller G-code and fewer tiny moves), but can reduce wall accuracy. Decreasing this value keeps walls closer to the original geometry, but retains more segments. If this setting conflicts with [Maximum wall resolution](wall-generator.md#maximum-wall-resolution), this deviation limit takes precedence.
