# G-Code Output¶

These settings control how G-code is generated and formatted. They impact readability, file size, print behavior, and compatibility with firmware and post-processing tools.

* [Reduce Infill Retraction](g-code-output.md#reduce-infill-retraction)
* [Add line number](g-code-output.md#add-line-number)
* [Verbose G-code](g-code-output.md#verbose-g-code)
* [High precision G-code](g-code-output.md#high-precision-g-code)
* [Label Objects](g-code-output.md#label-objects)
* [Exclude Objects](g-code-output.md#exclude-objects)
* [Filename Format](g-code-output.md#filename-format)
* [Change extrusion role G-code](g-code-output.md#change-extrusion-role-g-code)

## Reduce Infill Retraction[¶](g-code-output.md#reduce-infill-retraction) <a href="#reduce-infill-retraction" id="reduce-infill-retraction"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `reduce_infill_retraction`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--reduce-infill-retraction=1`.\
When enabled, the slicer will skip retractions for travel moves that occur entirely inside infill regions. This reduces the number of retractions and can speed up printing for complex models, but it may increase oozing or stringing inside infill. Slicing time may also increase slightly.

Each retraction adds moves that print nothing, and a travel that skips it skips all of them, keeping only the travel itself:

* The [retraction](/broken/pages/75e6952d821ef19c2ad711c5a0448fb610dfb3b0#length) pulls the filament back at the [Retraction speed](/broken/pages/75e6952d821ef19c2ad711c5a0448fb610dfb3b0#retraction-speed) before the travel, and the [deretraction](/broken/pages/75e6952d821ef19c2ad711c5a0448fb610dfb3b0#deretraction-speed) pushes it back, plus any [Extra length on restart](/broken/pages/75e6952d821ef19c2ad711c5a0448fb610dfb3b0#extra-length-on-restart), before the next line starts. With the default 0.8 mm at 30 mm/s, each of the two takes about 27 ms.
* With [Wipe while retracting](/broken/pages/75e6952d821ef19c2ad711c5a0448fb610dfb3b0#wipe-while-retracting), the nozzle also moves back along the last line for the [Wipe distance](/broken/pages/75e6952d821ef19c2ad711c5a0448fb610dfb3b0#wipe-distance) while it retracts.
* With a [Z-hop](/broken/pages/dc18322a6319f10648e1a1374e7cae7f8bb073ca#z-hop-height), the nozzle lifts before the travel and lowers after it, on the Z axis, which on most printers is much slower than X and Y.

Tens of milliseconds per travel can add up to minutes over the thousands of infill travels of a large print.

Travels shorter than the [Travel distance threshold](/broken/pages/75e6952d821ef19c2ad711c5a0448fb610dfb3b0#travel-distance-threshold) never retract, with or without this option. Infill lines whose ends are next to each other are joined into one path (see [Anchor](/broken/pages/da1f51648c030aebc578bfec4de7c7b47ec7ddd2#anchor)), so there is no travel to retract for between them.

**Recommended** when internal cosmetic quality is not critical and you want fewer retractions.

## Add line number[¶](g-code-output.md#add-line-number) <a href="#add-line-number" id="add-line-number"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Developer`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `gcode_add_line_number`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--gcode-add-line-number=1`.\
Prefix each G-code line with a sequential line number (N1, N2, ...). Useful for debugging or tools that expect numbered G-code.

## Verbose G-code[¶](g-code-output.md#verbose-g-code) <a href="#verbose-g-code" id="verbose-g-code"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `gcode_comments`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--gcode-comments=1`.\
Include descriptive comments for G-code lines and blocks to make the file human-readable and easier to debug.\
Verbose mode produces much larger files and may slow down SD-card printing on some printers.

## High precision G-code[¶](g-code-output.md#high-precision-g-code) <a href="#high-precision-g-code" id="high-precision-g-code"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Expert`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `high_precision_gcode`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--high-precision-gcode=1`.

Important

NEW FEATURE: **High precision G-code (experimental)**\
Available in: [Nightly builds](https://github.com/OrcaSlicer/OrcaSlicer/releases/tag/nightly-builds) or Releases greater than **2.4.2**.

Writes the X, Y, Z, I and J coordinates with 4 decimal places instead of 3, and E with 6 instead of 5, to reduce rounding errors in the G-code. Feedrates keep 3 decimal places.\
With [relative E distances](/broken/pages/eeff389a3bf7caa2aee6f13fbffe1d91ee4800d4#use-relative-e-distances), the rounding error of each move is also carried over to the next one, so short moves of about the same length don't all round the flow in the same direction.

This may help stabilize extrusion with small nozzles (e.g. 0.2 mm) and thin layers (e.g. 0.08 mm or less), where each move extrudes so little material that rounding errors matter most. The effect depends strongly on how well the rest of the settings are tuned and may be hard to notice unless the filament and print profiles are well [calibrated](/broken/pages/11c07341f1c2537a4800ccab7e8c9c26d87a5246).

* **Supports** are removed after printing, so they keep the standard precision. Support ironing keeps the higher precision, as it smooths the surface the object is printed on.
* **File size:** the G-code becomes about 10% larger, which may slow down printers that parse G-code slowly.
* **Off:** the G-code is the same as before this option existed.

## Label Objects[¶](g-code-output.md#label-objects) <a href="#label-objects" id="label-objects"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `gcode_label_objects`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--gcode-label-objects=1`.\
Insert comments that label moves with the object they belong to (object index or name). This is useful for integrations such as OctoPrint's Cancel Object plugin and for human inspection of the G-code.

## Exclude Objects[¶](g-code-output.md#exclude-objects) <a href="#exclude-objects" id="exclude-objects"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `exclude_object`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--exclude-object=1`.\
Add commands to the G-code that define each object and mark where it starts and ends, so the printer firmware can skip (cancel) individual objects during the print: `EXCLUDE_OBJECT_DEFINE`, `EXCLUDE_OBJECT_START` and `EXCLUDE_OBJECT_END` for Klipper, and `M486` for Marlin and RepRapFirmware.

### Outline Tolerance[¶](g-code-output.md#outline-tolerance) <a href="#outline-tolerance" id="outline-tolerance"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Expert`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `exclude_object_tolerance`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--exclude-object-tolerance=1`.

Controls the precision of the exclude-object outlines simplified via the Douglas-Peucker algorithm. This setting only applies to **Klipper** firmware (`EXCLUDE_OBJECT_DEFINE` lines), as Marlin and RepRapFirmware use `M486` commands without polygon definitions.

* **Default:** `0.1 mm`.
* **When to adjust:** If your printer has a limited CPU capacity and you are printing a full plate with many objects, highly detailed outlines can generate very large arrays. Processing these lines or running macros that iterate over them (such as KAMP adaptive meshing) can cause Klipper to trigger a `Timer too close` error.
* **Recommendation:** Raising this value to `0.2 mm` - `0.4 mm` significantly reduces the total number of points and prevents printer timeouts, with a negligible impact on outline precision. Setting it to `0` retains every point of the convex hull.

## Filename Format[¶](g-code-output.md#filename-format) <a href="#filename-format" id="filename-format"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `filename_format`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#text): `Text`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--filename-format={input_filename_base}_{filament_type[initial_tool]}_{print_time}.gcode`.\
Define a filename template for exported G-code. Templates may include tokens like project name, date, or other metadata to produce consistent and informative filenames on export.

For example:

```
{input_filename_base}_{filament_type[initial_tool]}_{print_time}.gcode
```

This can be used to generate filenames like `OrcaCube_PLA_1h15m.gcode`.

Tip

Check [File Name Template](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918#file-name-template) for available tokens and their meanings.

## Change extrusion role G-code[¶](g-code-output.md#change-extrusion-role-g-code) <a href="#change-extrusion-role-g-code" id="change-extrusion-role-g-code"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `process_change_extrusion_role_gcode`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#text): `Text`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--process-change-extrusion-role-gcode=value`.\
This G-code is inserted when the [extrusion role](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918#extrusion-roles) is changed.\
This is the process version of the **Change extrusion role G-code** that is also available in the [Material settings](/broken/pages/cf559c7d8c6efcfa6ad4874d5e3a5bf852fedf35#change-extrusion-role-g-code) and [Printer settings](/broken/pages/8a0cca48a8cb689eb2e37db1bc877c26189bf981#change-extrusion-role-g-code), and it runs after both of them.

Tip

Read the [Printer settings](/broken/pages/8a0cca48a8cb689eb2e37db1bc877c26189bf981#change-extrusion-role-g-code) for more details and examples.
