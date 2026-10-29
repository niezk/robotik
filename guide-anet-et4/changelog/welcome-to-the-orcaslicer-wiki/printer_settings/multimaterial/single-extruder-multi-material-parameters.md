# Single Extruder Multi-Material Parameters¶

This section describes the parameters specific to single extruder multi-material (SEMM) printing.

## Cooling tube position[¶](single-extruder-multi-material-parameters.md#cooling-tube-position) <a href="#cooling-tube-position" id="cooling-tube-position"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `cooling_tube_retraction`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--cooling-tube-retraction=1`.\
Distance of the center-point of the cooling tube from the extruder tip.

## Cooling tube length[¶](single-extruder-multi-material-parameters.md#cooling-tube-length) <a href="#cooling-tube-length" id="cooling-tube-length"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `cooling_tube_length`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--cooling-tube-length=1`.\
Length of the cooling tube to limit space for cooling moves inside it.

## Filament parking position[¶](single-extruder-multi-material-parameters.md#filament-parking-position) <a href="#filament-parking-position" id="filament-parking-position"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `parking_pos_retraction`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--parking-pos-retraction=1`.\
Distance of the extruder tip from the position where the filament is parked when unloaded. This should match the value in printer firmware.

## Extra loading distance[¶](single-extruder-multi-material-parameters.md#extra-loading-distance) <a href="#extra-loading-distance" id="extra-loading-distance"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `extra_loading_move`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--extra-loading-move=1`.\
When set to zero, the distance the filament is moved from parking position during load is exactly the same as it was moved back during unload. When positive, it is loaded further, if negative, the loading move is shorter than unloading.

## High extruder current on filament swap[¶](single-extruder-multi-material-parameters.md#high-extruder-current-on-filament-swap) <a href="#high-extruder-current-on-filament-swap" id="high-extruder-current-on-filament-swap"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `high_current_on_filament_swap`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--high-current-on-filament-swap=1`.\
It may be beneficial to increase the extruder motor current during the filament exchange sequence to allow for rapid ramming feed rates and to overcome resistance when loading a filament with an ugly shaped tip.
