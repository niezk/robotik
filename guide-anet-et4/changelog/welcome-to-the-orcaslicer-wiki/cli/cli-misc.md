# CLI Misc¶

Options for loading settings/filaments, selecting objects, output locations, logging, and 3MF metadata. See [CLI Mode](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24) for general flag syntax.

* [Loading Settings & Filaments](cli-misc.md#loading-settings-filaments)
* [Object Selection](cli-misc.md#object-selection)
* [Output & Logging](cli-misc.md#output-logging)
* [Arrange Behavior](cli-misc.md#arrange-behavior)
* [Metadata](cli-misc.md#metadata)
* [Print Behavior](cli-misc.md#print-behavior)

## Loading Settings & Filaments[¶](cli-misc.md#loading-settings-filaments) <a href="#loading-settings-filaments" id="loading-settings-filaments"></a>

These load the same per-tab JSON files produced by each settings tab's Save/Export action — see [Export Preset Bundle](/broken/pages/f2c68b382bf7caa0d1c1d0addfed2d60d9583c14#export-preset-bundle) for how those files are created in the GUI.

| Flag                   | Input                                 | Description                                                                                                                                             | Notes |
| ---------------------- | ------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- | ----- |
| `--load-settings`      | `"setting1.json;setting2.json"`       | Load process/machine settings from the given file(s), semicolon-separated.                                                                              |       |
| `--load-filaments`     | `"filament1.json;filament2.json;..."` | Load filament settings from the given file(s), semicolon-separated.                                                                                     |       |
| `--uptodate-settings`  | `"setting1.json;setting2.json"`       | Process/machine settings to load when used together with [`--uptodate`](/broken/pages/61ee1adbe009d97d3739836a2fa144a9f1598c07#misc-actions).           |       |
| `--uptodate-filaments` | `"filament1.json;filament2.json;..."` | Filament settings to load when used together with [`--uptodate`](/broken/pages/61ee1adbe009d97d3739836a2fa144a9f1598c07#misc-actions).                  |       |
| `--downward-check`     | boolean                               | Check whether the current machine is downward-compatible with the machines listed in `--downward-settings`.                                             |       |
| `--downward-settings`  | `"machine1.json;machine2.json;..."`   | Machine settings list to check against when `--downward-check` is enabled.                                                                              |       |
| `--load-custom-gcodes` | `custom_gcode_toolchange.json`        | Load a custom G-code toolchange definition from a JSON file. Related concept: [Machine G-code](/broken/pages/8a0cca48a8cb689eb2e37db1bc877c26189bf981). |       |

## Object Selection[¶](cli-misc.md#object-selection) <a href="#object-selection" id="object-selection"></a>

| Flag                   | Input                | Description                                                                                                                      | Notes                                                                                                                                      |
| ---------------------- | -------------------- | -------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| `--skip-objects`       | `"3,5,10,77"`        | Skip the given object indices when printing.                                                                                     |                                                                                                                                            |
| `--clone-objects`      | `"1,3,1,10"`         | Clone count for each object in the load list.                                                                                    | Cannot be combined with [`--assemble`](/broken/pages/c4bdcf8107a63e5f7b78401a5f9b4cc677fe24b9#object-handling).                            |
| `--load-assemble-list` | `assemble_list.json` | Load a full assemble object list (plates, objects, and their parameters) from a config file, instead of loading models directly. | Cannot be combined with positional input model files or with any [transform](/broken/pages/c4bdcf8107a63e5f7b78401a5f9b4cc677fe24b9) flag. |
| `--load-filament-ids`  | `"1,2,3,1"`          | Filament ID to assign to each loaded object, one entry per input file.                                                           | List length must match the number of input files.                                                                                          |

## Output & Logging[¶](cli-misc.md#output-logging) <a href="#output-logging" id="output-logging"></a>

| Flag                  | Input              | Description                                                                                                                                                                                                                                                                                                       | Notes                                                                                                                       |
| --------------------- | ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| `--datadir`           | `dir`              | Load and store settings at the given directory, instead of the default user config location. Useful for maintaining separate profile sets. Related concept: [Portable User Configuration](/broken/pages/15bf90f1647b89b37dbdd42e07af66a91bf4cb14#portable-user-configuration).                                    |                                                                                                                             |
| `--outputdir`         | `dir`              | Output directory for exported files.                                                                                                                                                                                                                                                                              | Created recursively if it doesn't exist; the process exits with an error if creation fails.                                 |
| `--export-statistics` | boolean            | Write the statistics of each sliced plate as JSON, as `plate_N.statistics.json` next to its G-code in the output directory and inside the 3MF of [`--export-3mf`](/broken/pages/61ee1adbe009d97d3739836a2fa144a9f1598c07#export): print time, filament and feature totals, and the same per layer and per object. | Same files as the [Export Statistics](/broken/pages/f2c68b382bf7caa0d1c1d0addfed2d60d9583c14#export-statistics) preference. |
| `--debug`             | `level` (int, 0-5) | Debug logging level: `0` fatal, `1` error, `2` warning, `3` info, `4` debug, `5` trace.                                                                                                                                                                                                                           | Default: `1`.                                                                                                               |
| `--logfile`           | `file`             | Redirect debug logging to a file instead of stderr.                                                                                                                                                                                                                                                               |                                                                                                                             |

## Arrange Behavior[¶](cli-misc.md#arrange-behavior) <a href="#arrange-behavior" id="arrange-behavior"></a>

These correspond to options in the GUI's [Auto Arrange](/broken/pages/0fcd3913806f2ebe7be268c6b82f8de56ec468b6#parameters) panel.

| Flag                            | Input   | Description                                                                                                                                                                                            | Notes                                            |
| ------------------------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------ |
| `--allow-multicolor-oneplate`   | boolean | Allow multiple materials/colors to be arranged onto the same plate. See "Allow multiple materials on same plate" in [Auto Arrange](/broken/pages/0fcd3913806f2ebe7be268c6b82f8de56ec468b6#parameters). | Default: on.                                     |
| `--allow-rotations`             | boolean | Allow arrange to rotate objects to fit. See "Auto rotate for arrangement" in [Auto Arrange](/broken/pages/0fcd3913806f2ebe7be268c6b82f8de56ec468b6#parameters).                                        | Default: on.                                     |
| `--align-to-y-axis`             | boolean | Turn each object so its long side runs along the Y axis before arranging. See "Align to Y axis" in [Auto Arrange](/broken/pages/0fcd3913806f2ebe7be268c6b82f8de56ec468b6#parameters).                  | Default: on for i3 printers, off for the others. |
| `--avoid-extrusion-cali-region` | boolean | Avoid the extrusion calibration region on the plate when arranging.                                                                                                                                    | Default: off.                                    |

## Metadata[¶](cli-misc.md#metadata) <a href="#metadata" id="metadata"></a>

| Flag                 | Input                 | Description                                                            | Notes                                        |
| -------------------- | --------------------- | ---------------------------------------------------------------------- | -------------------------------------------- |
| `--makerlab-name`    | `name`                | MakerLab name embedded when generating the 3MF.                        |                                              |
| `--makerlab-version` | `version`             | MakerLab version embedded when generating the 3MF.                     |                                              |
| `--metadata-name`    | `"name1;name2;..."`   | Custom metadata field name(s) to add to the 3MF, semicolon-separated.  | Paired positionally with `--metadata-value`. |
| `--metadata-value`   | `"value1;value2;..."` | Custom metadata field value(s) to add to the 3MF, semicolon-separated. | Paired positionally with `--metadata-name`.  |

## Print Behavior[¶](cli-misc.md#print-behavior) <a href="#print-behavior" id="print-behavior"></a>

| Flag                     | Input   | Description                                                                                                                   | Notes                       |
| ------------------------ | ------- | ----------------------------------------------------------------------------------------------------------------------------- | --------------------------- |
| `--enable-timelapse`     | boolean | Treat this slicing run as using timelapse. See [Timelapse](/broken/pages/e792de15ca89fe7bca7e8654ec76e5852fdd584b#timelapse). | Default: off.               |
| `--skip-modified-gcodes` | boolean | Skip modified G-code (from printer/filament presets) embedded in a loaded 3MF.                                                | Default: off.               |
| `--allow-newer-file`     | boolean | Allow slicing a 3MF that was saved by a newer OrcaSlicer version than the one running.                                        | Default: off.               |
| `--allow-mix-temp`       | boolean | Allow filaments with high/low temperature requirements to be printed together.                                                | Internal use; default: off. |
