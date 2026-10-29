# Basic Extruder Information¶

This section contains the basic information about the extruder.\
When using multiple extruders, you can set different values for each extruder.

* [Nozzle diameter](basic-extruder-information.md#nozzle-diameter)
* [Nozzle volume](basic-extruder-information.md#nozzle-volume)
* [Extruder Layer Height Limits](basic-extruder-information.md#extruder-layer-height-limits)
* [Extruder printable area](basic-extruder-information.md#extruder-printable-area)
* [Extruder offset Position](basic-extruder-information.md#extruder-offset-position)

## Nozzle diameter[¶](basic-extruder-information.md#nozzle-diameter) <a href="#nozzle-diameter" id="nozzle-diameter"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `nozzle_diameter[extruder_idx]`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--nozzle-diameter=1`.\
The diameter of the nozzle for each extruder.

Tip

You can use different nozzle diameters for each extruder to achieve different print qualities and speeds.\
Follow the [Mixed Nozzle Sizes](/broken/pages/d8b1228608cc1b174a441c764cc6cf625c30317d) guide for more information on how to use this feature.

## Nozzle volume[¶](basic-extruder-information.md#nozzle-volume) <a href="#nozzle-volume" id="nozzle-volume"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `nozzle_volume[extruder_idx]`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--nozzle-volume=1`.\
Volume of nozzle between the filament cutter and the end of the nozzle

## Extruder Layer Height Limits[¶](basic-extruder-information.md#extruder-layer-height-limits) <a href="#extruder-layer-height-limits" id="extruder-layer-height-limits"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variables](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `extruder_printable_height[extruder_idx]`, `min_layer_height[extruder_idx]`, `max_layer_height[extruder_idx]`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--extruder-printable-height=1` (same pattern for the other variables above).\
Min and max layer height limits for the extruder. These settings are used when adaptive layer height is enabled.

## Extruder printable area[¶](basic-extruder-information.md#extruder-printable-area) <a href="#extruder-printable-area" id="extruder-printable-area"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `extruder_printable_area[extruder_idx]`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Point group list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--extruder-printable-area=value`.\
The area of the bed that each extruder can reach, on printers whose extruders can't all cover the whole bed. On the Bambu Lab H2D, for example, the left nozzle reaches X 0 to 325 mm and the right nozzle X 25 to 350 mm of the 350 mm wide bed, so a 25 mm strip on each side can only be printed by one nozzle.

Orca uses these areas to:

* Show the left and right nozzle-only areas on the plate.
* Warn before slicing when an object extends beyond the printable range of the nozzle that has to print one of its filaments.
* Keep a filament off an extruder that can't reach every part printed with it when filaments are grouped automatically.
* Clip the brim to the area of the extruder that prints it.
* Keep the prime tower inside the area that every extruder can reach.
* Report an error after slicing when a filament's G-code path leaves the printable range of its extruder.

When the profile leaves it empty, every extruder can reach the whole [printable area](/broken/pages/0d906d45479df31a3f89c370bdbfa417919f98de#printable-area-bed-shape).

This value comes from the printer profile and can't be edited. It is only shown for printers with two extruders.

## Extruder offset Position[¶](basic-extruder-information.md#extruder-offset-position) <a href="#extruder-offset-position" id="extruder-offset-position"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `extruder_offset[extruder_idx]`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Point list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--extruder-offset=100,100`.\
If your firmware doesn't handle the extruder displacement you need the G-code to take it into account. This option lets you specify the displacement of each extruder with respect to the first one. It expects positive coordinates (they will be subtracted from the XY coordinate).
