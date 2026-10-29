# Prime Tower¶

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Simple`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `enable_prime_tower`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--enable-prime-tower=1`.\
The prime tower can be used to clean up residue on the nozzle and stabilize the chamber pressure inside the nozzle, in order to avoid appearance defects when printing objects.

Note

Some settings on this page depend on the printer's [Wipe tower type](/broken/pages/74f57ccd9ce07fa1f5a18d2766d92d9e5cb458ca). Bambu Lab printers always use the Type 1 tower. [Wipe Tower Rotation Angle](prime-tower.md#wipe-tower-rotation-angle), [Maximal bridging distance](prime-tower.md#maximal-bridging-distance), [Wipe tower purge lines spacing](prime-tower.md#wipe-tower-purge-lines-spacing), [Extra flow for purge](prime-tower.md#extra-flow-for-purge), [Maximum wipe tower print speed](prime-tower.md#maximum-wipe-tower-print-speed) and [Stabilization cone apex angle](prime-tower.md#stabilization-cone-apex-angle) are only shown with the Type 2 tower.

## Skip points[¶](prime-tower.md#skip-points) <a href="#skip-points" id="skip-points"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `prime_tower_skip_points`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--prime-tower-skip-points=1`.

Important

NEW FEATURE: **Skip points on the Type 2 prime tower**\
Available in: [Nightly builds](https://github.com/OrcaSlicer/OrcaSlicer/releases/tag/nightly-builds) or Releases greater than **2.4.2**.

Leaves a short gap in the outer wall of the prime tower where each tool change starts its purge, so the nozzle enters the tower through the gap instead of crossing the printed wall. Enabled by default. It has no effect on the [Cone](prime-tower.md#cone) wall of the Type 2 tower.

## Enable tower interface features[¶](prime-tower.md#enable-tower-interface-features) <a href="#enable-tower-interface-features" id="enable-tower-interface-features"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `enable_tower_interface_features`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--enable-tower-interface-features=1`.\
Changes how the prime tower is printed on interface layers, where different materials meet. On these layers the nozzle is heated to the filament's **Interface layer print temperature** (its maximum recommended nozzle temperature when set to -1), and extra filament can be pre-extruded before the purge. These values are set per filament in [Multimaterial Wipe Tower Parameters](/broken/pages/0c30c80c95069c94ac293993ffa3b80233b02819#multimaterial-wipe-tower-parameters).

The Type 1 tower applies this on the layers where a material category starts or stops being printed on the tower. The Type 2 tower applies it on every layer with a filament change, and also adds the filament's **Interface layer purge length** to the purge.

### Cool down from interface boost during prime tower[¶](prime-tower.md#cool-down-from-interface-boost-during-prime-tower) <a href="#cool-down-from-interface-boost-during-prime-tower" id="cool-down-from-interface-boost-during-prime-tower"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `enable_tower_interface_cooldown_during_tower`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--enable-tower-interface-cooldown-during-tower=1`.\
Only shown when [Enable tower interface features](prime-tower.md#enable-tower-interface-features) is enabled, and only used by the Type 2 tower. After heating to the interface temperature, the nozzle is set back to its print temperature at the start of the purge, so it cools down while the tower is printed. When disabled, the print temperature is restored only after the purge is finished.

## Internal ribs[¶](prime-tower.md#internal-ribs) <a href="#internal-ribs" id="internal-ribs"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `prime_tower_enable_framework`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--prime-tower-enable-framework=1`.\
Adds internal ribs to increase the stability of the prime tower. Only used by the Type 1 tower, where each purge section of the tower keeps its full size up to the top instead of shrinking on upper layers that need less purging.

## Width[¶](prime-tower.md#width) <a href="#width" id="width"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Simple`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `prime_tower_width`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--prime-tower-width=1`.\
Width of the prime tower.

## Prime volume[¶](prime-tower.md#prime-volume) <a href="#prime-volume" id="prime-volume"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Simple`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `prime_volume`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--prime-volume=1`.\
Volume of material, in mm³, printed on the prime tower after each tool change to prime the new extruder. Default is 45 mm³.

Unless the printer is a single extruder multi-material printer with [Purge in prime tower](/broken/pages/74f57ccd9ce07fa1f5a18d2766d92d9e5cb458ca#purge-in-prime-tower) enabled, the Type 2 tower purges this fixed volume at each tool change instead of the flushing volumes. On such printers the tower purges the flushing volumes and this option is hidden. The Type 1 tower takes the prime volume from each filament profile and uses this value only as a fallback.

## Brim width[¶](prime-tower.md#brim-width) <a href="#brim-width" id="brim-width"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `prime_tower_brim_width`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--prime-tower-brim-width=1`.\
Width of the brim around the prime tower.

## Infill gap[¶](prime-tower.md#infill-gap) <a href="#infill-gap" id="infill-gap"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `prime_tower_infill_gap`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Percentage`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--prime-tower-infill-gap=20%`.\
Spacing of the purge lines on the Type 1 prime tower, as a percentage of the line width. At 100% the lines are placed right next to each other; higher values leave gaps between them and make the tower larger for the same purge volume. Default is 150%.

The Type 2 tower ignores it and uses [Wipe tower purge lines spacing](prime-tower.md#wipe-tower-purge-lines-spacing) instead.

## Wipe Tower Rotation Angle[¶](prime-tower.md#wipe-tower-rotation-angle) <a href="#wipe-tower-rotation-angle" id="wipe-tower-rotation-angle"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `wipe_tower_rotation_angle`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--wipe-tower-rotation-angle=1`.\
Wipe tower rotation angle with respect to the X axis.

## Maximal bridging distance[¶](prime-tower.md#maximal-bridging-distance) <a href="#maximal-bridging-distance" id="maximal-bridging-distance"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `wipe_tower_bridging`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--wipe-tower-bridging=1`.\
Maximal distance between supports on sparse infill sections.

## Wipe tower purge lines spacing[¶](prime-tower.md#wipe-tower-purge-lines-spacing) <a href="#wipe-tower-purge-lines-spacing" id="wipe-tower-purge-lines-spacing"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `wipe_tower_extra_spacing`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Percentage`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--wipe-tower-extra-spacing=20%`.\
Spacing of purge lines on the wipe tower.

## Extra flow for purge[¶](prime-tower.md#extra-flow-for-purge) <a href="#extra-flow-for-purge" id="extra-flow-for-purge"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `wipe_tower_extra_flow`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Percentage`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--wipe-tower-extra-flow=20%`.\
Extra flow used for the purging lines on the wipe tower. This makes the purging lines thicker than they normally would be. The spacing is adjusted automatically.

## Maximum wipe tower print speed[¶](prime-tower.md#maximum-wipe-tower-print-speed) <a href="#maximum-wipe-tower-print-speed" id="maximum-wipe-tower-print-speed"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `wipe_tower_max_purge_speed`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--wipe-tower-max-purge-speed=1`.\
The maximum print speed when purging in the wipe tower and printing the wipe tower sparse layers. When purging, if the sparse infill speed or calculated speed from the filament max volumetric speed is lower, the lowest will be used instead.\
When printing the sparse layers, if the sparse infill speed or calculated speed from the filament max volumetric speed is lower, the lowest will be used instead.\
Increasing this speed may affect the tower's stability as well as increase the force with which the nozzle collides with any blobs that may have formed on the wipe tower.\
Before increasing this parameter beyond the default of 90 mm/s, make sure your printer can reliably bridge at the increased speeds and that ooze when tool changing is well controlled.\
The wipe tower external perimeters use the inner wall speed, also limited by this setting.

## Wall type[¶](prime-tower.md#wall-type) <a href="#wall-type" id="wall-type"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `wipe_tower_wall_type`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `Choice`.\
[Options](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `rectangle, cone, rib`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--wipe-tower-wall-type=rectangle`.\
Wipe tower outer wall type.

### Rectangle[¶](prime-tower.md#rectangle) <a href="#rectangle" id="rectangle"></a>

A rectangle with fixed width and height.

### Cone[¶](prime-tower.md#cone) <a href="#cone" id="cone"></a>

A cone with a fillet at the bottom to help stabilize the wipe tower. Only the Type 2 tower builds the cone. The Type 1 tower prints a rectangle instead, and on Bambu Lab printers Orca switches this option back to Rectangle.

#### Stabilization cone apex angle[¶](prime-tower.md#stabilization-cone-apex-angle) <a href="#stabilization-cone-apex-angle" id="stabilization-cone-apex-angle"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `wipe_tower_cone_angle`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--wipe-tower-cone-angle=1`.\
Angle at the apex of the cone that is used to stabilize the wipe tower. A larger angle means a wider base.

### Rib[¶](prime-tower.md#rib) <a href="#rib" id="rib"></a>

The default wall type. Adds four ribs to the tower wall for enhanced stability and makes the tower square, so [Width](prime-tower.md#width) cannot be set.

#### Extra rib length[¶](prime-tower.md#extra-rib-length) <a href="#extra-rib-length" id="extra-rib-length"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `wipe_tower_extra_rib_length`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--wipe-tower-extra-rib-length=1`.\
Positive values can increase the size of the rib wall, while negative values can reduce the size. However, the size of the rib wall cannot be smaller than that determined by the purge volume.

#### Rib width[¶](prime-tower.md#rib-width) <a href="#rib-width" id="rib-width"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `wipe_tower_rib_width`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--wipe-tower-rib-width=1`.\
Width of the rib wall.

#### Fillet wall[¶](prime-tower.md#fillet-wall) <a href="#fillet-wall" id="fillet-wall"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `wipe_tower_fillet_wall`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--wipe-tower-fillet-wall=1`.\
Rounds the corners of the prime tower's rib wall.

## No sparse layers[¶](prime-tower.md#no-sparse-layers) <a href="#no-sparse-layers" id="no-sparse-layers"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `wipe_tower_no_sparse_layers`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--wipe-tower-no-sparse-layers=1`.

Important

NEW FEATURE: **No sparse layers on every prime tower type**\
Available in: [Nightly builds](https://github.com/OrcaSlicer/OrcaSlicer/releases/tag/nightly-builds) or Releases greater than **2.4.2**.

If enabled, the prime tower is not printed on layers with no tool changes. The tower therefore stays low while the model keeps rising, and on the next layer that does have a tool change the extruder travels back down to print it.

Because the tower ends up below the model, the toolhead has to reach down to it past everything already printed. Orca checks the plate for that before slicing and rejects layouts where the nozzle, the toolhead body or the gantry rod would hit an object, highlighting the collision area and the height limit it would exceed. Move the model further from the tower, lower its height, or turn this option off.

Tip

If the plate layout can't avoid a collision, [Combine sparse layers](prime-tower.md#combine-sparse-layers) also cuts the time spent on sparse tower layers while keeping the tower level with the model.

Note

This option has no effect when [smooth timelapse](/broken/pages/e792de15ca89fe7bca7e8654ec76e5852fdd584b#timelapse) or [clumping detection](/broken/pages/e792de15ca89fe7bca7e8654ec76e5852fdd584b#enable-clumping-detection) is enabled, because both keep every sparse layer of the tower. Enabling it while smooth timelapse is selected switches timelapse to traditional, and selecting smooth timelapse turns this option off.

## Combine sparse layers[¶](prime-tower.md#combine-sparse-layers) <a href="#combine-sparse-layers" id="combine-sparse-layers"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `wipe_tower_sparse_layers_combination`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--wipe-tower-sparse-layers-combination=1`.

Important

NEW FEATURE: **Combine sparse prime tower layers**\
Available in: [Nightly builds](https://github.com/OrcaSlicer/OrcaSlicer/releases/tag/nightly-builds) or Releases greater than **2.4.2**.

If enabled, consecutive layers on which the prime tower has no filament change (sparse layers) are printed as a single thicker tower layer instead of one thin layer each, the same way [Infill Combination](/broken/pages/def49ed4375ccd47ffeb8694997bbd8dc609e159#infill-combination) merges sparse infill. The merged layer is printed on the last layer of the run, at the combined height of all the layers it covers, and the layers below it skip the tower entirely.

This removes most of the travel moves to the tower on sparse layers, which shortens print time. It saves less than [No sparse layers](prime-tower.md#no-sparse-layers), but the tower keeps rising with the model, so the toolhead never has to reach down to it: there is no collision risk and no restriction on the plate layout.

Layers are merged following these rules:

* Only whole layers are merged, so a merged layer always ends at an object layer height.
* The merged height never exceeds the maximum layer height of the nozzle printing the tower (see [Extruder Layer Height Limits](/broken/pages/54fc4ba47d549303cf6c193b25f9585c9e1bda1e#extruder-layer-height-limits)), or three quarters of the nozzle diameter when that limit is set to 0.
* Layers with a filament change are never merged, so every purge is still printed at its own height.
* The first layer is never merged.

Tip

At least two layers have to fit under the maximum layer height before anything is merged, so this option has no effect at common layer heights. For example, with a 0.3 mm maximum layer height, 0.2 mm layers are not merged (2 × 0.2 mm = 0.4 mm), while 0.1 mm layers are merged three at a time (3 × 0.1 mm = 0.3 mm). Use a lower layer height or raise the extruder's maximum layer height to benefit from it.

Note

This option is only shown when [No sparse layers](prime-tower.md#no-sparse-layers) is disabled, since dropping the sparse layers leaves nothing to combine. It also has no effect when [smooth timelapse](/broken/pages/e792de15ca89fe7bca7e8654ec76e5852fdd584b#timelapse) or [clumping detection](/broken/pages/e792de15ca89fe7bca7e8654ec76e5852fdd584b#enable-clumping-detection) is enabled, because both keep every sparse layer of the tower.

## Prime all printing extruders[¶](prime-tower.md#prime-all-printing-extruders) <a href="#prime-all-printing-extruders" id="prime-all-printing-extruders"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `single_extruder_multi_material_priming`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--single-extruder-multi-material-priming=1`.\
If enabled, all extruders used in the print are primed at the start of the print, before the first layer, by printing a short purge area for each of them side by side along the front edge of the bed. Only shown for printers using the Type 2 tower, and hidden when [Single Extruder Multi Material](/broken/pages/52afbee52364e39d301d42c21756fa3e40fe2f57#single-extruder-multi-material) is enabled.

With Marlin firmware, the printer beeps and pauses after priming: if the print overlaps the priming area, it waits for you to remove the priming extrusions, otherwise it continues after 10 seconds. With other firmware, Orca warns when the print is too close to the priming area.

## Belt purge tower width[¶](prime-tower.md#belt-purge-tower-width) <a href="#belt-purge-tower-width" id="belt-purge-tower-width"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `belt_purge_tower_width`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--belt-purge-tower-width=1`.

Important

NEW FEATURE: **Belt purge tower**\
Available in: [Nightly builds](https://github.com/OrcaSlicer/OrcaSlicer/releases/tag/nightly-builds) or Releases greater than **2.4.2**.

Sets the width of the [belt purge tower](/broken/pages/74f57ccd9ce07fa1f5a18d2766d92d9e5cb458ca#belt-purge-tower), measured across the belt. This tower replaces the prime tower on belt printers. The setting is shown when the belt purge tower is enabled in the printer settings.

Only the width is set here. The length follows the printed parts along the belt, and the height is calculated from the maximum purge volume required in a single layer. Increasing the width therefore reduces the tower's height.
