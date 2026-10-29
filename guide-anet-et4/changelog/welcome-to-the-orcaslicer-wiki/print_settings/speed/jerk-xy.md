# Jerk XY¶

In printer firmware, **Jerk** is the maximum speed change (in mm/s) the printer can make instantly, without accelerating. It controls direction changes and velocity transitions during movement.

* [Key Effects](jerk-xy.md#key-effects)
* [Cornering Control Types](jerk-xy.md#cornering-control-types)
  * [Junction Deviation](jerk-xy.md#junction-deviation)
* [Default](jerk-xy.md#default)
  * [Outer wall](jerk-xy.md#outer-wall)
  * [Inner wall](jerk-xy.md#inner-wall)
  * [Infill](jerk-xy.md#infill)
  * [Top surface](jerk-xy.md#top-surface)
  * [Initial layer](jerk-xy.md#initial-layer)
  * [Initial layer travel](jerk-xy.md#initial-layer-travel)
  * [Travel](jerk-xy.md#travel)
* [Useful links](jerk-xy.md#useful-links)

## Key Effects[¶](jerk-xy.md#key-effects) <a href="#key-effects" id="key-effects"></a>

* **Corner Control**:
  * Lower values = smoother corners, better quality.
  * Higher values = faster cornering, potential artifacts.
* **Print Speed**: Higher jerk reduces deceleration at direction changes, increasing overall speed.
* **Surface Quality**: Lower jerk minimizes vibrations and ringing, especially important for outer walls.

This setting overrides firmware jerk values when different motion types need specific settings. Orca limits jerk to not exceed the Printer's Motion Ability settings.

Tip

Jerk can work in conjunction with [Pressure Advance](/broken/pages/98e0a11e8871bb509a2675168d1a37d297df9e2e), [Adaptive Pressure Advance](/broken/pages/4f66a6f5693b4bfc0e71b9323776541409376697), and [Input Shaping](/broken/pages/7c942f82d3b10b8ff692dcce023e796cd63e4900) to optimize print quality and speed.\
It's recommended to follow the [calibration guide](/broken/pages/11c07341f1c2537a4800ccab7e8c9c26d87a5246) order for best results.

## Cornering Control Types[¶](jerk-xy.md#cornering-control-types) <a href="#cornering-control-types" id="cornering-control-types"></a>

* **Jerk**: Traditional method, sets a maximum speed for direction changes.
  * Klipper: [Square corner velocity](https://www.klipper3d.org/Config_Reference.html#printer)
  * RepRapFirmware: [Maximum instantaneous speed changes](https://docs.duet3d.com/User_manual/Reference/Gcodes#m566-set-allowable-instantaneous-speed-change)
  * Marlin 2: [Classic Jerk](https://marlinfw.org/docs/configuration/configuration.html#jerk-) (deprecated in favor of [Junction Deviation](https://marlinfw.org/docs/configuration/configuration.html#junction-deviation-), but can still be used).
  * Marlin Legacy: [Classic Jerk](https://marlinfw.org/docs/configuration/configuration.html#jerk-).
* [**Junction Deviation**](jerk-xy.md#junction-deviation): Modern method, calculates cornering speed based on acceleration.

Tip

Calibrate your cornering values using the [Cornering Calibration guide](/broken/pages/32e75ac81b67ea0e27c86dc13e73b020011ed424).

### Junction Deviation[¶](jerk-xy.md#junction-deviation) <a href="#junction-deviation" id="junction-deviation"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `default_junction_deviation`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--default-junction-deviation=1`.\
Alternative to Jerk, Junction Deviation is the default method for controlling cornering speed in Marlin 2 printers.\
Instead of setting a cornering speed for each line type, it calculates the cornering speed from [each line's acceleration](/broken/pages/8f016c37be2b0b663224cc06049d830a089c70e7) and the corner angle. A Junction Deviation equivalent to a given jerk value can be estimated with the formula:

JD=0.4⋅Jerk2Accel. JD = 0.4 \cdot \frac{\text{Jerk}^2}{\text{Accel.\}}

Higher values result in faster and more aggressive cornering speeds, while lower values produce smoother, more controlled cornering.

Note

Classic Jerk can still be used in Marlin 2, but it is deprecated in favor of Junction Deviation.\
If your printer uses Classic Jerk, set [Maximum Junction Deviation](/broken/pages/053648f94ba5f635d165734b67c47d50256deed6#maximum-junction-deviation) to `0` in the printer settings to enable the Jerk settings.

This value is limited by [Printer settings > Motion ability > Maximum Junction Deviation](/broken/pages/053648f94ba5f635d165734b67c47d50256deed6#maximum-junction-deviation).

## Default[¶](jerk-xy.md#default) <a href="#default" id="default"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `default_jerk`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--default-jerk=1`.\
Default Jerk value.

Note

If this value is set to 0, the jerk will be set to the printer's default jerk.

### Outer wall[¶](jerk-xy.md#outer-wall) <a href="#outer-wall" id="outer-wall"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `outer_wall_jerk`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--outer-wall-jerk=1`.\
Jerk for outer wall printing. This is usually set to a lower value than normal printing to ensure better quality.

### Inner wall[¶](jerk-xy.md#inner-wall) <a href="#inner-wall" id="inner-wall"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `inner_wall_jerk`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--inner-wall-jerk=1`.\
Jerk for inner wall printing. This is usually set to a moderately higher value than outer wall jerk to improve speed.

### Infill[¶](jerk-xy.md#infill) <a href="#infill" id="infill"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `infill_jerk`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--infill-jerk=1`.\
Jerk for infill printing. This is usually set to a value higher than inner wall printing to improve speed.

### Top surface[¶](jerk-xy.md#top-surface) <a href="#top-surface" id="top-surface"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `top_surface_jerk`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--top-surface-jerk=1`.\
Jerk for top surface printing. This is usually set to a lower value than infill to ensure better quality.

### Initial layer[¶](jerk-xy.md#initial-layer) <a href="#initial-layer" id="initial-layer"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `initial_layer_jerk`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--initial-layer-jerk=1`.\
Jerk for initial layer printing. This is usually set to a lower value than top surface to improve adhesion.

### Initial layer travel[¶](jerk-xy.md#initial-layer-travel) <a href="#initial-layer-travel" id="initial-layer-travel"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `initial_layer_travel_jerk`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float or Percentage list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--initial-layer-travel-jerk=20%`.\
Jerk for initial layer travel. Using a lower value can improve build plate adhesion. If the value is expressed as a percentage (e.g. 50%), it will be calculated based on the [Travel Jerk](jerk-xy.md#travel).

### Travel[¶](jerk-xy.md#travel) <a href="#travel" id="travel"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `travel_jerk`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--travel-jerk=1`.\
Jerk for travel moves. This is usually set to a higher value than infill to reduce travel time.

## Useful links[¶](jerk-xy.md#useful-links) <a href="#useful-links" id="useful-links"></a>

* [Klipper Kinematics](https://www.klipper3d.org/Kinematics.html?h=accelerat#acceleration)
* [Marlin Junction Deviation](https://marlinfw.org/docs/configuration/configuration.html#junction-deviation-)
* [JD Explained and Visualized, by Paul Wanamaker](https://reprap.org/forum/read.php?1,739819)
* [Computing JD for Marlin Firmware](https://blog.kyneticcnc.com/2018/10/computing-junction-deviation-for-marlin.html)
* [Improving GRBL: Cornering Algorithm](https://onehossshay.wordpress.com/2011/09/24/improving_grbl_cornering_algorithm/)
* [Pressure Advance Calibration](/broken/pages/98e0a11e8871bb509a2675168d1a37d297df9e2e)
* [Adaptive Pressure Advance](/broken/pages/4f66a6f5693b4bfc0e71b9323776541409376697)
