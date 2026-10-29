# Machine Frame Transforms¶

Important

NEW FEATURE: **Belt printer support**\
Available in: [Nightly builds](https://github.com/OrcaSlicer/OrcaSlicer/releases/tag/nightly-builds) or Releases greater than **2.4.2**.

![belt\_machine\_frame\_transforms](.gitbook/assets/belt_machine_frame_transforms.png)

These settings convert OrcaSlicer's coordinates into machine coordinates for a belt printer. They are found in **Printer settings → Basic information → Machine frame transforms** and are shown when [belt printing](/broken/pages/00dcd987ac21f7e44ecf650ee21f58b8c880cf8a#enable-belt-printing) is enabled. The remap rows are only shown in **Developer** mode.

The transforms are applied in this order:

1. The [G-code axis remap](machine-frame-transforms.md#g-code-axis-remap) determines which slicer axis maps to each machine axis.
2. The [machine-frame tilt](machine-frame-transforms.md#machine-frame-tilt) compensates for the gantry not being perpendicular to the belt.

These settings are configured in the printer profile to match the machine's kinematics. The [Belt Printing](/broken/pages/226f2361e5d5e6ef3f7abf3becc7918d447a2ef7) guide explains their role in the slicing process.

Caution

Incorrect values can send the toolhead to an unintended position, potentially beyond the machine's travel limits. Check the result with **Show raw G-code (belt only)** in the preview's view menu (see [Preview](/broken/pages/226f2361e5d5e6ef3f7abf3becc7918d447a2ef7#preview)), and monitor the first print at the printer.

* [How axis remapping works](machine-frame-transforms.md#how-axis-remapping-works)
  * [Remap values](machine-frame-transforms.md#remap-values)
  * [Example: the belt profiles](machine-frame-transforms.md#example-the-belt-profiles)
  * [Where the remap is applied](machine-frame-transforms.md#where-the-remap-is-applied)
  * [What to watch for](machine-frame-transforms.md#what-to-watch-for)
* [G-code axis remap](machine-frame-transforms.md#g-code-axis-remap)
* [Machine-frame tilt](machine-frame-transforms.md#machine-frame-tilt)
  * [Decouple machine-frame tilt](machine-frame-transforms.md#decouple-machine-frame-tilt)
  * [Machine-frame tilt angle](machine-frame-transforms.md#machine-frame-tilt-angle)

## How axis remapping works[¶](machine-frame-transforms.md#how-axis-remapping-works) <a href="#how-axis-remapping-works" id="how-axis-remapping-works"></a>

An axis remap has three fields, **X**, **Y** and **Z**, one for each output axis. Each field selects an input axis and defines how its coordinate is mapped to the output. Together, the three fields swap, flip and mirror axes without changing distances.

### Remap values[¶](machine-frame-transforms.md#remap-values) <a href="#remap-values" id="remap-values"></a>

| Value                           | Result for a coordinate `v` on the selected input axis                                           |
| ------------------------------- | ------------------------------------------------------------------------------------------------ |
| **+X**, **+Y**, **+Z**          | `v`: the coordinate is copied.                                                                   |
| **-X**, **-Y**, **-Z**          | `-v`: the coordinate is negated, so the axis is flipped about the origin.                        |
| **Rev X**, **Rev Y**, **Rev Z** | `max - v`: the axis is mirrored inside the build volume, so 0 becomes `max` and `max` becomes 0. |

For the Rev values, `max` is the maximum coordinate of the selected input axis: the largest X or Y coordinate in the [printable area](/broken/pages/0d906d45479df31a3f89c370bdbfa417919f98de#printable-area-bed-shape), or the [printable height](/broken/pages/0d906d45479df31a3f89c370bdbfa417919f98de#printable-height) for Z.

Leaving the three fields at **+X**, **+Y**, **+Z** preserves the original coordinates.

### Example: the belt profiles[¶](machine-frame-transforms.md#example-the-belt-profiles) <a href="#example-the-belt-profiles" id="example-the-belt-profiles"></a>

The belt profiles included with OrcaSlicer use this [G-code axis remap](machine-frame-transforms.md#g-code-axis-remap):

| Field | Value | Meaning                                                         |
| ----- | ----- | --------------------------------------------------------------- |
| **X** | Rev X | Machine X runs across the belt, mirrored: `X = width - x`.      |
| **Y** | +Z    | Machine Y, the gantry axis, receives the height above the belt. |
| **Z** | +Y    | Machine Z, the belt axis, receives the position along the belt. |

A point placed in Prepare at `x = 20`, `y = 100`, `z = 5` on a belt 350 mm wide is therefore remapped to `X = 330`, `Y = 5`, `Z = 100`. The [machine-frame tilt](machine-frame-transforms.md#machine-frame-tilt) is then applied to those coordinates.

### Where the remap is applied[¶](machine-frame-transforms.md#where-the-remap-is-applied) <a href="#where-the-remap-is-applied" id="where-the-remap-is-applied"></a>

The remap acts on the toolpaths after slicing, so it only changes the axis letters and coordinate values used to write each move. The model itself is only rotated by the [belt tilt](/broken/pages/00dcd987ac21f7e44ecf650ee21f58b8c880cf8a#belt-tilt) before slicing, and that rotation is undone before the remap, so the remap receives points in the coordinate system of the model as placed in Prepare.

```
flowchart LR
    A[Model] --> B[Belt tilt rotation]
    B --> C[Slice]
    C --> D[Back-transform]
    D --> E[G-code axis remap]
    E --> F[Machine-frame tilt]
    F --> G[G-code]
```

### What to watch for[¶](machine-frame-transforms.md#what-to-watch-for) <a href="#what-to-watch-for" id="what-to-watch-for"></a>

* **Use every input axis exactly once.** OrcaSlicer does not check this. Assigning the same input axis to two outputs, for example **+X** in both the X and Y fields, discards one axis and flattens the print.
* **Custom G-code is not remapped.** Start, end, layer change and other [machine G-code](/broken/pages/8a0cca48a8cb689eb2e37db1bc877c26189bf981) is written to the file unchanged, so it must already be in machine coordinates.
* **Every move is written with X, Y and Z** while a remap is active, because any slicer axis can map to any machine axis.
* **Arc moves are limited.** G2/G3 arcs are only written when X and Y are left at **+X** and **+Y**. [Arc fitting](/broken/pages/c70b83c3a32422c9168494b30baab0b5314ff4ad#arc-fitting) is disabled on belt printers.
* **The remap is stored in the printer profile.** The fields are hidden when belt printing is disabled, but any configured remap remains active.

## G-code axis remap[¶](machine-frame-transforms.md#g-code-axis-remap) <a href="#g-code-axis-remap" id="g-code-axis-remap"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Developer`.\
[Variables](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `gcode_remap_x`, `gcode_remap_y`, `gcode_remap_z`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `Choice`.\
[Options](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `pos_x, pos_y, pos_z, neg_x, neg_y, neg_z, rev_x, rev_y, rev_z`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--gcode-remap-x=pos_x` (same pattern for the other variables above).\
Selects which slicer axis maps to each machine axis in the exported G-code. The remap is applied during G-code generation, after slicing, and does not change the toolpaths.

The **G-code remap X**, **Y** and **Z** rows are the machine axes. The values are described in [How axis remapping works](machine-frame-transforms.md#how-axis-remapping-works).

These fields are only shown when the settings [mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022) is **Developer**.

Note

The subsequent [machine-frame tilt](machine-frame-transforms.md#machine-frame-tilt) expects the axis mapping used by the belt profiles: height above the belt on the gantry axis and position along the belt on machine Z.

## Machine-frame tilt[¶](machine-frame-transforms.md#machine-frame-tilt) <a href="#machine-frame-tilt" id="machine-frame-tilt"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Expert`.\
[Variables](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `belt_frame_tilt_decouple`, `belt_frame_tilt_angle`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb): `belt_frame_tilt_decouple` (Boolean), `belt_frame_tilt_angle` (Float).\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--belt-frame-tilt-decouple=1` (`belt_frame_tilt_decouple` shown; other variables above follow their own type).\
On a belt printer, the gantry is not perpendicular to the belt. One millimeter of gantry travel therefore raises the nozzle by less than one millimeter and also moves it along the belt. The machine-frame tilt compensates for both effects so that the printed part matches the model.

![belt\_machine\_frame](.gitbook/assets/belt_machine_frame.svg)

For a point at height `h` above the belt and position `y` along it, with a gantry tilted at angle `α`:

* The gantry must travel `h / sin α` to reach that height.
* The layer through the point meets the belt at a distance of `h · cot α` farther along, so the belt position is `y + h · cot α`.

With the [belt profile remap](machine-frame-transforms.md#example-the-belt-profiles) and a [belt tilt](/broken/pages/00dcd987ac21f7e44ecf650ee21f58b8c880cf8a#belt-tilt) about X, the remapped coordinates are converted to machine coordinates as follows:

\[XmachineYmachineZmachine]=\[XYsin⁡αZ+Ycot⁡α] \begin{bmatrix} X\_{machine} \\\ Y\_{machine} \\\ Z\_{machine} \end{bmatrix} = \begin{bmatrix} X \\\ \dfrac{Y}{\sin\alpha} \\\ Z + Y\cot\alpha \end{bmatrix}

For a belt tilt about Y, the same correction is applied to X instead of Y: X is divided by `sin α` and Z becomes `Z - X · cot α`.

For a tilt about X at 45°, this simplifies to `Y · 1.414` for the gantry and `Z + Y` for the belt. At 90°, the gantry is perpendicular to the belt and the coordinates remain unchanged.

By default, the angle is the [belt tilt angle](/broken/pages/00dcd987ac21f7e44ecf650ee21f58b8c880cf8a#tilt-angle), so one value controls both the slicing rotation and this correction. No correction is applied when the [tilt axis](/broken/pages/00dcd987ac21f7e44ecf650ee21f58b8c880cf8a#tilt-axis) is **Z** or **None**.

### Decouple machine-frame tilt[¶](machine-frame-transforms.md#decouple-machine-frame-tilt) <a href="#decouple-machine-frame-tilt" id="decouple-machine-frame-tilt"></a>

Allows the machine-frame correction to use a separate angle from the belt tilt angle.

Enable this option only when the gantry's physical tilt differs from the slicing angle, for example to slice at 30° on a 45° machine.

Warning

Slicing at an angle different from the gantry's tilt changes how close the nozzle and hotend come to previously printed layers. Check the clearance before printing.

### Machine-frame tilt angle[¶](machine-frame-transforms.md#machine-frame-tilt-angle) <a href="#machine-frame-tilt-angle" id="machine-frame-tilt-angle"></a>

The angle, in degrees, used for the machine-frame correction while [Decouple machine-frame tilt](machine-frame-transforms.md#decouple-machine-frame-tilt) is enabled. It is ignored otherwise.
