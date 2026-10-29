# Special Mode¶

These settings control advanced slicing and printing behaviors, such as how layers are processed, object printing order, and special effects like spiral vase mode.

* [Slicing Mode](special-mode.md#slicing-mode)
  * [Regular](special-mode.md#regular)
  * [Close Holes](special-mode.md#close-holes)
  * [Even Odd](special-mode.md#even-odd)
* [Print Sequence](special-mode.md#print-sequence)
  * [By Layer](special-mode.md#by-layer)
  * [By Object](special-mode.md#by-object)
* [Intra-layer order](special-mode.md#intra-layer-order)
* [Spiral vase](special-mode.md#spiral-vase)
  * [Smooth Spiral](special-mode.md#smooth-spiral)
    * [Max XY Smoothing](special-mode.md#max-xy-smoothing)
  * [Spiral starting flow ratio](special-mode.md#spiral-starting-flow-ratio)
  * [Spiral finishing flow ratio](special-mode.md#spiral-finishing-flow-ratio)
* [Timelapse](special-mode.md#timelapse)
* [Enable clumping detection](special-mode.md#enable-clumping-detection)

## Slicing Mode[¶](special-mode.md#slicing-mode) <a href="#slicing-mode" id="slicing-mode"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `slicing_mode`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `Choice`.\
[Options](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `regular, even_odd, close_holes`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--slicing-mode=regular`.\
The slicing mode determines how the outlines found in each layer of the model are interpreted as solid areas or holes. Different modes can be used for models that need special handling.

### Regular[¶](special-mode.md#regular) <a href="#regular" id="regular"></a>

This is the default slicing mode. It slices the model layer by layer, generating G-code for each layer.\
Use this for most prints where no special modifications are needed.

### Close Holes[¶](special-mode.md#close-holes) <a href="#close-holes" id="close-holes"></a>

Use "Close holes" to automatically close all holes in the model during slicing in the XY plane.\
Every hole in each layer's slices is filled, so the model prints solid inside its outer outlines, including holes that are meant to stay open. This is useful for models whose holes should be solid, such as meshes where internal surfaces or openings are modeling artifacts.

![close-holes](<.gitbook/assets/close holes.png>)

### Even Odd[¶](special-mode.md#even-odd) <a href="#even-odd" id="even-odd"></a>

Use "Even-odd" for specific models like [3DLabPrint](https://3dlabprint.com/) airplane models. In this mode, nested outlines alternate between solid areas and holes (the even-odd fill rule), which may be required for certain proprietary or experimental prints.

## Print Sequence[¶](special-mode.md#print-sequence) <a href="#print-sequence" id="print-sequence"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Simple`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `print_sequence`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `Choice`.\
[Options](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `by layer, by object`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--print-sequence="by layer"`.\
This setting controls how multiple objects are printed in a single print job.

### By Layer[¶](special-mode.md#by-layer) <a href="#by-layer" id="by-layer"></a>

This option prints all objects layer by layer, one layer at a time. This is the default and works well for most multi-part prints.

### By Object[¶](special-mode.md#by-object) <a href="#by-object" id="by-object"></a>

This option prints each object completely before moving on to the next object. This is better for prints where objects need to cool separately or when using different materials per object, but it may increase total print time.

This setting requires more space between models and may not be suitable for all print scenarios.

Objects are printed in the order of the object list. See **As object list** in [Intra-layer order](special-mode.md#intra-layer-order) to change that order.

## Intra-layer order[¶](special-mode.md#intra-layer-order) <a href="#intra-layer-order" id="intra-layer-order"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `print_order`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `Choice`.\
[Options](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `default, as_obj_list, best_of, snake`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--print-order=default`.\
Determines the order in which object instances are visited within a single layer, which controls how much travel is spent moving between them.

Shorter, more cyclic paths reduce oozing and avoid dragging the nozzle over parts that have already been printed, which can make [Z Hop](/broken/pages/dc18322a6319f10648e1a1374e7cae7f8bb073ca) and [Avoid crossing walls](/broken/pages/8737adce37259a727713a40d86d1257eda155156#avoid-crossing-walls) unnecessary in many plates.

Important

NEW FEATURE: **Snake and Best of all (shortest path) intra-layer ordering**\
Available in: [Nightly builds](https://github.com/OrcaSlicer/OrcaSlicer/releases/tag/nightly-builds) or Releases greater than **2.4.2**.

* **Default**: Up to ten instances or islands are visited along the shortest possible closed path. Larger sets use nearest-neighbor chaining, refined by reversing sections of the path (2-opt), moving short runs of stops elsewhere (or-opt) and removing crossings. A good general choice and the recommended option for most plates.
*   **As object list**: Instances are printed in the same order as the object list, without any path optimization. Use it when you need a predictable, manually controlled order, for custom sequencing or debugging. [By Object](special-mode.md#by-object) also prints in this order.

    > \[!IMPORTANT] NEW FEATURE: **Order By in the plate menu**\
    > Available in: [Nightly builds](https://github.com/OrcaSlicer/OrcaSlicer/releases/tag/nightly-builds) or Releases greater than **2.4.2**.

    To change the order of the object list:

    * Drag an object to a new position inside its plate in the object list.
    * Right-click a plate, in the object list or in the 3D view, and choose **Order By** > **Name**, **Filament**, **Height** or **Size**. **Order By** > **All Plates** sorts the objects of every plate.

    Each sort is ascending. If the objects are already in that order, it reverses them, so choosing the same entry twice gives the descending order. **Name** puts "Part 2" before "Part 10", **Height** compares the top of each object, and **Size** compares the volume of its bounding box. Objects with the same value keep their current order, so an order you made by dragging stays inside each group. Undo restores the previous order.

    > \[!TIP]
    >
    > * **Order By** > **Height** prints the tallest object last. With [By Object](special-mode.md#by-object), only the last object can use the full [Printable height](/broken/pages/0d906d45479df31a3f89c370bdbfa417919f98de#printable-height). The objects before it must stay below the extruder clearance [Height to lid](/broken/pages/9bc9ed5059270cf6d62284013cea21d2495ad10d#height-to-lid) or [Height to rod](/broken/pages/9bc9ed5059270cf6d62284013cea21d2495ad10d#height-to-rod). An object reported as too tall may slice once it prints last.
    > * **Order By** > **Filament** prints the objects of each filament one after another, which saves filament changes with [By Object](special-mode.md#by-object).
* **Snake**: Serpentine, row-by-row traversal (objects are grouped into rows and each row is traversed in the opposite direction to the previous one), refined with 2-opt. Well suited to regular grids of many small parts.
* **Best of all (shortest path)**: Every strategy is evaluated and the shortest one is used. The object instance order is decided once for the whole print, while the ordering of individual islands is decided per layer, so different layers may end up using different strategies. Slightly slower to slice.

Note

Except with **As object list**, ordering is applied at the island level, not only per instance, so each separate region of a layer is ordered individually. This mainly benefits assemblies and objects whose layers overlap.

Inside each island, the infill, ironing and support paths are also printed in a short order, whatever this setting: up to eight paths in the shortest possible order, more by refining a nearest-neighbor chain. Paths that must keep their direction, such as [Grid](/broken/pages/a147f0b85dea1cbf1cf61adb81420a35f687c13f#grid) infill, are only reordered.

With multiple filaments or tools in the same layer, minimizing tool changes takes priority: objects are grouped by filament first, and this setting only orders the instances within each filament group. The overall sequence may therefore not look like the shortest path across the plate.

## Spiral vase[¶](special-mode.md#spiral-vase) <a href="#spiral-vase" id="spiral-vase"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Simple`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `spiral_mode`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--spiral-mode=1`.\
Spiral vase mode transforms a solid model into a single-walled print with solid bottom layers, eliminating seams by continuously spiraling the outer contour.\
This creates a smooth, vase-like appearance.

### Smooth Spiral[¶](special-mode.md#smooth-spiral) <a href="#smooth-spiral" id="smooth-spiral"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Simple`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `spiral_mode_smooth`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--spiral-mode-smooth=1`.\
When enabled, Smooth Spiral smooths out X and Y moves as well, resulting in no visible seams even on non-vertical walls.\
This produces the smoothest possible spiral print.

Note

If you are using absolute E distances, the smoothing may not work as expected.

#### Max XY Smoothing[¶](special-mode.md#max-xy-smoothing) <a href="#max-xy-smoothing" id="max-xy-smoothing"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `spiral_mode_max_xy_smoothing`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float or Percentage`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--spiral-mode-max-xy-smoothing=20%`.\
Maximum distance to move points in XY to achieve a smooth spiral. If expressed as a percentage, it is calculated relative to the nozzle diameter.\
Higher values allow more smoothing but may distort the model slightly.

### Spiral starting flow ratio[¶](special-mode.md#spiral-starting-flow-ratio) <a href="#spiral-starting-flow-ratio" id="spiral-starting-flow-ratio"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `spiral_starting_flow_ratio`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--spiral-starting-flow-ratio=1`.\
Sets the starting flow ratio when transitioning from the last bottom layer to the spiral.\
Normally, the flow scales from 0% to 100% during the first loop, which can sometimes cause under-extrusion at the start.\
Adjust this to fine-tune the transition and prevent issues. Only applied when [Use relative E distances](/broken/pages/eeff389a3bf7caa2aee6f13fbffe1d91ee4800d4#use-relative-e-distances) is enabled.

### Spiral finishing flow ratio[¶](special-mode.md#spiral-finishing-flow-ratio) <a href="#spiral-finishing-flow-ratio" id="spiral-finishing-flow-ratio"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `spiral_finishing_flow_ratio`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--spiral-finishing-flow-ratio=1`.\
Sets the finishing flow ratio when ending the spiral. Normally, the flow scales from 100% to 0% during the last loop, which can lead to under-extrusion at the end.\
Use this to control the ending and ensure consistent extrusion. Only applied when [Use relative E distances](/broken/pages/eeff389a3bf7caa2aee6f13fbffe1d91ee4800d4#use-relative-e-distances) is enabled.

## Timelapse[¶](special-mode.md#timelapse) <a href="#timelapse" id="timelapse"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Simple`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `timelapse_type`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `Choice`.\
[Options](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `0, 1`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--timelapse-type=0`.\
Selects how the printer's camera takes the snapshots for a timelapse video. A snapshot is taken after each layer, and the snapshots are combined into a video when the print finishes. Recording itself is turned on with the **Timelapse** option of the print dialog when sending the job to the printer.

This option is only shown for Bambu Lab printers. The moves and camera commands for each snapshot come from the printer's [Timelapse G-code](/broken/pages/8a0cca48a8cb689eb2e37db1bc877c26189bf981#timelapse-g-code), which is inserted once per layer. On other printers, add your own snapshot commands to that G-code.

* **Traditional**: The snapshot is taken without a prime tower. Whether the toolhead stays where it is or moves out of the way for the snapshot depends on the printer's Timelapse G-code.
* **Smooth**: After each layer, the toolhead moves to the excess chute and the snapshot is taken there. The next layer then starts by printing the prime tower, which wipes off any filament that leaked from the nozzle during the snapshot before the model is printed.

Note

Smooth mode requires a [prime tower](/broken/pages/5aa3302c55047356a98465bb114707e629d121d9), which is printed on every layer, even when the plate uses a single filament. Without it, the model may show flaws.

* Selecting Smooth while the prime tower is disabled offers to enable it, and disabling the prime tower while Smooth is selected asks for confirmation.
* Selecting Smooth turns off [No sparse layers](/broken/pages/5aa3302c55047356a98465bb114707e629d121d9#no-sparse-layers), and enabling No sparse layers switches timelapse back to Traditional.
* Smooth is not supported with the [By Object](special-mode.md#by-object) print sequence when the plate has more than one object.

[Spiral vase](special-mode.md#spiral-vase) mode requires Traditional. On printers with an i3 structure, such as the Bambu Lab A1 and A1 mini, no timelapse video is generated in spiral vase mode, and Traditional timelapse is not supported with the By Object print sequence.

## Enable clumping detection[¶](special-mode.md#enable-clumping-detection) <a href="#enable-clumping-detection" id="enable-clumping-detection"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `enable_wrapping_detection`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--enable-wrapping-detection=1`.\
Lets the printer check, by probing, whether filament has clumped around the nozzle during the first layers of the print. When enabled, the printer's [Clumping detection G-code](/broken/pages/8a0cca48a8cb689eb2e37db1bc877c26189bf981#clumping-detection-g-code) is inserted on each layer, and the Bambu Lab profiles run the check on a few of the early layers.

This option is only shown for printers that support it, currently the Bambu Lab H2D, H2D Pro, H2C and P2S. It is turned off when switching to a printer that does not support it.

* **Prime tower**: Clumping detection requires a [prime tower](/broken/pages/5aa3302c55047356a98465bb114707e629d121d9), which is printed even when the plate uses a single filament. Enabling the option while the prime tower is disabled asks for confirmation, and slicing without a prime tower shows a warning, as the model may show flaws.
* **Detection area**: The printer profile defines an area of the bed that is used for probing. While the option is enabled, this area is shown on the plate and kept free when arranging, and slicing stops with an error if an object or the prime tower overlaps it.
* **Incompatible settings**: Not supported with the [By Object](special-mode.md#by-object) print sequence when the plate has more than one object, and turned off when [Spiral vase](special-mode.md#spiral-vase) mode is enabled. [No sparse layers](/broken/pages/5aa3302c55047356a98465bb114707e629d121d9#no-sparse-layers) has no effect while it is enabled.
