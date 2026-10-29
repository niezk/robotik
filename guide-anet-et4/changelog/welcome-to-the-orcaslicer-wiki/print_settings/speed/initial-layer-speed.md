# Initial layer speed¶

Printing the first layer slower than the rest of the print is a widely recommended practice. This helps ensure strong adhesion to the print bed, reduces the chances of warping or curling at the edges, and allows better compensation for minor leveling inconsistencies.

## Initial layer[¶](initial-layer-speed.md#initial-layer) <a href="#initial-layer" id="initial-layer"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `initial_layer_speed`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--initial-layer-speed=1`.\
This setting determines the printing speed of the [outer/inner walls](/broken/pages/9c18c604dcea802bce8c6264ba1f60829f4f8ed5) and the brim on the first layer.\
All other first layer extrusions, such as [solid infill](/broken/pages/a93444d6bc5d3f832eed7be5e316e5e8f71eee5d) and the [sparse infill](/broken/pages/da1f51648c030aebc578bfec4de7c7b47ec7ddd2) printed when [bottom layers](/broken/pages/a93444d6bc5d3f832eed7be5e316e5e8f71eee5d#shell-layers) is set to 0, use the [First layer infill](initial-layer-speed.md#initial-layer-infill) speed.\
Adjusting this speed helps ensure proper adhesion and print quality for the initial layer.

## Initial layer infill[¶](initial-layer-speed.md#initial-layer-infill) <a href="#initial-layer-infill" id="initial-layer-infill"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `initial_layer_infill_speed`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--initial-layer-infill-speed=1`.\
Defines the speed used for everything on the first layer except walls and brim, mainly the [solid infill](/broken/pages/a93444d6bc5d3f832eed7be5e316e5e8f71eee5d#shell-layers) regions. These areas require more precise and consistent extrusion to create a flat and stable surface for subsequent layers. Printing this section too fast may result in high internal stresses (increased risk of warping), poor layer uniformity, or adhesion failures.

## Initial layer travel speed[¶](initial-layer-speed.md#initial-layer-travel-speed) <a href="#initial-layer-travel-speed" id="initial-layer-travel-speed"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `initial_layer_travel_speed`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float or Percentage list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--initial-layer-travel-speed=20%`.\
Sets the travel (non-printing movement) speed for the first layer. This doesn't affect print quality and can be set as a percentage of the [travel speed](/broken/pages/2f5b1de38dab546988d4313298d94c3193f2f792).\
Usually, this is set to 100% of the [travel speed](/broken/pages/2f5b1de38dab546988d4313298d94c3193f2f792), but it can be reduced if you want to minimize vibrations or if your printer has issues with high-speed travel movements.

## Number of slow layers[¶](initial-layer-speed.md#number-of-slow-layers) <a href="#number-of-slow-layers" id="number-of-slow-layers"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `slow_down_layers`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Integer`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--slow-down-layers=1`.\
Specifies how many of the first layers should be printed at a reduced speed. Instead of jumping straight to full speed after the first layer, the speed gradually increases in a linear fashion over this number of layers. This gradual ramp-up helps maintain adhesion and gives the print more stability in its early stages, especially on prints with a small contact area or materials prone to warping.

![number-of-slow-layers](<../../../.gitbook/assets/number of slow layers.png>)
