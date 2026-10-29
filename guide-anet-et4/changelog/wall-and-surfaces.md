# Wall and surfaces¶

* [Walls printing order](wall-and-surfaces.md#walls-printing-order)
  * [Inner/Outer](wall-and-surfaces.md#innerouter)
  * [Inner/Outer/Inner](wall-and-surfaces.md#innerouterinner)
  * [Outer/Inner](wall-and-surfaces.md#outerinner)
  * [Narrow walls](wall-and-surfaces.md#narrow-walls)
  * [Print infill first](wall-and-surfaces.md#print-infill-first)
* [Wall loop direction](wall-and-surfaces.md#wall-loop-direction)
* [Surface flow ratio](wall-and-surfaces.md#surface-flow-ratio)
* [Only one wall](wall-and-surfaces.md#only-one-wall)
  * [Threshold](wall-and-surfaces.md#threshold)
* [Avoid crossing walls](wall-and-surfaces.md#avoid-crossing-walls)
  * [Max detour length](wall-and-surfaces.md#max-detour-length)
* [Small area flow compensation](wall-and-surfaces.md#small-area-flow-compensation)
  * [Flow Compensation Model](wall-and-surfaces.md#flow-compensation-model)

## Walls printing order[¶](wall-and-surfaces.md#walls-printing-order) <a href="#walls-printing-order" id="walls-printing-order"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `wall_sequence`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `Choice`.\
[Options](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `inner wall/outer wall, outer wall/inner wall, inner-outer-inner wall`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--wall-sequence="inner wall/outer wall"`.\
Print sequence of the internal (inner) and external (outer) walls.\
The order applies to each side of a wall on its own: the walls around a hole follow it just like the walls around the contour.

Note

Under an [Outer](/broken/pages/8f34753934cc3186e335ccb9927588ff743c306a#outer), [Outer and Inner](/broken/pages/8f34753934cc3186e335ccb9927588ff743c306a#outer-and-inner) or [Leading edge only](/broken/pages/8f34753934cc3186e335ccb9927588ff743c306a#leading-edge-only) brim, the first layer prints its outer walls first whatever this setting, so the brim runs straight on into the outer wall.\
[Auto](/broken/pages/8f34753934cc3186e335ccb9927588ff743c306a#auto), [Mouse Ears](/broken/pages/8f34753934cc3186e335ccb9927588ff743c306a#mouse-ears) and [Painted](/broken/pages/8f34753934cc3186e335ccb9927588ff743c306a#painted) brims may leave the outer walls bare, so they keep this order.

### Inner/Outer[¶](wall-and-surfaces.md#innerouter) <a href="#innerouter" id="innerouter"></a>

Use Inner/Outer for best overhangs. This is because the overhanging walls can adhere to a neighboring perimeter while printing. However, this option results in slightly reduced surface quality as the external perimeter is deformed by being squashed to the internal perimeter.

![inner-outer](<.gitbook/assets/inner outer.gif>)

### Inner/Outer/Inner[¶](wall-and-surfaces.md#innerouterinner) <a href="#innerouterinner" id="innerouterinner"></a>

Use Inner/Outer/Inner for the best external surface finish and dimensional accuracy as the external wall is printed undisturbed from an internal perimeter. However, overhang performance will reduce as there is no internal perimeter to print the external wall against. This option requires a minimum of 3 walls to be effective as it prints the internal walls from the 3rd perimeter onwards first, then the external perimeter and, finally, the first internal perimeter. This option is recommended over the Outer/Inner option in most cases.

![inner-outer-inner](<.gitbook/assets/inner outer inner.gif>)

* The first layer is printed [Inner/Outer](wall-and-surfaces.md#innerouter).
* Where a side has fewer than 3 walls there is nothing to print first, so that side is printed [Outer/Inner](wall-and-surfaces.md#outerinner).
* A wall too narrow for an inner wall on each side prints the hole first, see [Narrow walls](wall-and-surfaces.md#narrow-walls).

### Outer/Inner[¶](wall-and-surfaces.md#outerinner) <a href="#outerinner" id="outerinner"></a>

Use Outer/Inner for the same external wall quality and dimensional accuracy benefits of [Inner/Outer/Inner](wall-and-surfaces.md#innerouterinner) option. However, the Z seams will appear less consistent as the first extrusion of a new layer starts on a visible surface.

![outer-inner](<.gitbook/assets/outer inner.gif>)

### Narrow walls[¶](wall-and-surfaces.md#narrow-walls) <a href="#narrow-walls" id="narrow-walls"></a>

When a wall is too narrow for the walls of both its sides, like the wall of a thin tube, the contour and the hole share the room between them:

* **2 lines**: only the outer walls of the contour and the hole fit, touching each other. The hole's outer wall is printed first so the contour's leans on it, unless the order is [Outer/Inner](wall-and-surfaces.md#outerinner).
* **3 lines**: the two outer walls and one line between them. [Arachne](/broken/pages/54a6fe288c2767d758a6868ebef10f327f69163c#arachne) prints that line as an inner wall shared by both sides, and it follows the wall order like any other inner wall. [Inner/Outer/Inner](wall-and-surfaces.md#innerouterinner) has no 3rd wall to print first, so it prints the hole's outer wall, then the contour's, then the line between them.

For example, a tube with 0.5mm walls and 3 wall loops, with Arachne:

| Tube wall | Lines | Inner/Outer            | Outer/Inner            | Inner/Outer/Inner, after the first layer |
| --------- | ----- | ---------------------- | ---------------------- | ---------------------------------------- |
| 1mm       | 2     | hole, contour          | contour, hole          | hole, contour                            |
| 1.5mm     | 3     | middle, contour, hole  | contour, hole, middle  | hole, contour, middle                    |
| 2mm       | 4     | each side inner, outer | each side outer, inner | each side outer, inner                   |

[Classic](/broken/pages/54a6fe288c2767d758a6868ebef10f327f69163c#classic) fills the middle of a 3 line wall with [gap fill](/broken/pages/da1f51648c030aebc578bfec4de7c7b47ec7ddd2#apply-gap-fill) instead, printed after both outer walls, which keep the 2 line order.

### Print infill first[¶](wall-and-surfaces.md#print-infill-first) <a href="#print-infill-first" id="print-infill-first"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `is_infill_first`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--is-infill-first=1`.\
When this option is enabled, the [infill](/broken/pages/da1f51648c030aebc578bfec4de7c7b47ec7ddd2) and [top/bottom shells](/broken/pages/a93444d6bc5d3f832eed7be5e316e5e8f71eee5d) are printed first, followed by the walls. The first layer always prints the walls first, for better bed adhesion. This can be useful for some overhangs where the infill can support the walls.

![infill-first](<.gitbook/assets/infill first.gif>)

**However**, the infill will slightly push out the printed walls where it is attached to them, resulting in a worse external surface finish. It can also cause the infill to shine through the external surfaces of the part.

![infill-ghosting](<.gitbook/assets/infill ghosting.png>)

When using this option, it is recommended to use the [Precise Wall](/broken/pages/c70b83c3a32422c9168494b30baab0b5314ff4ad#precise-wall), [Inner/Outer/Inner](wall-and-surfaces.md#innerouterinner) wall printing order or reduce [Infill/Wall Overlap](/broken/pages/da1f51648c030aebc578bfec4de7c7b47ec7ddd2#infill-wall-overlap) to avoid the infill pushing out the external wall.

## Wall loop direction[¶](wall-and-surfaces.md#wall-loop-direction) <a href="#wall-loop-direction" id="wall-loop-direction"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `wall_direction`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `Choice`.\
[Options](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `ccw, cw`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--wall-direction=ccw`.\
The direction in which the **contour** wall loops are extruded when looking down from the top.\
Holes are printed in the opposite direction to the contour to maintain alignment with layers whose contour polygons are incomplete and change direction, also partially forming the contour of a hole. A hole whose outer wall touches the contour's with nothing between them, like a [narrow wall](wall-and-surfaces.md#narrow-walls) 2 lines wide, runs with the contour instead, so both walls are laid side by side in the same direction. Check [PR 12669](https://github.com/OrcaSlicer/OrcaSlicer/pull/12669) for more details about reversing hole direction.

The usage of [Reverse on even](/broken/pages/21eba2f54a17a4877cb2b14599233756a824a377#reverse-on-even) will reverse wall direction based on this setting.

Note

This option will be disabled if spiral vase mode is enabled.

## Surface flow ratio[¶](wall-and-surfaces.md#surface-flow-ratio) <a href="#surface-flow-ratio" id="surface-flow-ratio"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variables](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `print_flow_ratio`, `top_solid_infill_flow_ratio`, `bottom_solid_infill_flow_ratio`, `set_other_flow_ratios`, `first_layer_flow_ratio`, `outer_wall_flow_ratio`, `inner_wall_flow_ratio`, `overhang_flow_ratio`, `sparse_infill_flow_ratio`, `internal_solid_infill_flow_ratio`, `gap_fill_flow_ratio`, `support_flow_ratio`, `support_interface_flow_ratio`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float` — every variable above except `set_other_flow_ratios`, which is a [Boolean](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean) enable toggle for all the others (`--set-other-flow-ratios=1`).\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--print-flow-ratio=1` (same pattern for the other Float variables above).\
The Flow ratio (`print_flow_ratio`) scales all extrusion flow of the object proportionally.

The top and bottom surface flow ratios affect the amount of material for [top or bottom solid infill](/broken/pages/a93444d6bc5d3f832eed7be5e316e5e8f71eee5d). You can decrease them slightly to get a smoother surface finish.\
The actual top or bottom surface flow used is calculated by multiplying this value by the [filament flow ratio](/broken/pages/4da0e8a2d1390e2f4166da4f6cca2f83837a3bb6#flow-ratio), and if set, the object's flow ratio.

Other flow ratios, such as ratios for the first layer (does not affect brims and skirts), outer and inner walls, overhang perimeters, sparse infill, internal solid infill, gap fill, support, and support interfaces, can also be adjusted after enabling the "Set other flow ratios" option.

Tip

Before using a value other than 1, it is recommended to [calibrate the flow ratio](/broken/pages/de2365cb9daaa98d9ad3608097376a29f2371e9c) to ensure that the flow ratio is set correctly for your printer and filament.

## Only one wall[¶](wall-and-surfaces.md#only-one-wall) <a href="#only-one-wall" id="only-one-wall"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Simple`.\
[Variables](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `only_one_wall_first_layer`, `only_one_wall_top`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--only-one-wall-first-layer=1` (same pattern for the other variables above).\
Use only one wall on flat surfaces, to give more space to the [top infill pattern](/broken/pages/a93444d6bc5d3f832eed7be5e316e5e8f71eee5d#surface-pattern). Especially useful in small features, like letters, where the top surface is very small and [concentric pattern](/broken/pages/a147f0b85dea1cbf1cf61adb81420a35f687c13f#concentric) from walls would not cover it properly.

![only-one-wall](<.gitbook/assets/only one wall.gif>)

Each option needs the shell it acts on, so they are only available when the matching [Shell Layers](/broken/pages/a93444d6bc5d3f832eed7be5e316e5e8f71eee5d#shell-layers) is greater than 0: without a top shell there is no top surface for the top option to act on, and the same applies to the first layer and the bottom shell.

Tip

See [Surface Expansion and Only One Wall](/broken/pages/a93444d6bc5d3f832eed7be5e316e5e8f71eee5d#surface-expansion-and-only-one-wall) for how the inner walls are handled over an expanded top surface when using more than one wall.

### Threshold[¶](wall-and-surfaces.md#threshold) <a href="#threshold" id="threshold"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `min_width_top_surface`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float or Percentage`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--min-width-top-surface=20%`.\
If a top surface has to be printed and it's partially covered by another layer, it won't be considered as a top layer where its width is below this value. This can be useful to keep _Only one wall on top surfaces_ from triggering on surfaces that should be covered only by walls.\
This value can be in mm or a % of the inner wall line width.

![only-one-wall-threshold](<.gitbook/assets/only one wall threshold.png>)

Warning

If enabled, artifacts can be created if you have some thin features on the next layer, like letters. Set this setting to 0 to remove these artifacts.

## Avoid crossing walls[¶](wall-and-surfaces.md#avoid-crossing-walls) <a href="#avoid-crossing-walls" id="avoid-crossing-walls"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `reduce_crossing_wall`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--reduce-crossing-wall=1`.\
This option instructs the slicer to avoid crossing perimeters (walls) during travel moves.\
Instead of traveling directly through a wall, the print head will detour around it, which can significantly reduce surface defects and stringing.

While this increases print time slightly, the improvement in print quality, especially with materials prone to stringing like **PETG** or **TPU**, often justifies the trade-off.\
Highly recommended for detailed or aesthetic prints.

![avoid-crossing-walls](<.gitbook/assets/avoid crossing walls.png>)

### Max detour length[¶](wall-and-surfaces.md#max-detour-length) <a href="#max-detour-length" id="max-detour-length"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `max_travel_detour_distance`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float or Percentage`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--max-travel-detour-distance=20%`.\
Defines the maximum distance the printer is allowed to detour to avoid crossing a wall. Can be set as:

* **Absolute value in millimeters:** exactly how far the detour can extend (e.g., `5mm`).
* **Percentage** of the direct travel path (e.g., `50%`).
* **0** disables the **limit** and allows detours of **any length**.

Use this setting to balance print time and wall quality: longer detours mean fewer wall crossings but slower prints.

## Small area flow compensation[¶](wall-and-surfaces.md#small-area-flow-compensation) <a href="#small-area-flow-compensation" id="small-area-flow-compensation"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variables](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `small_area_infill_flow_compensation`, `small_area_infill_flow_compensation_model`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb): `small_area_infill_flow_compensation` (Boolean), `small_area_infill_flow_compensation_model` (Text list).\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--small-area-infill-flow-compensation=1` (`small_area_infill_flow_compensation` shown; other variables above follow their own type).\
Enables adaptive flow control for small infill areas. This feature helps address extrusion problems that often occur in small regions of solid infill, such as the tops of narrow letters or fine features.\
In these cases, standard extrusion flow may be too much for the available space, leading to over-extrusion or poor surface quality.

![flow-compensation-model](<.gitbook/assets/flow compensation model.png>)

It works by dynamically adjusting the extrusion flow based on the length of the extrusion path, ensuring more precise material deposition in small spaces.

The compensation only applies to internal solid infill, top surfaces and first layer bottom surfaces, and only when that surface uses the [Rectilinear](/broken/pages/a147f0b85dea1cbf1cf61adb81420a35f687c13f#rectilinear), [Aligned Rectilinear](/broken/pages/a147f0b85dea1cbf1cf61adb81420a35f687c13f#aligned-rectilinear), [Monotonic](/broken/pages/a147f0b85dea1cbf1cf61adb81420a35f687c13f#monotonic) or [Monotonic line](/broken/pages/a147f0b85dea1cbf1cf61adb81420a35f687c13f#monotonic-line) pattern.

This is a native implementation of @Alexander-T-Moss's [Small Area Flow Compensation](https://github.com/Alexander-T-Moss/Small-Area-Flow-Comp).

### Flow Compensation Model[¶](wall-and-surfaces.md#flow-compensation-model) <a href="#flow-compensation-model" id="flow-compensation-model"></a>

The model uses a list of Extrusion Length and Flow Correction Factor value pairs. Each pair defines how much flow should be used for a specific Extrusion Length.\
For values between the listed points, the flow follows a smooth curve through them (PCHIP interpolation), which never overshoots the listed values.

![flow-compensation-model-graph](<.gitbook/assets/flow compensation model graph.png>)

For example, for the following model:

| Extrusion Length | Flow Correction Factor |
| ---------------- | ---------------------- |
| 0                | 0                      |
| 0.2              | 0.4444                 |
| 0.4              | 0.6145                 |
| 0.6              | 0.7059                 |
| 0.8              | 0.7619                 |
| 1.5              | 0.8571                 |
| 2                | 0.8889                 |
| 3                | 0.9231                 |
| 5                | 0.952                  |
| 10               | 1                      |

You should write it as:

```
0,0;
0.2,0.4444;
0.4,0.6145;
0.6,0.7059;
0.8,0.7619;
1.5,0.8571;
2,0.8889;
3,0.9231;
5,0.9520;
10,1;
```
