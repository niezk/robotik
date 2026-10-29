# Retraction¶

Retraction is the process of pulling the filament back into the nozzle to prevent oozing and stringing during non-print moves.\
If the retraction length is too short, it may not effectively prevent oozing, while if it's too long, it can lead to clogs or under-extrusion.\
Filaments like PETG and TPU are more prone to stringing, so they may require longer retraction lengths compared to PLA or ABS. You can override your printer's default retraction settings for each filament in [Material Setting Overrides](/broken/pages/81491811ca710a7d7f259cedc43d59f3fb1d8de0#retraction).

Tip

Check out the [Retraction Test](/broken/pages/e6b6ad6b99eb71f43300b2ccaf614ef88bf90bb4) to help determine the optimal retraction settings for your filament.

* [Length](retraction.md#length)
* [Extra length on restart](retraction.md#extra-length-on-restart)
* [Retraction speed](retraction.md#retraction-speed)
* [Deretraction speed](retraction.md#deretraction-speed)
* [Travel distance threshold](retraction.md#travel-distance-threshold)
* [Retract on layer change](retraction.md#retract-on-layer-change)
* [Wipe while retracting](retraction.md#wipe-while-retracting)
* [Wipe distance](retraction.md#wipe-distance)
* [Retract amount before wipe](retraction.md#retract-amount-before-wipe)
* [Retract amount after wipe](retraction.md#retract-amount-after-wipe)
* [Retraction When Switching Materials](retraction.md#retraction-when-switching-materials)
  * [Long retraction when cut (beta)](retraction.md#long-retraction-when-cut-beta)

## Length[¶](retraction.md#length) <a href="#length" id="length"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Simple`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `retraction_length[extruder_idx]`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--retraction-length=1`.\
When retraction is triggered before changing tool, filament is pulled back by the specified amount (the length is measured on raw filament, before it enters the extruder).

## Extra length on restart[¶](retraction.md#extra-length-on-restart) <a href="#extra-length-on-restart" id="extra-length-on-restart"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `retract_restart_extra[extruder_idx]`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--retract-restart-extra=1`.\
When the retraction is compensated after changing tool, the extruder will push this additional amount of filament.

## Retraction speed[¶](retraction.md#retraction-speed) <a href="#retraction-speed" id="retraction-speed"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `retraction_speed[extruder_idx]`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--retraction-speed=1`.\
Speed for retracting filament from the nozzle.

## Deretraction speed[¶](retraction.md#deretraction-speed) <a href="#deretraction-speed" id="deretraction-speed"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `deretraction_speed[extruder_idx]`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--deretraction-speed=1`.\
Speed for reloading filament into the nozzle. Zero means same speed of retraction.

## Travel distance threshold[¶](retraction.md#travel-distance-threshold) <a href="#travel-distance-threshold" id="travel-distance-threshold"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `retraction_minimum_travel[extruder_idx]`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--retraction-minimum-travel=1`.\
Only trigger retraction when the travel distance is longer than this threshold.

## Retract on layer change[¶](retraction.md#retract-on-layer-change) <a href="#retract-on-layer-change" id="retract-on-layer-change"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `retract_when_changing_layer[extruder_idx]`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Boolean list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--retract-when-changing-layer=1`.\
This forces a retraction on layer changes.

## Wipe while retracting[¶](retraction.md#wipe-while-retracting) <a href="#wipe-while-retracting" id="wipe-while-retracting"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `wipe[extruder_idx]`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Boolean list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--wipe=1`.\
This moves the nozzle along the last extrusion path when retracting to clean any leaked material on the nozzle. This can minimize blobs when printing a new part after traveling.

## Wipe distance[¶](retraction.md#wipe-distance) <a href="#wipe-distance" id="wipe-distance"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `wipe_distance[extruder_idx]`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--wipe-distance=1`.\
Describe how long the nozzle will move along the last path when retracting.\
Depending on how long the wipe operation lasts, how fast and long the extruder/filament retraction settings are, a retraction move may be needed to retract the remaining filament. Setting a value in the retract amount before wipe setting below will perform any excess retraction before the wipe, else it will be performed after.

## Retract amount before wipe[¶](retraction.md#retract-amount-before-wipe) <a href="#retract-amount-before-wipe" id="retract-amount-before-wipe"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `retract_before_wipe[extruder_idx]`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Percentage list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--retract-before-wipe=20%`.\
This is the length of fast retraction before a wipe, relative to retraction length.

## Retract amount after wipe[¶](retraction.md#retract-amount-after-wipe) <a href="#retract-amount-after-wipe" id="retract-amount-after-wipe"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Expert`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `retract_after_wipe[extruder_idx]`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Percentage list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--retract-after-wipe=20%`.

Important

NEW FEATURE: **Retract amount after wipe**\
Available in: [Nightly builds](https://github.com/OrcaSlicer/OrcaSlicer/releases/tag/nightly-builds) or Releases greater than **2.4.2**.

This is the length of fast retraction after a wipe, relative to retraction length.\
Together with [Retract amount before wipe](retraction.md#retract-amount-before-wipe), this lets you split the retraction across the wipe: some before, some after, and the remainder performed during the wipe move itself. The value is clamped by 100% minus the retract amount before wipe, so the two combined never exceed the total retraction length.\
Moving more of the retraction to after the wipe allows shorter wipe distances while keeping seams clean, which is helpful for high-detail models and stringing-prone filaments.

## Retraction When Switching Materials[¶](retraction.md#retraction-when-switching-materials) <a href="#retraction-when-switching-materials" id="retraction-when-switching-materials"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variables](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `retract_length_toolchange[extruder_idx]`, `retract_restart_extra_toolchange[extruder_idx]`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--retract-length-toolchange=1` (same pattern for the other variables above).\
Retraction settings specifically for material changes during tool changes in multi-material prints.

### Long retraction when cut (beta)[¶](retraction.md#long-retraction-when-cut-beta) <a href="#long-retraction-when-cut-beta" id="long-retraction-when-cut-beta"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Developer`.\
[Variables](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `long_retractions_when_cut[extruder_idx]`, `retraction_distances_when_cut[extruder_idx]`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb): `long_retractions_when_cut` (Boolean list), `retraction_distances_when_cut` (Float list).\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--long-retractions-when-cut=1` (`long_retractions_when_cut` shown; other variables above follow their own type).\
Experimental feature: Retracting and cutting off the filament at a longer distance during changes to minimize purge. While this reduces flush significantly, it may also raise the risk of nozzle clogs or other printing problems.
