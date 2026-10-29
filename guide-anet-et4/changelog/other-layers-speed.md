# Other layers speed¶

## Speed limitations[¶](other-layers-speed.md#speed-limitations) <a href="#speed-limitations" id="speed-limitations"></a>

Important

Every speed setting is limited by several parameters like:

* [Maximum Volumetric Speed](/broken/pages/3c98b517ea8b8a9c2acbf94db99cc63b9a9dd16e)
* Machine / Motion ability
* [Acceleration](/broken/pages/8f016c37be2b0b663224cc06049d830a089c70e7)
* [Jerk settings](/broken/pages/7be52dd66f6f98ad86dab218c36e11ddebf56960)
* [Filament layer cooling time](/broken/pages/d7c372477cc904769ba325c42008522f74ffec75#slow-printing-down-for-better-layer-cooling)
* [Speed limitations](other-layers-speed.md#speed-limitations)
* [Outer wall](other-layers-speed.md#outer-wall)
* [Inner wall](other-layers-speed.md#inner-wall)
* [Small perimeters](other-layers-speed.md#small-perimeters)
  * [Small perimeters threshold](other-layers-speed.md#small-perimeters-threshold)
* [Sparse infill](other-layers-speed.md#sparse-infill)
* [Internal solid infill](other-layers-speed.md#internal-solid-infill)
* [Top surface](other-layers-speed.md#top-surface)
* [Gap infill](other-layers-speed.md#gap-infill)
* [Ironing speed](other-layers-speed.md#ironing-speed)
* [Support](other-layers-speed.md#support)
* [Support interface](other-layers-speed.md#support-interface)
* [Small tree support perimeters](other-layers-speed.md#small-tree-support-perimeters)
  * [Small tree support perimeters threshold](other-layers-speed.md#small-tree-support-perimeters-threshold)

## Outer wall[¶](other-layers-speed.md#outer-wall) <a href="#outer-wall" id="outer-wall"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `outer_wall_speed`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--outer-wall-speed=1`.\
Speed of the outer wall, which is the outermost, visible wall. It is usually printed slower than the [inner wall](other-layers-speed.md#inner-wall) to get better quality and good layer adhesion. This setting is also limited by [Machine / Motion ability / Resonance avoidance speed settings](/broken/pages/ccf0c15f3bed88abec16bacceff4810aac275310).\
It can be excluded from the [layer cooling slowdown](/broken/pages/d7c372477cc904769ba325c42008522f74ffec75#slow-printing-down-for-better-layer-cooling) with [Don't slow down outer walls](/broken/pages/d7c372477cc904769ba325c42008522f74ffec75#dont-slow-down-outer-walls).

## Inner wall[¶](other-layers-speed.md#inner-wall) <a href="#inner-wall" id="inner-wall"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `inner_wall_speed`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--inner-wall-speed=1`.\
Speed of the inner walls, which are printed faster than the outer wall to reduce print time. Their flow is still recommended to stay well below the [maximum volumetric speed](/broken/pages/3c98b517ea8b8a9c2acbf94db99cc63b9a9dd16e) to ensure good layer adhesion and reduce internal stresses in the material.

## Small perimeters[¶](other-layers-speed.md#small-perimeters) <a href="#small-perimeters" id="small-perimeters"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `small_perimeter_speed`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float or Percentage list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--small-perimeter-speed=20%`.\
Speed of walls with a theoretical radius <= [small perimeters threshold](other-layers-speed.md#small-perimeters-threshold). Any shape (not only circles) will be considered as a small perimeter.

If expressed as a percentage (for example: 80%), it will be calculated on the [outer wall speed](other-layers-speed.md#outer-wall).

Note

The default is 50% of the [outer wall speed](other-layers-speed.md#outer-wall).

### Small perimeters threshold[¶](other-layers-speed.md#small-perimeters-threshold) <a href="#small-perimeters-threshold" id="small-perimeters-threshold"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `small_perimeter_threshold`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--small-perimeter-threshold=1`.\
**Radius** in millimeters below which the speed of perimeters will be reduced to the [small perimeters speed](other-layers-speed.md#small-perimeters).\
A perimeter is considered small when:

Perimeter Length2π≤Threshold \frac{\text{Perimeter Length\}}{2\pi} \leq \text{Threshold}

For example, if the threshold is set to 5 mm, then the perimeter length must be less than or equal to 31.4 mm `(2 * π * 5 mm)` to be considered a small perimeter.

* A Circle with a diameter of 10 mm will have a perimeter length of approximately 31.4 mm, which is equal to the threshold, so it will be considered a small perimeter.
* A Cube of 10mm x 10mm will have a perimeter length of 40 mm, which is greater than the threshold, so it will not be considered a small perimeter.
* A Cube of 5mm x 5mm will have a perimeter length of 20 mm, which is less than the threshold, so it will be considered a small perimeter.

Note

Zero will disable [small perimeters speed](other-layers-speed.md#small-perimeters), and walls will use their regular speed, such as the [outer wall speed](other-layers-speed.md#outer-wall).

## Sparse infill[¶](other-layers-speed.md#sparse-infill) <a href="#sparse-infill" id="sparse-infill"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `sparse_infill_speed`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--sparse-infill-speed=1`.\
Speed of [sparse infill](/broken/pages/da1f51648c030aebc578bfec4de7c7b47ec7ddd2) which is printed faster than solid infill to reduce print time.\
If you are using your [Infill Pattern](/broken/pages/da1f51648c030aebc578bfec4de7c7b47ec7ddd2) as an aesthetic feature, you may want to set it closer to the [outer wall speed](other-layers-speed.md#outer-wall) to get better quality.

## Internal solid infill[¶](other-layers-speed.md#internal-solid-infill) <a href="#internal-solid-infill" id="internal-solid-infill"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `internal_solid_infill_speed`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--internal-solid-infill-speed=1`.\
Speed of internal solid infill, which fills the interior of the model with solid layers.\
This is typically set faster than the [top surface speed](other-layers-speed.md#top-surface) to optimize print time, while still ensuring adequate strength and layer adhesion. Adjusting this speed can help balance print quality and efficiency, especially for models requiring strong internal structures.\
Solid infill is also considered when [infill % is set to 100%](/broken/pages/da1f51648c030aebc578bfec4de7c7b47ec7ddd2#internal-solid-infill).

## Top surface[¶](other-layers-speed.md#top-surface) <a href="#top-surface" id="top-surface"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `top_surface_speed`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--top-surface-speed=1`.\
Speed of the [topmost solid layers](/broken/pages/a93444d6bc5d3f832eed7be5e316e5e8f71eee5d) of the print. This is usually set similar to the [outer wall speed](other-layers-speed.md#outer-wall) to achieve a smoother and higher-quality finish on visible surfaces. Lower speeds help minimize surface defects and improve the appearance of the final printed object.

## Gap infill[¶](other-layers-speed.md#gap-infill) <a href="#gap-infill" id="gap-infill"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `gap_infill_speed`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--gap-infill-speed=1`.\
Speed of [gap infill](/broken/pages/da1f51648c030aebc578bfec4de7c7b47ec7ddd2#apply-gap-fill), which is used to fill small gaps or holes in the print.

## Ironing speed[¶](other-layers-speed.md#ironing-speed) <a href="#ironing-speed" id="ironing-speed"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `ironing_speed`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--ironing-speed=1`.\
[Ironing](/broken/pages/773973b34ceefeb20e0955b2307ec254cf82ab14) and [Support Ironing](/broken/pages/0a96a23ec4091c1aefc9bca8a50840f599340f7a) speed, typically slower than the top surface speed to ensure a smooth finish.\
Each filament can replace this speed with its own Ironing speed in its [setting overrides](/broken/pages/81491811ca710a7d7f259cedc43d59f3fb1d8de0#ironing).

## Support[¶](other-layers-speed.md#support) <a href="#support" id="support"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `support_speed`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--support-speed=1`.\
Speed at which [support](/broken/pages/a5ac9e1d60ddd3e6c582c4a55c887162b3caeab4) material is printed. Slower speeds help ensure that supports are stable and effective during the print process.

## Support interface[¶](other-layers-speed.md#support-interface) <a href="#support-interface" id="support-interface"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `support_interface_speed`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--support-interface-speed=1`.\
Speed for the support interface layers, which are the layers directly contacting the model. This is usually set even slower than the main [support speed](other-layers-speed.md#support) to maximize surface quality where the support meets the model and to make support removal easier.

## Small tree support perimeters[¶](other-layers-speed.md#small-tree-support-perimeters) <a href="#small-tree-support-perimeters" id="small-tree-support-perimeters"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `small_support_perimeter_speed`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float or Percentage list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--small-support-perimeter-speed=20%`.

Important

NEW FEATURE: **Small tree support perimeters** (speed and threshold)\
Available in: [Nightly builds](https://github.com/OrcaSlicer/OrcaSlicer/releases/tag/nightly-builds) or Releases greater than **2.4.2**.

Same as [Small perimeters](other-layers-speed.md#small-perimeters), but for supports.\
This separate setting affects the speed of support extrusions whose length is within the [small support perimeters threshold](other-layers-speed.md#small-tree-support-perimeters-threshold).\
If expressed as a percentage (for example: 80%), it will be calculated on the [support](other-layers-speed.md#support) or [support interface](other-layers-speed.md#support-interface) speed.\
The default is 50% of the [support](other-layers-speed.md#support) or [support interface](other-layers-speed.md#support-interface) speed.

### Small tree support perimeters threshold[¶](other-layers-speed.md#small-tree-support-perimeters-threshold) <a href="#small-tree-support-perimeters-threshold" id="small-tree-support-perimeters-threshold"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `small_support_perimeter_threshold`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--small-support-perimeter-threshold=1`.\
Sets the threshold below which the [small support perimeters](other-layers-speed.md#small-tree-support-perimeters) speed is applied. Like the [small perimeters threshold](other-layers-speed.md#small-perimeters-threshold), it is a radius: a support extrusion is considered small when its length is <= 2π × threshold.\
The default threshold is 0 mm, which disables it.
