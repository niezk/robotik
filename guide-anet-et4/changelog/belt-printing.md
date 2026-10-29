# Belt Printing¶

Important

NEW FEATURE: **Belt printer support**\
Available in: [Nightly builds](https://github.com/OrcaSlicer/OrcaSlicer/releases/tag/nightly-builds) or Releases greater than **2.4.2**.

A belt printer (also called a conveyor or "infinite Z" printer) replaces the fixed bed with a moving belt and tilts the gantry over it, usually by 45°. Because the belt carries printed material away from the nozzle, a part can be longer than the machine, and a series of parts can be printed without clearing the bed between them.

OrcaSlicer supports these machines with a dedicated belt printer mode, used by printers such as the Printcepts BabyBelt Pro, the IdeaFormer IR3 V2 and CR-30 style machines. This guide explains how that mode works and what changes in your workflow. The individual options are described in [Belt printer](/broken/pages/00dcd987ac21f7e44ecf650ee21f58b8c880cf8a) and [Machine frame transforms](/broken/pages/df5fc5714e332bba3841f83b76b802a9cacdf887).

* [How a belt printer differs](belt-printing.md#how-a-belt-printer-differs)
* [Setting up a belt printer](belt-printing.md#setting-up-a-belt-printer)
  * [Starter profiles](belt-printing.md#starter-profiles)
  * [A printer that is not listed](belt-printing.md#a-printer-that-is-not-listed)
* [How OrcaSlicer slices for a belt](belt-printing.md#how-orcaslicer-slices-for-a-belt)
  * [1. Pre-slice rotation](belt-printing.md#1-pre-slice-rotation)
  * [2. Slice](belt-printing.md#2-slice)
  * [3. Supports and brim](belt-printing.md#3-supports-and-brim)
  * [4. Back-transform](belt-printing.md#4-back-transform)
  * [5. Machine frame](belt-printing.md#5-machine-frame)
* [Working with a belt printer](belt-printing.md#working-with-a-belt-printer)
  * [Placing and arranging parts](belt-printing.md#placing-and-arranging-parts)
  * [First layer](belt-printing.md#first-layer)
  * [Brim](belt-printing.md#brim)
  * [Supports](belt-printing.md#supports)
  * [Multi-color printing](belt-printing.md#multi-color-printing)
  * [Preview](belt-printing.md#preview)
  * [Calibration](belt-printing.md#calibration)
* [Features that are not available](belt-printing.md#features-that-are-not-available)

## How a belt printer differs[¶](belt-printing.md#how-a-belt-printer-differs) <a href="#how-a-belt-printer-differs" id="how-a-belt-printer-differs"></a>

A slicer normally assumes that the bed lies in the XY plane and that layers stack along Z. A belt printer differs in both respects:

* **The layers are tilted.** The nozzle moves in the plane of the tilted gantry, so every layer is a slanted plane that starts on the belt and rises in the direction of belt travel.
* **The belt is an axis.** The motor that advances the belt is the printer's Z axis and the gantry height is its Y axis, so the "bed" lies in the machine's XZ plane and is, in principle, endless.

![belt\_flat\_bed\_vs\_belt](https://www.orcaslicer.com/wiki/images/belt/belt_flat_bed_vs_belt.svg?raw=true)

## Setting up a belt printer[¶](belt-printing.md#setting-up-a-belt-printer) <a href="#setting-up-a-belt-printer" id="setting-up-a-belt-printer"></a>

To enable belt mode, select [Enable belt printing](/broken/pages/00dcd987ac21f7e44ecf650ee21f58b8c880cf8a#enable-belt-printing) in **Printer settings → Basic information → Belt printer**. The group is only shown when the settings mode is **Advanced** or higher. With the option disabled, OrcaSlicer uses its standard printing behavior.

![belt\_printer\_wizard](.gitbook/assets/belt_printer_wizard.png)

### Starter profiles[¶](belt-printing.md#starter-profiles) <a href="#starter-profiles" id="starter-profiles"></a>

| Printer              | Vendor     | Nozzles            | Processes                    | Filaments                           |
| -------------------- | ---------- | ------------------ | ---------------------------- | ----------------------------------- |
| Generic Belt Printer | Custom     | 0.2, 0.4, 0.6, 0.8 | 0.20mm Standard, 0.12mm Fine | Filament library                    |
| BabyBelt Pro         | Printcepts | 0.4                | 0.20mm Standard              | Generic PLA, Generic PETG, eSUN PLA |
| IdeaFormer IR3 V2    | IdeaFormer | 0.4                | 0.20mm Standard              | Generic PLA, Generic PETG, eSUN PLA |

### A printer that is not listed[¶](belt-printing.md#a-printer-that-is-not-listed) <a href="#a-printer-that-is-not-listed" id="a-printer-that-is-not-listed"></a>

1. Add the **Generic Belt Printer** from the **Custom** vendor.
2. In [Printable space](/broken/pages/0d906d45479df31a3f89c370bdbfa417919f98de), set the printable area to match your belt: **X** is the width across the belt and **Y** is the belt length to display as one plate.
3. Set the [Printable height](/broken/pages/0d906d45479df31a3f89c370bdbfa417919f98de#printable-height) to the clearance under the gantry. On a belt printer, this limits the part's height above the belt, not its length along the belt.
4. Check the [Belt tilt](/broken/pages/00dcd987ac21f7e44ecf650ee21f58b8c880cf8a#belt-tilt) angle against your machine and save the profile.
5. Enter your machine's [start and end G-code](/broken/pages/8a0cca48a8cb689eb2e37db1bc877c26189bf981) and [motion limits](/broken/pages/053648f94ba5f635d165734b67c47d50256deed6), then tune the profile for your machine.

Tip

The belt options are available as [placeholders](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918) in custom G-code. The BabyBelt Pro profile, for example, passes the tilt to its start macro with `PRINT_START ANGLE=[belt_slice_rotation_angle] ...`.

Warning

Start, end and other custom G-code is written to the file unchanged. It is not rotated or remapped, so write it in machine coordinates: Y is the gantry and Z is the belt.

## How OrcaSlicer slices for a belt[¶](belt-printing.md#how-orcaslicer-slices-for-a-belt) <a href="#how-orcaslicer-slices-for-a-belt" id="how-orcaslicer-slices-for-a-belt"></a>

OrcaSlicer uses its existing slicing engine by transforming the model before slicing and the resulting toolpaths afterward.

```
flowchart LR
    A[Model on the belt] --> B[1. Pre-slice rotation]
    B --> C[2. Slice]
    C --> D[3. Supports and brim]
    D --> E[4. Back-transform]
    E --> F[5. Machine frame]
    F --> G[G-code]
```

### 1. Pre-slice rotation[¶](belt-printing.md#1-pre-slice-rotation) <a href="#id-1-pre-slice-rotation" id="id-1-pre-slice-rotation"></a>

The model is rotated by the [belt tilt](/broken/pages/00dcd987ac21f7e44ecf650ee21f58b8c880cf8a#belt-tilt) before it is sliced. Slicing the rotated model into horizontal layers produces layers that are tilted relative to the original model. This rotation preserves the model's shape and dimensions.

### 2. Slice[¶](belt-printing.md#2-slice) <a href="#id-2-slice" id="id-2-slice"></a>

The rotated model is sliced using the standard process, so walls, infill, seams, ironing, painting and most other features work on a belt without belt-specific settings.

### 3. Supports and brim[¶](belt-printing.md#3-supports-and-brim) <a href="#id-3-supports-and-brim" id="id-3-supports-and-brim"></a>

In the rotated coordinate system, the belt is a tilted plane rather than the plane at Z = 0. Supports and the brim are generated relative to that plane:

* Normal, tree and organic supports end on the belt surface, and nothing is generated below it. Under an overhang at the leading end of a part they reach the belt ahead of the part's first contact with it, so the support can start before the part itself.
* The brim is printed on the belt, with each layer contributing one strip.

### 4. Back-transform[¶](belt-printing.md#4-back-transform) <a href="#id-4-back-transform" id="id-4-back-transform"></a>

When the toolpaths are written, every point is rotated back into the coordinate system of the model as placed in Prepare, so the next step receives the coordinates shown in Prepare.

### 5. Machine frame[¶](belt-printing.md#5-machine-frame) <a href="#id-5-machine-frame" id="id-5-machine-frame"></a>

The firmware does not account for the tilted gantry, so OrcaSlicer converts the coordinates into the required motor positions in two steps:

1. The [G-code axis remap](/broken/pages/df5fc5714e332bba3841f83b76b802a9cacdf887#g-code-axis-remap) swaps the axes. In the belt profiles, the height above the belt becomes machine Y, the position along the belt becomes machine Z, and X is reversed.
2. The [machine-frame tilt](/broken/pages/df5fc5714e332bba3841f83b76b802a9cacdf887#machine-frame-tilt) scales the gantry coordinate and shifts the belt coordinate so that a vertical wall in the model prints vertically.

## Working with a belt printer[¶](belt-printing.md#working-with-a-belt-printer) <a href="#working-with-a-belt-printer" id="working-with-a-belt-printer"></a>

### Placing and arranging parts[¶](belt-printing.md#placing-and-arranging-parts) <a href="#placing-and-arranging-parts" id="placing-and-arranging-parts"></a>

In Prepare, the plate represents the belt surface, shown flat. X runs across the belt, Y runs along it and Z is the height above the belt, so parts are placed and oriented as on any other printer. The part closest to Y = 0 is printed first.

![belt\_prepare\_plate](.gitbook/assets/belt_prepare_plate.png)

* With [Infinite Y axis](/broken/pages/00dcd987ac21f7e44ecf650ee21f58b8c880cf8a#infinite-y-axis) enabled, a part may extend beyond the displayed plate along Y.
* A part must fit the belt width, and its height must fit under the gantry ([Printable height](/broken/pages/0d906d45479df31a3f89c370bdbfa417919f98de#printable-height)).
* [Auto arrange](/broken/pages/0fcd3913806f2ebe7be268c6b82f8de56ec468b6) places parts starting at the end of the belt that prints first. It groups parts that use the same filament so each filament change occurs once, and it leaves room for the brim and the [belt purge tower](/broken/pages/74f57ccd9ce07fa1f5a18d2766d92d9e5cb458ca#belt-purge-tower).

Tip

Part orientation affects overhangs differently than on a flat bed. Each layer is printed against the previous one, progressing from the end of the part that prints first toward the end that prints last. An overhang that points back along the belt is printed onto existing material, while an overhang at the leading end of the part starts in mid-air and needs support.

### First layer[¶](belt-printing.md#first-layer) <a href="#first-layer" id="first-layer"></a>

On a flat bed, the first layer is the first slice. On a belt, every tilted layer touches the belt along a narrow strip, so the "first layer" is a band along the belt surface that extends through the entire print.

OrcaSlicer applies first-layer speed, acceleration, jerk and temperature to extrusions inside that band, which is one [first layer height](/broken/pages/2c08bb28e128ee0601904ad0a628782951bc11ea#first-layer-height) thick. Settings that count layers, including the number of layers printed [without cooling](/broken/pages/d7c372477cc904769ba325c42008522f74ffec75#no-cooling-for-the-first), count bands of that thickness above the belt surface instead.

### Brim[¶](belt-printing.md#brim) <a href="#brim" id="brim"></a>

Each layer meets the belt along a single line, so a [brim](/broken/pages/8f34753934cc3186e335ccb9927588ff743c306a) is more useful than on a flat bed. Three options are specific to belt printers:

![belt\_brim\_options](.gitbook/assets/belt_brim_options.png)

* [Leading length](/broken/pages/8f34753934cc3186e335ccb9927588ff743c306a#leading-length) extends the brim ahead of the part, anchoring the leading edge to material already attached to the belt.
* [Extra width](/broken/pages/8f34753934cc3186e335ccb9927588ff743c306a#extra-width) widens the brim across the belt.
* The [Leading edge only](/broken/pages/8f34753934cc3186e335ccb9927588ff743c306a#leading-edge-only) brim type limits the brim to the area where the part first contacts the belt.

### Supports[¶](belt-printing.md#supports) <a href="#supports" id="supports"></a>

All [support types](/broken/pages/a5ac9e1d60ddd3e6c582c4a55c887162b3caeab4) can be used and terminate at the belt surface. [Painted supports](/broken/pages/e142152c4a8336fa79900a69f2cd265fa6e43ef5) and [painted seams](/broken/pages/499549f00852518c397f84b689890171edbe0e30) follow the same rotation as the model.

### Multi-color printing[¶](belt-printing.md#multi-color-printing) <a href="#multi-color-printing" id="multi-color-printing"></a>

The standard [prime tower](/broken/pages/5aa3302c55047356a98465bb114707e629d121d9) cannot be printed on a belt. It is replaced by the [belt purge tower](/broken/pages/74f57ccd9ce07fa1f5a18d2766d92d9e5cb458ca#belt-purge-tower), a long, thin object that OrcaSlicer adds beside the parts along the far edge of the belt. Material is purged into this object at every filament change.

![belt\_purge\_tower\_prepare](.gitbook/assets/belt_purge_tower_prepare.png)

### Preview[¶](belt-printing.md#preview) <a href="#preview" id="preview"></a>

The preview shows the toolpaths in the model's coordinate system, so the part appears upright as designed. To see the coordinates written to the G-code instead, enable **Show raw G-code (belt only)** in the view menu of the preview canvas (the eye icon in the toolbar), or press `B`. The layers then lie along the belt axis the way the machine prints them. This only changes the preview; the exported G-code is the same either way.

![belt\_preview\_designed](.gitbook/assets/belt_preview_designed.png) ![belt\_preview\_view\_menu](.gitbook/assets/belt_preview_view_menu.png) ![belt\_preview\_raw](.gitbook/assets/belt_preview_raw.png)

### Calibration[¶](belt-printing.md#calibration) <a href="#calibration" id="calibration"></a>

* The [temperature tower](/broken/pages/997c84d925b5c4e01d5d5c3bb47c84d949b256d0) dialog offers a **Test model** selection on belt printers: **Standard** or **Overhang**.
* For [pressure advance](/broken/pages/98e0a11e8871bb509a2675168d1a37d297df9e2e), only the **PA Tower** method is enabled on belt printers.

![belt\_temp\_tower\_dialog](.gitbook/assets/belt_temp_tower_dialog.png)

## Features that are not available[¶](belt-printing.md#features-that-are-not-available) <a href="#features-that-are-not-available" id="features-that-are-not-available"></a>

Some features are incompatible with belt printing or would cause unsuitable belt movements. OrcaSlicer disables these features in the settings or prevents slicing when they are enabled.

| Feature                                                                                       | On a belt printer                                                                                                                              |
| --------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| [Skirt](/broken/pages/c1db5ba9eabdd3f5539eaecc05b5a6c1efdeac1b)                               | Disabled. No skirt is generated.                                                                                                               |
| [Raft](/broken/pages/95f71e091ed1cc246f563f406e1b5624bec1bd46)                                | Slicing is blocked when raft layers are configured.                                                                                            |
| Draft shield                                                                                  | Slicing is blocked when enabled.                                                                                                               |
| [Prime tower](/broken/pages/5aa3302c55047356a98465bb114707e629d121d9)                         | Never generated. Use the [belt purge tower](/broken/pages/74f57ccd9ce07fa1f5a18d2766d92d9e5cb458ca#belt-purge-tower).                          |
| [Arc fitting](/broken/pages/c70b83c3a32422c9168494b30baab0b5314ff4ad#arc-fitting)             | Disabled. The machine-frame transform turns a circle into an ellipse, which G2/G3 cannot represent.                                            |
| [Scarf joint seam](/broken/pages/d510c886533141d059d469a1d79d3c1c34992e9e#scarf-joint-seam)   | Disabled. The scarf would start inside the previous layer.                                                                                     |
| [Spiral vase](/broken/pages/e792de15ca89fe7bca7e8654ec76e5852fdd584b#spiral-vase) with a brim | Incompatible with belt brims, which extend across layers beyond Z = 0.                                                                         |
| [Z hop](/broken/pages/dc18322a6319f10648e1a1374e7cae7f8bb073ca)                               | Set to 0 in the belt profiles because lifting away from a tilted layer requires belt movement, which can cause problems on most belt printers. |
| Brim types Auto, Mouse ears and Painted                                                       | Printed as an outer brim. See [Brim](/broken/pages/8f34753934cc3186e335ccb9927588ff743c306a#type).                                             |
| PA Line and PA Pattern calibration                                                            | Unavailable. Use PA Tower.                                                                                                                     |

## Fun things to try[¶](belt-printing.md#fun-things-to-try) <a href="#fun-things-to-try" id="fun-things-to-try"></a>

You can print a cube with all its walls in vase mode.
