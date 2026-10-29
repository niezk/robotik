# Adaptive Bed Mesh¶

OrcaSlicer introduces comprehensive support for adaptive bed meshing across a variety of firmware, including Marlin, Klipper, and RepRapFirmware (RRF).\
This feature allows users to seamlessly integrate adaptive bed mesh commands within the Machine Start G-code.\
The implementation is designed to be straightforward, requiring no additional plugins or alterations to firmware settings, thereby enhancing user experience and print quality directly from OrcaSlicer.\
![ABM-PrinterConfig](<../../../.gitbook/assets/ABM PrinterConfig.png>)

* [Bed mesh](adaptive-bed-mesh.md#bed-mesh)
* [Probe point distance](adaptive-bed-mesh.md#probe-point-distance)
* [Mesh margin](adaptive-bed-mesh.md#mesh-margin)
* [Available g-code variables for Adaptive Bed Mesh Command](adaptive-bed-mesh.md#available-g-code-variables-for-adaptive-bed-mesh-command)
* [Example of Adaptive Bed Mesh usage in OrcaSlicer](adaptive-bed-mesh.md#example-of-adaptive-bed-mesh-usage-in-orcaslicer)
  * [Marlin](adaptive-bed-mesh.md#marlin)
  * [Klipper](adaptive-bed-mesh.md#klipper)
  * [RRF](adaptive-bed-mesh.md#rrf)

## Bed mesh[¶](adaptive-bed-mesh.md#bed-mesh) <a href="#bed-mesh" id="bed-mesh"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variables](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `bed_mesh_min`, `bed_mesh_max`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#point): `Point`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--bed-mesh-min=100,100` (same pattern for the other variables above).\
This option sets the min and max point for the allowed bed mesh area. Due to the probe's XY offset, most printers are unable to probe the entire bed. To ensure the probe point does not go outside the bed area, the minimum and maximum points of the bed mesh should be set appropriately.\
OrcaSlicer ensures that adaptive\_bed\_mesh\_min/adaptive\_bed\_mesh\_max values do not exceed these min/max points. This information can usually be obtained from your printer manufacturer.\
The default setting is (-99999, -99999), which means there are no limits, thus allowing probing across the entire bed.

## Probe point distance[¶](adaptive-bed-mesh.md#probe-point-distance) <a href="#probe-point-distance" id="probe-point-distance"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `bed_mesh_probe_distance`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#point): `Point`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--bed-mesh-probe-distance=100,100`.\
This option sets the preferred distance between probe points (grid size) for the X and Y directions, with the default being 50mm for both X and Y.

## Mesh margin[¶](adaptive-bed-mesh.md#mesh-margin) <a href="#mesh-margin" id="mesh-margin"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `adaptive_bed_mesh_margin`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--adaptive-bed-mesh-margin=1`.\
This option determines the additional distance by which the adaptive bed mesh area should be expanded in the XY directions.

Note

Klipper users: OrcaSlicer will adjust adaptive bed mesh area according to the margin. It is recommended to set the margin to 0 in Klipper config or pass 0 when calling BED\_MESH\_CALIBRATE command(please refer to the example below).

## Available g-code variables for Adaptive Bed Mesh Command[¶](adaptive-bed-mesh.md#available-g-code-variables-for-adaptive-bed-mesh-command) <a href="#available-g-code-variables-for-adaptive-bed-mesh-command" id="available-g-code-variables-for-adaptive-bed-mesh-command"></a>

`bed_mesh_probe_count`: Represents the probe count in the X and Y directions. This value is calculated based on the size of the adaptive bed mesh area and the distance between probe points.

`adaptive_bed_mesh_min`: Specifies the minimum coordinates of the adaptive bed mesh area, defining the starting point of the mesh.

`adaptive_bed_mesh_max`: Determines the maximum coordinates of the adaptive bed mesh area, indicating the endpoint of the mesh.

`ALGORITHM`: Identifies the algorithm used for adaptive bed mesh interpolation. This variable is useful for Klipper users. If bed\_mesh\_probe\_count is less than 4, the algorithm is set to `lagrange`. Otherwise, it is set to `bicubic`.

## Example of Adaptive Bed Mesh usage in OrcaSlicer[¶](adaptive-bed-mesh.md#example-of-adaptive-bed-mesh-usage-in-orcaslicer) <a href="#example-of-adaptive-bed-mesh-usage-in-orcaslicer" id="example-of-adaptive-bed-mesh-usage-in-orcaslicer"></a>

### Marlin[¶](adaptive-bed-mesh.md#marlin) <a href="#marlin" id="marlin"></a>

```
; Marlin don't support specify the probe count yet, so we only specify the probe area
G29 L{adaptive_bed_mesh_min[0]} R{adaptive_bed_mesh_max[0]} F{adaptive_bed_mesh_min[1]} B{adaptive_bed_mesh_max[1]} T V4
```

### Klipper[¶](adaptive-bed-mesh.md#klipper) <a href="#klipper" id="klipper"></a>

```
; Always pass `ADAPTIVE_MARGIN=0` because Orca has already handled `adaptive_bed_mesh_margin` internally
; Make sure to set ADAPTIVE to 0 otherwise Klipper will use it's own adaptive bed mesh logic
BED_MESH_CALIBRATE mesh_min={adaptive_bed_mesh_min[0]},{adaptive_bed_mesh_min[1]} mesh_max={adaptive_bed_mesh_max[0]},{adaptive_bed_mesh_max[1]} ALGORITHM=[bed_mesh_algo] PROBE_COUNT={bed_mesh_probe_count[0]},{bed_mesh_probe_count[1]} ADAPTIVE=0 ADAPTIVE_MARGIN=0
```

### RRF[¶](adaptive-bed-mesh.md#rrf) <a href="#rrf" id="rrf"></a>

```
M557 X{adaptive_bed_mesh_min[0]}:{adaptive_bed_mesh_max[0]} Y{adaptive_bed_mesh_min[1]}:{adaptive_bed_mesh_max[1]} P{bed_mesh_probe_count[0]}:{bed_mesh_probe_count[1]}
```

![ABM-Machine-G-code](<../../../.gitbook/assets/ABM Machine G code.png>)
