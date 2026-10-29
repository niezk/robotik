# Acceleration¶

Acceleration in 3D printing is usually set in the printer's firmware.\
These settings override the firmware acceleration when the [normal printing acceleration](acceleration.md#normal-printing) is greater than 0.\
Orca limits the acceleration so it doesn't exceed the maximum set in the printer's Motion Ability settings.

* [Normal printing](acceleration.md#normal-printing)
* [Outer wall](acceleration.md#outer-wall)
* [Inner wall](acceleration.md#inner-wall)
* [Bridge](acceleration.md#bridge)
* [Sparse infill](acceleration.md#sparse-infill)
* [Internal solid infill](acceleration.md#internal-solid-infill)
* [Initial layer](acceleration.md#initial-layer)
* [Initial layer travel](acceleration.md#initial-layer-travel)
* [Top surface](acceleration.md#top-surface)
* [Travel](acceleration.md#travel)
* [Enable accel to decel](acceleration.md#enable-accel-to-decel)
  * [Accel to decel](acceleration.md#accel-to-decel)

## Normal printing[¶](acceleration.md#normal-printing) <a href="#normal-printing" id="normal-printing"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `default_acceleration`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--default-acceleration=1`.\
The default acceleration for both normal printing and travel after the first layer.

Note

If this value is set to 0, Orca doesn't send acceleration commands, so the printer's own acceleration is used and the other acceleration settings are disabled.

## Outer wall[¶](acceleration.md#outer-wall) <a href="#outer-wall" id="outer-wall"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `outer_wall_acceleration`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--outer-wall-acceleration=1`.\
Acceleration for [outer wall](/broken/pages/e7564d8175752533bd6013e85bc33a5635aa36fb#outer-wall) printing. This is usually set to a lower value than normal printing to ensure better quality.

## Inner wall[¶](acceleration.md#inner-wall) <a href="#inner-wall" id="inner-wall"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `inner_wall_acceleration`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--inner-wall-acceleration=1`.\
Acceleration for [inner wall](/broken/pages/e7564d8175752533bd6013e85bc33a5635aa36fb#inner-wall) printing. This is usually set to a higher value than outer wall printing to improve speed.

## Bridge[¶](acceleration.md#bridge) <a href="#bridge" id="bridge"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `bridge_acceleration`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float or Percentage list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--bridge-acceleration=20%`.\
Acceleration of [bridges](/broken/pages/17606932e85b0df52609804927852a6cae28fceb#bridge-speed). If the value is expressed as a percentage (e.g. 50%), it will be calculated based on the outer wall acceleration.

## Sparse infill[¶](acceleration.md#sparse-infill) <a href="#sparse-infill" id="sparse-infill"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `sparse_infill_acceleration`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float or Percentage list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--sparse-infill-acceleration=20%`.\
Acceleration of [sparse infill](/broken/pages/e7564d8175752533bd6013e85bc33a5635aa36fb#sparse-infill). If the value is expressed as a percentage (e.g. 100%), it will be calculated based on the default acceleration.

## Internal solid infill[¶](acceleration.md#internal-solid-infill) <a href="#internal-solid-infill" id="internal-solid-infill"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `internal_solid_infill_acceleration`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float or Percentage list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--internal-solid-infill-acceleration=20%`.\
Acceleration of [internal solid infill](/broken/pages/e7564d8175752533bd6013e85bc33a5635aa36fb#internal-solid-infill). If the value is expressed as a percentage (e.g. 100%), it will be calculated based on the default acceleration.

## Initial layer[¶](acceleration.md#initial-layer) <a href="#initial-layer" id="initial-layer"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `initial_layer_acceleration`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--initial-layer-acceleration=1`.\
Acceleration of [initial layer](/broken/pages/1902fd5fb4f97cd776e6116015b89995974ec588). Using a lower value can improve build plate adhesion.

## Initial layer travel[¶](acceleration.md#initial-layer-travel) <a href="#initial-layer-travel" id="initial-layer-travel"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `initial_layer_travel_acceleration`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float or Percentage list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--initial-layer-travel-acceleration=20%`.\
Acceleration of [initial layer travel](/broken/pages/1902fd5fb4f97cd776e6116015b89995974ec588#initial-layer-travel-speed). Using a lower value can improve build plate adhesion. If the value is expressed as a percentage (e.g. 50%), it will be calculated based on the [Travel Acceleration](acceleration.md#travel).

## Top surface[¶](acceleration.md#top-surface) <a href="#top-surface" id="top-surface"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `top_surface_acceleration`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--top-surface-acceleration=1`.\
Acceleration of [top surface infill](/broken/pages/e7564d8175752533bd6013e85bc33a5635aa36fb#top-surface). Using a lower value may improve top surface quality.\
A value similar to the [outer wall acceleration](acceleration.md#outer-wall) is recommended.

## Travel[¶](acceleration.md#travel) <a href="#travel" id="travel"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `travel_acceleration`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--travel-acceleration=1`.\
Acceleration of [travel](/broken/pages/2f5b1de38dab546988d4313298d94c3193f2f792) moves. This is usually set to a higher value than normal printing to reduce travel time.

## Enable accel to decel[¶](acceleration.md#enable-accel-to-decel) <a href="#enable-accel-to-decel" id="enable-accel-to-decel"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `accel_to_decel_enable`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--accel-to-decel-enable=1`.\
Adjusts Klipper's `max_accel_to_decel` automatically. Each time Orca sets the acceleration with `SET_VELOCITY_LIMIT ACCEL=`, it adds `ACCEL_TO_DECEL=` at the [accel to decel](acceleration.md#accel-to-decel) percentage of that acceleration. When disabled, `ACCEL_TO_DECEL` is not sent.\
This option is only shown when the [G-code flavor](/broken/pages/eeff389a3bf7caa2aee6f13fbffe1d91ee4800d4#g-code-flavor) is Klipper, and it is enabled by default.

### Accel to decel[¶](acceleration.md#accel-to-decel) <a href="#accel-to-decel" id="accel-to-decel"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `accel_to_decel_factor`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Percentage`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--accel-to-decel-factor=20%`.\
Percentage of the acceleration that Klipper's `max_accel_to_decel` is set to, from 1% to 100% (default 50%).\
For example, at 5000 mm/s² and 50%, Orca sends `SET_VELOCITY_LIMIT ACCEL=5000 ACCEL_TO_DECEL=2500`.\
It can only be edited when [Enable accel to decel](acceleration.md#enable-accel-to-decel) is checked.
