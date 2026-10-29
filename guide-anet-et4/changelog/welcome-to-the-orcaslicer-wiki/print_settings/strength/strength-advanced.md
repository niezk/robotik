# Strength Advanced¶

* [Align directions to model](strength-advanced.md#align-directions-to-model)
* [Bridge infill direction](strength-advanced.md#bridge-infill-direction)
* [Relative Bridge Angle](strength-advanced.md#relative-bridge-angle)
* [Minimum sparse infill threshold](strength-advanced.md#minimum-sparse-infill-threshold)
* [Infill Combination](strength-advanced.md#infill-combination)
  * [Max layer height](strength-advanced.md#max-layer-height)
* [Detect narrow internal solid infill](strength-advanced.md#detect-narrow-internal-solid-infill)
* [Ensure vertical shell thickness](strength-advanced.md#ensure-vertical-shell-thickness)

## Align directions to model[¶](strength-advanced.md#align-directions-to-model) <a href="#align-directions-to-model" id="align-directions-to-model"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `align_infill_direction_to_model`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--align-infill-direction-to-model=1`.\
Aligns [infill](/broken/pages/da1f51648c030aebc578bfec4de7c7b47ec7ddd2#direction), [bridge](strength-advanced.md#bridge-infill-direction), [ironing](/broken/pages/773973b34ceefeb20e0955b2307ec254cf82ab14#angle-offset) and [top/bottom surface fill](/broken/pages/a93444d6bc5d3f832eed7be5e316e5e8f71eee5d#surface-pattern) directions to follow the model's orientation on the build plate.\
When enabled, these directions rotate together with the model so the printed features keep their intended orientation relative to the part, preserving optimal strength and surface characteristics regardless of how the model is placed.

![fill-direction-to-model](<../../../.gitbook/assets/fill direction to model.png>)

## Bridge infill direction[¶](strength-advanced.md#bridge-infill-direction) <a href="#bridge-infill-direction" id="bridge-infill-direction"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variables](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `bridge_angle`, `internal_bridge_angle`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--bridge-angle=1` (same pattern for the other variables above).\
If left to zero, the bridging angle will be calculated automatically for each specific bridge.\
Otherwise the provided angle will be used according to:

* The absolute coordinates
* The absolute coordinates + Model rotation: If [Align directions to model](strength-advanced.md#align-directions-to-model) is enabled
* The optimal automatic angle + this value: If [Relative Bridge Angle](strength-advanced.md#relative-bridge-angle) is enabled

Note

Use 180° for zero absolute angle.

## Relative Bridge Angle[¶](strength-advanced.md#relative-bridge-angle) <a href="#relative-bridge-angle" id="relative-bridge-angle"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `relative_bridge_angle`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--relative-bridge-angle=1`.\
When enabled, the bridge angle values are added to the automatically calculated bridge direction instead of overriding it.\
A small angle (<10°) is recommended to improve bridge coverage in closed shapes.

![bridge-angle-0](<../../../.gitbook/assets/bridge angle 0.png>) ![bridge-angle-2](<../../../.gitbook/assets/bridge angle 2.png>) ![bridge-angle-8](<../../../.gitbook/assets/bridge angle 8.png>)

## Minimum sparse infill threshold[¶](strength-advanced.md#minimum-sparse-infill-threshold) <a href="#minimum-sparse-infill-threshold" id="minimum-sparse-infill-threshold"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `minimum_sparse_infill_area`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--minimum-sparse-infill-area=1`.\
Sparse infill areas smaller than the threshold value (in mm²) are replaced by [internal solid infill](/broken/pages/da1f51648c030aebc578bfec4de7c7b47ec7ddd2#internal-solid-infill). This setting helps to ensure that small areas of sparse infill do not compromise the strength of the print. It is particularly useful for models with intricate designs or small features where sparse infill may not provide sufficient support.

## Infill Combination[¶](strength-advanced.md#infill-combination) <a href="#infill-combination" id="infill-combination"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `infill_combination`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--infill-combination=1`.\
Automatically combine [sparse infill](/broken/pages/da1f51648c030aebc578bfec4de7c7b47ec7ddd2) of several layers so they print together, reducing print time. Walls are still printed with the original [layer height](/broken/pages/2c08bb28e128ee0601904ad0a628782951bc11ea).

![fill-combination](<../../../.gitbook/assets/fill combination.png>)

### Max layer height[¶](strength-advanced.md#max-layer-height) <a href="#max-layer-height" id="max-layer-height"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `infill_combination_max_layer_height`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float or Percentage`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--infill-combination-max-layer-height=20%`.\
Maximum layer height for the combined sparse infill.\
Set it to 0 or 100% to use the nozzle diameter (for maximum reduction in print time), or to a value of \~80% to maximize sparse infill strength.

The number of layers over which infill is combined is derived by dividing this value by the layer height and rounding down to a whole number.

Use either absolute mm values (e.g., 0.32mm for a 0.4mm nozzle) or percentages (e.g., 80%). This value must not be larger than the nozzle diameter.

## Detect narrow internal solid infill[¶](strength-advanced.md#detect-narrow-internal-solid-infill) <a href="#detect-narrow-internal-solid-infill" id="detect-narrow-internal-solid-infill"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `detect_narrow_internal_solid_infill`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--detect-narrow-internal-solid-infill=1`.\
This option auto-detects narrow internal solid infill areas. If enabled, the [concentric pattern](/broken/pages/a147f0b85dea1cbf1cf61adb81420a35f687c13f#concentric) will be used in those areas to speed up printing. Otherwise, they use the selected [internal solid infill](/broken/pages/da1f51648c030aebc578bfec4de7c7b47ec7ddd2#internal-solid-infill) pattern (for example, the [rectilinear pattern](/broken/pages/a147f0b85dea1cbf1cf61adb81420a35f687c13f#rectilinear)).

## Ensure vertical shell thickness[¶](strength-advanced.md#ensure-vertical-shell-thickness) <a href="#ensure-vertical-shell-thickness" id="ensure-vertical-shell-thickness"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `ensure_vertical_shell_thickness`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `Choice`.\
[Options](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `none, ensure_critical_only, ensure_moderate, ensure_all`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--ensure-vertical-shell-thickness=none`.\
Add solid infill near sloping surfaces to guarantee the vertical shell thickness (top and bottom solid layers).

* **None**: No solid infill will be added anywhere. **Caution:** Use this option carefully if your model has sloped surfaces.
* **Critical Only**: Avoid adding solid infill for walls.
* **Moderate**: Add solid infill for heavily sloping surfaces only.
* **All (default)**: Add solid infill for all suitable sloping surfaces.
