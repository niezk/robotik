# Machine G-code¶

Machine G-code are custom G-code scripts that are executed at specific points during the printing process. These scripts can be used to customize printer behavior, such as setting temperatures, moving the print head, or controlling fans.

Tip

See your printer's firmware documentation for supported G-code commands and features.

* [Marlin G-code](https://marlinfw.org/meta/gcode/)
* [RepRap G-code](https://reprap.org/wiki/G-code)
* [Klipper G-code](https://www.klipper3d.org/G-Codes)

Important

Machine G-code scripts are powerful tools for customizing your printing process. However, they can also cause issues if not used correctly.\
It's recommended to use a known base of G-code commands for your specific printer firmware (e.g., Marlin, RepRap, etc.) and to understand the implications of each command used in the scripts.\
Always test your G-code scripts thoroughly before using them in production.

* [Machine start G-code](machine-g-code.md#machine-start-g-code)
* [Machine end G-code](machine-g-code.md#machine-end-g-code)
* [Printing by object G-code](machine-g-code.md#printing-by-object-g-code)
* [Before layer change G-code](machine-g-code.md#before-layer-change-g-code)
* [Layer change G-code](machine-g-code.md#layer-change-g-code)
* [Timelapse G-code](machine-g-code.md#timelapse-g-code)
* [Clumping detection G-code](machine-g-code.md#clumping-detection-g-code)
* [Change filament G-code](machine-g-code.md#change-filament-g-code)
* [Change extrusion role G-code](machine-g-code.md#change-extrusion-role-g-code)
* [Pause G-code](machine-g-code.md#pause-g-code)
* [Template Custom G-code](machine-g-code.md#template-custom-g-code)

## Machine start G-code[¶](machine-g-code.md#machine-start-g-code) <a href="#machine-start-g-code" id="machine-start-g-code"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `machine_start_gcode`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#text): `Text`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--machine-start-gcode=value`.\
This G-code is executed at the beginning of a print job, before any printing starts. It is typically used to prepare the printer for printing, such as homing axes, heating the bed and nozzle, and performing any necessary pre-print checks.

You can also use it for setting up custom notifications with M300 (play beep sound) or use a custom purge sequence:

```
G90 ; use absolute coordinates
M83 ; extruder relative mode
M140 S[bed_temperature_initial_layer_single] ; set final bed temp
M104 S150 ; set temporary nozzle temp to prevent oozing during homing
G4 S10 ; allow partial nozzle warmup
G28 ; home all axis
G1 Z25 F240 ; lift nozzle
G1 X2 Y10 F3000 ; move to front left
M104 S[nozzle_temperature_initial_layer] ; set final nozzle temp
M190 S[bed_temperature_initial_layer_single] ; wait for bed temp to stabilize
M109 S[nozzle_temperature_initial_layer] ; wait for nozzle temp to stabilize
; Start Beep to indicate ready to print
M300 P136 S622
M300 P136 S0
M300 P136 S311
M300 P136 S466
M300 P273 S0
M300 P136 S415
M300 P409 S0
M300 P136 S622
M300 P136 S0
M300 P545 S466
; Purge Line
G1 Z0.28 F240 ; move to a custom layer height for purge
G1 X{first_layer_print_min[0]-15} Y{first_layer_print_min[1]} Z0.8 F6000.0 ; position 15mm left from the lower left of the first layer
G1 X{first_layer_print_min[0]-15} Y{first_layer_print_min[1]+30} E30 F360.0 ; extrude 30mm of filament in the y direction
G92 E0.0 ; reset extruder
G1 E-0.5 F2100 ; small retraction
G1 Y{first_layer_print_min[1]+40} F6000.0 ; move an additional 10mm without extruding
G92 E0.0 ; reset extruder
```

## Machine end G-code[¶](machine-g-code.md#machine-end-g-code) <a href="#machine-end-g-code" id="machine-end-g-code"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `machine_end_gcode`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#text): `Text`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--machine-end-gcode=value`.\
This G-code is executed at the end of a print job, after all printing is complete. It is typically used to turn off heaters, move the print head away from the print, and perform any necessary post-print actions.

## Printing by object G-code[¶](machine-g-code.md#printing-by-object-g-code) <a href="#printing-by-object-g-code" id="printing-by-object-g-code"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `printing_by_object_gcode`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#text): `Text`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--printing-by-object-gcode=value`.\
This G-code is executed at the start of printing each individual object in a multi-object print job. It can be used to set specific parameters or perform actions for each object.

## Before layer change G-code[¶](machine-g-code.md#before-layer-change-g-code) <a href="#before-layer-change-g-code" id="before-layer-change-g-code"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `before_layer_change_gcode`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#text): `Text`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--before-layer-change-gcode=value`.\
This G-code is inserted at every layer change before the Z lift.

## Layer change G-code[¶](machine-g-code.md#layer-change-g-code) <a href="#layer-change-g-code" id="layer-change-g-code"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `layer_change_gcode`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#text): `Text`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--layer-change-gcode=value`.\
This G-code is inserted at every layer change after the Z lift.

## Timelapse G-code[¶](machine-g-code.md#timelapse-g-code) <a href="#timelapse-g-code" id="timelapse-g-code"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `time_lapse_gcode`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#text): `Text`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--time-lapse-gcode=value`.\
This G-code is used for capturing timelapse videos. It typically includes commands to move the print head out of the way for a photo and then return it to the previous position.

## Clumping detection G-code[¶](machine-g-code.md#clumping-detection-g-code) <a href="#clumping-detection-g-code" id="clumping-detection-g-code"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `wrapping_detection_gcode`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#text): `Text`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--wrapping-detection-gcode=value`.\
This G-code is inserted on every layer when [Enable clumping detection](/broken/pages/e792de15ca89fe7bca7e8654ec76e5852fdd584b#enable-clumping-detection) is enabled, to run the printer's check for filament clumped around the nozzle. Use the `layer_num` placeholder to choose the layers to check; the Bambu Lab profiles check a few of the early layers.

## Change filament G-code[¶](machine-g-code.md#change-filament-g-code) <a href="#change-filament-g-code" id="change-filament-g-code"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `change_filament_gcode`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#text): `Text`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--change-filament-gcode=value`.\
This G-code is inserted when filament is changed, including T commands to trigger tool change.

## Change extrusion role G-code[¶](machine-g-code.md#change-extrusion-role-g-code) <a href="#change-extrusion-role-g-code" id="change-extrusion-role-g-code"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `change_extrusion_role_gcode`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#text): `Text`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--change-extrusion-role-gcode=value`.\
This G-code is inserted when the [extrusion role](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918#extrusion-roles) is changed. This is the Machine section of the feature "Change Extrusion Role G-code" that is also available in the [Material settings](/broken/pages/cf559c7d8c6efcfa6ad4874d5e3a5bf852fedf35#change-extrusion-role-g-code) and [Process settings](/broken/pages/0af98e38fec56fc5c304620f4275365dea6ded9c#change-extrusion-role-g-code).

Example G-codes:

* Marlin g-code to set fan speed to 10% (S25 out of S255) for BridgeInfill role and 30% (S75 out of S255) for other roles:

```
{if( extrusion_role == "BridgeInfill")}
M106 S25
{else}
M106 S75
{endif}
```

* Marlin G-code to set the fan speed to 0% for the ['Internal Sparse Infill' role](/broken/pages/da1f51648c030aebc578bfec4de7c7b47ec7ddd2) and the first three layers, and to 30% `0.3*255` for the other roles. This achieves good layer adhesion while maintaining perimeter quality.:

```
{if(extrusion_role)=="InternalInfill" || layer_num < 4 }
M106 S0
{else}
M106 S{0.3*255}
{endif}
```

* Marlin g-code to set pressure advance to 0 for ['Internal Sparse Infill' role](/broken/pages/da1f51648c030aebc578bfec4de7c7b47ec7ddd2) and restore it to previous value for other roles:

```
{if( extrusion_role == "InternalInfill")}
M900 K0
{else}
M900 K{pressure_advance[0]}
{endif}
```

## Pause G-code[¶](machine-g-code.md#pause-g-code) <a href="#pause-g-code" id="pause-g-code"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `machine_pause_gcode`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#text): `Text`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--machine-pause-gcode=value`.\
This G-code will be used as a code for the pause print. Users can insert pause G-code in the G-code viewer.

## Template Custom G-code[¶](machine-g-code.md#template-custom-g-code) <a href="#template-custom-g-code" id="template-custom-g-code"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `template_custom_gcode`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#text): `Text`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--template-custom-gcode=value`.\
This section allows users to define custom G-code templates that can be reused across different print jobs. Users can create and manage their own G-code snippets for various purposes.
