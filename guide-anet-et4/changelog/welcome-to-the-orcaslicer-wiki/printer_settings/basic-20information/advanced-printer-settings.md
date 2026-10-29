# Advanced Printer Settings¶

Advanced settings related to the printer configuration.

* [Printer structure](advanced-printer-settings.md#printer-structure)
* [G-code flavor](advanced-printer-settings.md#g-code-flavor)
* [Skip G-code config block](advanced-printer-settings.md#skip-g-code-config-block)
* [Pellet Modded Printer](advanced-printer-settings.md#pellet-modded-printer)
* [Use 3rd-party print host](advanced-printer-settings.md#use-3rd-party-print-host)
* [Printer Agent](advanced-printer-settings.md#printer-agent)
* [Scan first layer](advanced-printer-settings.md#scan-first-layer)
* [Power Loss Recovery](advanced-printer-settings.md#power-loss-recovery)
* [Disable set remaining print time](advanced-printer-settings.md#disable-set-remaining-print-time)
* [G-code thumbnails](advanced-printer-settings.md#g-code-thumbnails)
* [Use relative E distances](advanced-printer-settings.md#use-relative-e-distances)
* [Use firmware retraction](advanced-printer-settings.md#use-firmware-retraction)
* [Bed temperature type](advanced-printer-settings.md#bed-temperature-type)
* [Time cost](advanced-printer-settings.md#time-cost)
* [Build plate tilt](advanced-printer-settings.md#build-plate-tilt)

## Printer structure[¶](advanced-printer-settings.md#printer-structure) <a href="#printer-structure" id="printer-structure"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Developer`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `printer_structure`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `Choice`.\
[Options](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `undefine, corexy, i3, hbot, delta`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--printer-structure=undefine`.\
The physical arrangement and components of a printing device.

## G-code flavor[¶](advanced-printer-settings.md#g-code-flavor) <a href="#g-code-flavor" id="g-code-flavor"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `gcode_flavor`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `Choice`.\
[Options](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `marlin, klipper, reprapfirmware, repetier, marlin2`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--gcode-flavor=marlin`.\
What kind of G-code the printer is compatible with.

## Skip G-code config block[¶](advanced-printer-settings.md#skip-g-code-config-block) <a href="#skip-g-code-config-block" id="skip-g-code-config-block"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `gcode_skip_config_block`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--gcode-skip-config-block=1`.

Important

NEW FEATURE: **Skip G-code config block**\
Available in: [Nightly builds](https://github.com/OrcaSlicer/OrcaSlicer/releases/tag/nightly-builds) or Releases greater than **2.4.2**.

Removes the `CONFIG_BLOCK` (the commented-out block listing every resolved slicer setting) from the exported G-code file.

Some printer firmware parsers crash when reading certain lines in this block, most notably Anycubic's go-klipper choking on `; filament_colour_type = 1;1;1;1`. Enabling this option avoids those upload/parsing failures by not writing the block at all.

Caution

The G-code file will no longer contain the resolved slicer settings, so it can no longer be used to recover the print configuration afterward.

## Pellet Modded Printer[¶](advanced-printer-settings.md#pellet-modded-printer) <a href="#pellet-modded-printer" id="pellet-modded-printer"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Simple`.\
[Variables](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `pellet_flow_coefficient`, `pellet_modded_printer`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb): `pellet_flow_coefficient` (Float list), `pellet_modded_printer` (Boolean).\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--pellet-flow-coefficient=1` (`pellet_flow_coefficient` shown; other variables above follow their own type).\
Enable this option if your printer uses pellets instead of filaments. Large format printers with print volumes in the order of 1m^3 generally use pellets for printing. The overall tech is very similar to FDM printing. It is FDM printing, but instead of filaments, it uses pellets.

The difference here is that where filaments have a filament\_diameter that is used to calculate the volume of filament ingested, pellets have a particular flow\_coefficient that is empirically devised for that particular pellet.

pellet\_flow\_coefficient is basically a measure of the packing density of a particular pellet. Shape, material and density of an individual pellet will determine the packing density and the only thing that matters for 3d printing is how much of that pellet material is extruded by one turn of whatever feeding mehcanism/gear your printer uses. You can emperically derive that for your own pellets for a particular printer model.

We are translating the pellet\_flow\_coefficient into filament\_diameter so that everything works just like it does already with very minor adjustments.

filament\_diameter=4pellet\_flow\_coefficient⋅π \text{filament\\\_diameter} = \sqrt{\frac{4}{\text{pellet\\\_flow\\\_coefficient} \cdot \pi\}}

sqrt just makes the relationship between flow\_coefficient and volume linear.

Higher packing density -> more material extruded by single turn -> higher pellet\_flow\_coefficient -> treated as if a filament of larger diameter is being used. All other calculations remain the same for slicing.

## Use 3rd-party print host[¶](advanced-printer-settings.md#use-3rd-party-print-host) <a href="#use-3rd-party-print-host" id="use-3rd-party-print-host"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `bbl_use_printhost`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
Not available via CLI — see [Setting Overrides](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides) for the full list of excluded keys.\
Allow controlling BambuLab's printer through 3rd party print hosts.

## Printer Agent[¶](advanced-printer-settings.md#printer-agent) <a href="#printer-agent" id="printer-agent"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `printer_agent`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#text): `Text` (shown as a dropdown of registered agents).\
Not available via CLI — see [Setting Overrides](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides) for the full list of excluded keys.\
Select the network agent implementation used to communicate with the printer. The list contains the built-in agents plus any agents registered by loaded [printer agent plugins](/broken/pages/15a2ad303eaf34d70c221d8da6194257a61edc58). When empty, Bambu Lab printers use `bbl` and all other printers use `orca`.

Note

Plugin printer agents only receive print jobs when **Preferences → Developer → Experimental Features → Use printer agents instead of print hosts** is enabled.

## Scan first layer[¶](advanced-printer-settings.md#scan-first-layer) <a href="#scan-first-layer" id="scan-first-layer"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `scan_first_layer`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--scan-first-layer=1`.\
Enable this to enable the camera on printer to check the quality of first layer.

## Power Loss Recovery[¶](advanced-printer-settings.md#power-loss-recovery) <a href="#power-loss-recovery" id="power-loss-recovery"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `enable_power_loss_recovery`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `Choice`.\
[Options](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `printer_configuration, enable, disable`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--enable-power-loss-recovery=printer_configuration`.\
Enable or Disable power loss recovery by inserting commands in generated G-code.\
Set `Printer configuration` to use the current printer's power loss recovery configuration.

Note

Only for [Bambu Lab](https://wiki.bambulab.com/en/knowledge-sharing/power-loss-recovery) or [Marlin 2 firmware](https://marlinfw.org/docs/gcode/M413.html) based printers.

Power loss recovery saves the current execution point to non-volatile memory (SD card) but this can introduce some issues:

* When the slicer generates many short moves (e.g. curves), frequent save/read operations can introduce pauses that may leave blobs.
* Repeated writes also increase wear on the memory device and its Terabytes Written (TBW).

Tip

If enabled, it's recommended to enable [Arc fitting](/broken/pages/c70b83c3a32422c9168494b30baab0b5314ff4ad#arc-fitting) in `Quality Settings > Precision` to reduce the number of G-code commands.

Caution

High warping models or materials will not be recovered properly due to bed adhesion loss after power-off.

## Disable set remaining print time[¶](advanced-printer-settings.md#disable-set-remaining-print-time) <a href="#disable-set-remaining-print-time" id="disable-set-remaining-print-time"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `disable_m73`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--disable-m73=1`.\
Disable generating of the M73: Set remaining print time in the final G-code.

## G-code thumbnails[¶](advanced-printer-settings.md#g-code-thumbnails) <a href="#g-code-thumbnails" id="g-code-thumbnails"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `thumbnails`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#text): `Text`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--thumbnails=48x48/PNG,300x300/PNG`.\
Picture sizes to be stored into a .gcode and .sl1 / .sl1s files, in the following format: "XxY, XxY, ..."

## Use relative E distances[¶](advanced-printer-settings.md#use-relative-e-distances) <a href="#use-relative-e-distances" id="use-relative-e-distances"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `use_relative_e_distances`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--use-relative-e-distances=1`.\
Relative extrusion is recommended when using "label\_objects" option. Some extruders work better with this option unchecked (absolute extrusion mode). Wipe tower is only compatible with relative mode. It is recommended on most printers. Default is checked.

## Use firmware retraction[¶](advanced-printer-settings.md#use-firmware-retraction) <a href="#use-firmware-retraction" id="use-firmware-retraction"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `use_firmware_retraction`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--use-firmware-retraction=1`.\
This experimental setting uses G10 and G11 commands to have the firmware handle the retraction. This is only supported in recent Marlin.

## Bed temperature type[¶](advanced-printer-settings.md#bed-temperature-type) <a href="#bed-temperature-type" id="bed-temperature-type"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `bed_temperature_formula`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `Choice`.\
[Options](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `by_first_filament, by_highest_temp`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--bed-temperature-formula=by_first_filament`.\
This option determines how the bed temperature is set during slicing: based on the temperature of the first filament or the highest temperature of the printed filaments.

## Time cost[¶](advanced-printer-settings.md#time-cost) <a href="#time-cost" id="time-cost"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `time_cost`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--time-cost=1`.\
The printer cost per hour.

## Build plate tilt[¶](advanced-printer-settings.md#build-plate-tilt) <a href="#build-plate-tilt" id="build-plate-tilt"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Expert`.\
[Variables](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `build_plate_tilt_x`, `build_plate_tilt_y`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--build-plate-tilt-x=1` (same pattern for the other variables above).

Important

NEW FEATURE: **Build plate tilt**\
Available in: [Nightly builds](https://github.com/OrcaSlicer/OrcaSlicer/releases/tag/nightly-builds) or Releases greater than **2.4.2**.

**Build plate tilt X** and **Build plate tilt Y** specify the build surface's tilt in degrees. Support generation uses these values to adjust its gravity direction, so overhangs are evaluated relative to the machine's actual downward direction rather than the slicer's Z axis.

Set both to 0 for a level bed.

On a [belt printer](/broken/pages/00dcd987ac21f7e44ecf650ee21f58b8c880cf8a), these values are derived from the [belt tilt](/broken/pages/00dcd987ac21f7e44ecf650ee21f58b8c880cf8a#belt-tilt) each time a print is prepared, overwriting any manual entries. A belt tilt about X sets **Build plate tilt X**, and a belt tilt about Y sets **Build plate tilt Y**.
