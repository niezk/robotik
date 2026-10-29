# Material Flow Ratio and Pressure Advance¶

Flow ratio and pressure advance settings for the selected material.

* [Flow Ratio](material-flow-ratio-and-pressure-advance.md#flow-ratio)
* [Pressure Advance](material-flow-ratio-and-pressure-advance.md#pressure-advance)
  * [Enable adaptive Pressure Advance (beta)](material-flow-ratio-and-pressure-advance.md#enable-adaptive-pressure-advance-beta)
    * [Enable adaptive pressure advance for overhangs (beta)](material-flow-ratio-and-pressure-advance.md#enable-adaptive-pressure-advance-for-overhangs-beta)
    * [Pressure advance for bridges](material-flow-ratio-and-pressure-advance.md#pressure-advance-for-bridges)
    * [Adaptive pressure advance measurements (beta)](material-flow-ratio-and-pressure-advance.md#adaptive-pressure-advance-measurements-beta)
      * [How to calibrate Adaptive Pressure Advance](material-flow-ratio-and-pressure-advance.md#how-to-calibrate-adaptive-pressure-advance)

## Flow Ratio[¶](material-flow-ratio-and-pressure-advance.md#flow-ratio) <a href="#flow-ratio" id="flow-ratio"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `filament_flow_ratio`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--filament-flow-ratio=1`.\
The material may have volumetric change after switching between molten and crystalline states. This setting changes all extrusion flow of this filament in G-code proportionally.\
The recommended value range is between 0.95 and 1.05. You may be able to tune this value to get a nice flat surface if there is slight overflow or underflow.\
The final object flow ratio is this value multiplied by the [filament flow ratio](/broken/pages/4da0e8a2d1390e2f4166da4f6cca2f83837a3bb6#flow-ratio).

Tip

Check the [Flow Ratio Calibration guide](/broken/pages/de2365cb9daaa98d9ad3608097376a29f2371e9c).

## Pressure Advance[¶](material-flow-ratio-and-pressure-advance.md#pressure-advance) <a href="#pressure-advance" id="pressure-advance"></a>

[Modes](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022):\
`Simple` [Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `enable_pressure_advance`.\
`Advanced` [Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `pressure_advance`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb): `enable_pressure_advance` (Boolean list), `pressure_advance` (Float list).\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--enable-pressure-advance=1` (`enable_pressure_advance` shown; other variables above follow their own type).\
Pressure advance [Klipper](https://www.klipper3d.org/Pressure_Advance.html) and [RepRap](https://docs.duet3d.com/User_manual/Tuning/Pressure_advance) AKA [Linear advance (Marlin)](https://marlinfw.org/docs/features/lin_advance.html) is a feature that compensates for the lag in filament pressure within the nozzle during acceleration and deceleration. It helps improve print quality by reducing issues like blobs, oozing, and inconsistent extrusion, especially at corners or during fast movements.

Note

Auto calibration result will be overwritten once enabled

Tip

Check the [Pressure Advance Calibration guide](/broken/pages/98e0a11e8871bb509a2675168d1a37d297df9e2e).

### Enable adaptive Pressure Advance (beta)[¶](material-flow-ratio-and-pressure-advance.md#enable-adaptive-pressure-advance-beta) <a href="#enable-adaptive-pressure-advance-beta" id="enable-adaptive-pressure-advance-beta"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `adaptive_pressure_advance`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Boolean list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--adaptive-pressure-advance=1`.\
With increasing print speeds (and hence increasing volumetric flow through the nozzle) and increasing accelerations, it has been observed that the effective PA value typically decreases. This means that a single PA value is not always 100% optimal for all features and a compromise value is usually used that does not cause too much bulging on features with lower flow speed and accelerations while also not causing gaps on faster features.

This feature aims to address this limitation by modeling the response of your printer's extrusion system depending on the volumetric flow speed and acceleration it is printing at. Internally, it generates a fitted model that can extrapolate the needed pressure advance for any given volumetric flow speed and acceleration, which is then emitted to the printer depending on the current print conditions.

When enabled, the pressure advance value above is overridden. However, a reasonable default value above is strongly recommended to act as a fallback and for when tool changing.

Tip

Check the [Adaptive Pressure Advance Calibration guide](/broken/pages/4f66a6f5693b4bfc0e71b9323776541409376697).

#### Enable adaptive pressure advance for overhangs (beta)[¶](material-flow-ratio-and-pressure-advance.md#enable-adaptive-pressure-advance-for-overhangs-beta) <a href="#enable-adaptive-pressure-advance-for-overhangs-beta" id="enable-adaptive-pressure-advance-for-overhangs-beta"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `adaptive_pressure_advance_overhangs`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Boolean list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--adaptive-pressure-advance-overhangs=1`.\
Enable adaptive PA for overhangs as well as when flow changes within the same feature. This is an experimental option, as if the PA profile is not set accurately, it will cause uniformity issues on the external surfaces before and after overhangs.

#### Pressure advance for bridges[¶](material-flow-ratio-and-pressure-advance.md#pressure-advance-for-bridges) <a href="#pressure-advance-for-bridges" id="pressure-advance-for-bridges"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `adaptive_pressure_advance_bridges`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--adaptive-pressure-advance-bridges=1`.\
Pressure advance value for bridges. Set to 0 to disable.\
A lower PA value when printing bridges helps reduce the appearance of slight under extrusion immediately after bridges.\
This is caused by the pressure drop in the nozzle when printing in the air and a lower PA helps counteract this.

#### Adaptive pressure advance measurements (beta)[¶](material-flow-ratio-and-pressure-advance.md#adaptive-pressure-advance-measurements-beta) <a href="#adaptive-pressure-advance-measurements-beta" id="adaptive-pressure-advance-measurements-beta"></a>

Add sets of **pressure advance** (PA) values, the **volumetric flow speeds** and **accelerations** they were measured at, separated by a comma.\
One set of values per line. For example:

```
[PA 1],[FLOW 1],[ACCELERATION 1]
[PA 2],[FLOW 2],[ACCELERATION 2]
...
[PA n],[FLOW n],[ACCELERATION n]
```

```
0.04,3.96,3000
0.033,3.96,10000
0.029,7.91,3000
0.026,7.91,10000
```

**How to calibrate Adaptive Pressure Advance**[**¶**](material-flow-ratio-and-pressure-advance.md#how-to-calibrate-adaptive-pressure-advance)

It's highly recommended to use the [Adaptive Pressure Advance Calibration guide](/broken/pages/4f66a6f5693b4bfc0e71b9323776541409376697).

1. Run the pressure advance test for at least 3 speeds per acceleration value. It is recommended that the test is run for at least the speed of the external perimeters, the speed of the internal perimeters and the fastest feature print speed in your profile (usually it's the sparse or solid infill). Then run them for the same speeds for the slowest and fastest print accelerations, and no faster than the recommended maximum acceleration as given by the Klipper input shaper.
2. Take note of the optimal PA value for each volumetric flow speed and acceleration. You can find the flow number by selecting "flow" from the color scheme drop down and move the horizontal slider over the PA pattern lines. The number should be visible at the bottom of the page. The ideal PA value should be decreasing the higher the volumetric flow is. If it is not, confirm that your extruder is functioning correctly. The slower and with less acceleration you print, the larger the range of acceptable PA values. If no difference is visible, use the PA value from the faster test.
3. Enter the triplets of PA values, Flow and Accelerations in the text box here and save your filament profile.
