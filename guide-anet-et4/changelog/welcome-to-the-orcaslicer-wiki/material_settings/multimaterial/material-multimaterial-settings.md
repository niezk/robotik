# Material Multimaterial Settings¶

This page documents the settings used when printing with multiple materials in Orca Slicer. It explains wipe-tower parameters, tool-change behaviour for both single-extruder and multi-extruder multimaterial setups, and ramming/purge options that help ensure reliable, contamination-free material changes.

* [Multimaterial Wipe Tower Parameters](material-multimaterial-settings.md#multimaterial-wipe-tower-parameters)
  * [Minimal purge on wipe tower](material-multimaterial-settings.md#minimal-purge-on-wipe-tower)
* [Multi Filament](material-multimaterial-settings.md#multi-filament)
* [Tool change parameters with single extruder](material-multimaterial-settings.md#tool-change-parameters-with-single-extruder)
  * [Loading speed at the start](material-multimaterial-settings.md#loading-speed-at-the-start)
  * [Loading speed](material-multimaterial-settings.md#loading-speed)
  * [Unloading speed at the start](material-multimaterial-settings.md#unloading-speed-at-the-start)
  * [Unloading speed](material-multimaterial-settings.md#unloading-speed)
  * [Delay after unloading](material-multimaterial-settings.md#delay-after-unloading)
  * [Number of cooling moves](material-multimaterial-settings.md#number-of-cooling-moves)
  * [Speed of the first cooling move](material-multimaterial-settings.md#speed-of-the-first-cooling-move)
  * [Speed of the last cooling move](material-multimaterial-settings.md#speed-of-the-last-cooling-move)
  * [Stamping loading speed](material-multimaterial-settings.md#stamping-loading-speed)
  * [Stamping distance](material-multimaterial-settings.md#stamping-distance)
  * [Ramming parameters](material-multimaterial-settings.md#ramming-parameters)
    * [Total ramming](material-multimaterial-settings.md#total-ramming)
    * [Ramming line](material-multimaterial-settings.md#ramming-line)
* [Tool change parameters with multi extruder](material-multimaterial-settings.md#tool-change-parameters-with-multi-extruder)
  * [Enable ramming for multi-tool setups](material-multimaterial-settings.md#enable-ramming-for-multi-tool-setups)
    * [Multi-tool ramming volume](material-multimaterial-settings.md#multi-tool-ramming-volume)
    * [Multi-tool ramming flow](material-multimaterial-settings.md#multi-tool-ramming-flow)

## Multimaterial Wipe Tower Parameters[¶](material-multimaterial-settings.md#multimaterial-wipe-tower-parameters) <a href="#multimaterial-wipe-tower-parameters" id="multimaterial-wipe-tower-parameters"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variables](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `filament_minimal_purge_on_wipe_tower`, `filament_tower_interface_pre_extrusion_dist`, `filament_tower_interface_pre_extrusion_length`, `filament_tower_ironing_area`, `filament_tower_interface_purge_volume`, `filament_tower_interface_print_temp`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb): `filament_minimal_purge_on_wipe_tower` (Float list), `filament_tower_interface_pre_extrusion_dist` (Float list), `filament_tower_interface_pre_extrusion_length` (Float list), `filament_tower_ironing_area` (Float list), `filament_tower_interface_purge_volume` (Float list), `filament_tower_interface_print_temp` (Integer list).\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--filament-minimal-purge-on-wipe-tower=1` (`filament_minimal_purge_on_wipe_tower` shown; other variables above follow their own type).\
Wipe towers are sacrificial structures printed alongside the main object to purge excess material from the nozzle after a tool change in multimaterial printing. This ensures that the next extrusion uses the correct filament color or type without contamination from the previous material.

### Minimal purge on wipe tower[¶](material-multimaterial-settings.md#minimal-purge-on-wipe-tower) <a href="#minimal-purge-on-wipe-tower" id="minimal-purge-on-wipe-tower"></a>

After a tool change, the exact position of the newly loaded filament inside the nozzle may not be known, and the filament pressure is likely not yet stable. Before purging the print head into an infill or a sacrificial object, Orca Slicer will always prime this amount of material into the wipe tower to produce successive infill or sacrificial object extrusions reliably.

## Multi Filament[¶](material-multimaterial-settings.md#multi-filament) <a href="#multi-filament" id="multi-filament"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variables](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `long_retractions_when_ec`, `retraction_distances_when_ec`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb): `long_retractions_when_ec` (Boolean list), `retraction_distances_when_ec` (Float list).\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--long-retractions-when-ec=1` (`long_retractions_when_ec` shown; other variables above follow their own type).\
Enable long retraction when the extruder changes and set its retraction distance value for extruder changes.

## Tool change parameters with single extruder[¶](material-multimaterial-settings.md#tool-change-parameters-with-single-extruder) <a href="#tool-change-parameters-with-single-extruder" id="tool-change-parameters-with-single-extruder"></a>

These settings control filament loading and unloading for single-extruder multimaterial systems (where multiple filaments are fed to a single hotend). They govern how much filament is primed or purged on the wipe tower, the speeds used during load/unload phases, delays for flexible materials, cooling-move behaviour, stamping and the ramming routine. Proper tuning reduces cross-contamination between filaments and improves tool-change reliability.

### Loading speed at the start[¶](material-multimaterial-settings.md#loading-speed-at-the-start) <a href="#loading-speed-at-the-start" id="loading-speed-at-the-start"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `filament_loading_speed_start`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--filament-loading-speed-start=1`.\
Speed used at the very beginning of loading phase.

### Loading speed[¶](material-multimaterial-settings.md#loading-speed) <a href="#loading-speed" id="loading-speed"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `filament_loading_speed`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--filament-loading-speed=1`.\
Speed used for loading the filament on the wipe tower.

### Unloading speed at the start[¶](material-multimaterial-settings.md#unloading-speed-at-the-start) <a href="#unloading-speed-at-the-start" id="unloading-speed-at-the-start"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `filament_unloading_speed_start`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--filament-unloading-speed-start=1`.\
Speed used for unloading the tip of the filament immediately after ramming.

### Unloading speed[¶](material-multimaterial-settings.md#unloading-speed) <a href="#unloading-speed" id="unloading-speed"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `filament_unloading_speed`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--filament-unloading-speed=1`.\
Speed used for unloading the filament on the wipe tower (does not affect initial part of unloading just after ramming).

### Delay after unloading[¶](material-multimaterial-settings.md#delay-after-unloading) <a href="#delay-after-unloading" id="delay-after-unloading"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `filament_toolchange_delay`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--filament-toolchange-delay=1`.\
Time to wait after the filament is unloaded. May help to get reliable tool changes with flexible materials that may need more time to shrink to original dimensions.

### Number of cooling moves[¶](material-multimaterial-settings.md#number-of-cooling-moves) <a href="#number-of-cooling-moves" id="number-of-cooling-moves"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `filament_cooling_moves`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Integer list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--filament-cooling-moves=1`.\
Filament is cooled by being moved back and forth in the cooling tubes. Specify desired number of these moves.

### Speed of the first cooling move[¶](material-multimaterial-settings.md#speed-of-the-first-cooling-move) <a href="#speed-of-the-first-cooling-move" id="speed-of-the-first-cooling-move"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `filament_cooling_initial_speed`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--filament-cooling-initial-speed=1`.\
Cooling moves are gradually accelerating beginning at this speed.

### Speed of the last cooling move[¶](material-multimaterial-settings.md#speed-of-the-last-cooling-move) <a href="#speed-of-the-last-cooling-move" id="speed-of-the-last-cooling-move"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `filament_cooling_final_speed`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--filament-cooling-final-speed=1`.\
Cooling moves are gradually accelerating towards this speed.

### Stamping loading speed[¶](material-multimaterial-settings.md#stamping-loading-speed) <a href="#stamping-loading-speed" id="stamping-loading-speed"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `filament_stamping_loading_speed`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--filament-stamping-loading-speed=1`.\
Speed used for stamping.

### Stamping distance[¶](material-multimaterial-settings.md#stamping-distance) <a href="#stamping-distance" id="stamping-distance"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `filament_stamping_distance`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--filament-stamping-distance=1`.\
Stamping distance measured from the center of the cooling tube. If set to non-zero value, filament is moved toward the nozzle between the individual cooling moves ("stamping"). This option configures how long this movement should be before the filament is retracted again.

### Ramming parameters[¶](material-multimaterial-settings.md#ramming-parameters) <a href="#ramming-parameters" id="ramming-parameters"></a>

This string is edited by RammingDialog and contains ramming specific parameters.

#### Total ramming[¶](material-multimaterial-settings.md#total-ramming) <a href="#total-ramming" id="total-ramming"></a>

The total amount of filament that will be forcibly extruded (rammed) into the nozzle during the ramming stage. This value represents the full volume (or equivalent extrusion length) applied by the ramming routine to ensure the nozzle contains the intended material and pressure before printing resumes.

#### Ramming line[¶](material-multimaterial-settings.md#ramming-line) <a href="#ramming-line" id="ramming-line"></a>

Defines the geometry or pattern used when ramming material (for example a short line or dot on the wipe tower). The ramming line parameters control where the rammed material is deposited so it is reliably captured by the wipe structure instead of contaminating the printed part.

## Tool change parameters with multi extruder[¶](material-multimaterial-settings.md#tool-change-parameters-with-multi-extruder) <a href="#tool-change-parameters-with-multi-extruder" id="tool-change-parameters-with-multi-extruder"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `filament_multitool_ramming`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Boolean list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--filament-multitool-ramming=1`.\
These options apply to printers that use multiple independent extruders or hotends (multi-tool setups). When enabled, ramming and related parameters define a small, controlled extrusion on the wipe tower immediately before a tool change to ensure the outgoing tool is cleared and the incoming tool begins with consistent filament at the nozzle. Use these settings to tune multi-tool handoffs and avoid color or material mixing.

### Enable ramming for multi-tool setups[¶](material-multimaterial-settings.md#enable-ramming-for-multi-tool-setups) <a href="#enable-ramming-for-multi-tool-setups" id="enable-ramming-for-multi-tool-setups"></a>

Perform ramming when using multi-tool printer (i.e. when the 'Single Extruder Multimaterial' in Printer Settings is unchecked). When checked, a small amount of filament is rapidly extruded on the wipe tower just before the tool change. This option is only used when the wipe tower is enabled.

#### Multi-tool ramming volume[¶](material-multimaterial-settings.md#multi-tool-ramming-volume) <a href="#multi-tool-ramming-volume" id="multi-tool-ramming-volume"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `filament_multitool_ramming_volume`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--filament-multitool-ramming-volume=1`.\
The volume to be rammed before the tool change.

#### Multi-tool ramming flow[¶](material-multimaterial-settings.md#multi-tool-ramming-flow) <a href="#multi-tool-ramming-flow" id="multi-tool-ramming-flow"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `filament_multitool_ramming_flow`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--filament-multitool-ramming-flow=1`.\
Flow used for ramming the filament before the tool change.
