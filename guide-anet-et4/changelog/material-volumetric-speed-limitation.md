# Material Volumetric Speed Limitation¶

Each material profile includes a **maximum volumetric speed** setting, which limits your [print speed](/broken/pages/e7564d8175752533bd6013e85bc33a5635aa36fb) to prevent issues like nozzle clogs, under-extrusion, or poor layer adhesion.

Tip

Calibrating the maximum volumetric speed for each filament you use is highly recommended. Refer to the [Max Volumetric Speed (FlowRate) Calibration](/broken/pages/3c98b517ea8b8a9c2acbf94db99cc63b9a9dd16e) guide for detailed instructions on how to perform this calibration.

## Adaptive volumetric speed[¶](material-volumetric-speed-limitation.md#adaptive-volumetric-speed) <a href="#adaptive-volumetric-speed" id="adaptive-volumetric-speed"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Developer`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `filament_adaptive_volumetric_speed`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Boolean list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--filament-adaptive-volumetric-speed=1`.

Warning

Experimental and incomplete feature imported from BBS.\
Functional for some profiles that already have the variable saved.

When enabled, the extrusion flow is limited by the smaller of the fitted value (calculated from line width and layer height) and the user-defined maximum flow. When disabled, only the user-defined maximum flow is applied.

## Max volumetric speed[¶](material-volumetric-speed-limitation.md#max-volumetric-speed) <a href="#max-volumetric-speed" id="max-volumetric-speed"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `filament_max_volumetric_speed`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--filament-max-volumetric-speed=1`.\
This setting is the volume of filament that can be melted and extruded per second. Printing speed is limited by max volumetric speed, in case of too high and unreasonable speed setting. This value cannot be zero.
