# CLI Transform¶

Transform options change the loaded model's geometry or placement before slicing. See [CLI Mode](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24) for general flag syntax.

Important

Transform flags are applied in the order they appear on the command line, not in the order listed on this page. `--rotate 90 --scale 2` rotates then scales; `--scale 2 --rotate 90` scales then rotates. For most of these options the end result is identical either way, but it's worth being deliberate about ordering when combining several.

* [Arrangement](cli-transform.md#arrangement)
* [Geometry](cli-transform.md#geometry)
* [Object Handling](cli-transform.md#object-handling)

## Arrangement[¶](cli-transform.md#arrangement) <a href="#arrangement" id="arrangement"></a>

| Flag              | Input          | Description                                                                                                                                                                                      | Notes                |
| ----------------- | -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------- |
| `--arrange`       | `option` (int) | Arrange objects on the plate: `0` = disable, `1` = force enable, any other value = auto. See [Auto Arrange](/broken/pages/0fcd3913806f2ebe7be268c6b82f8de56ec468b6) for the underlying behavior. |                      |
| `--ensure-on-bed` | boolean        | Lift any object that is partially below the bed so it sits on top of it.                                                                                                                         | Disabled by default. |
| `--orient`        | `option` (int) | Auto-orient objects: `0` = disable, `1` = force enable, any other value = auto. See [Auto Orient](/broken/pages/48768aee70a91c4cb4a5ed9e042d45cdb835a2bd).                                       |                      |

## Geometry[¶](cli-transform.md#geometry) <a href="#geometry" id="geometry"></a>

| Flag             | Input            | Description                                                                                                                                                                                                                            | Notes                                                                                                         |
| ---------------- | ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| `--convert-unit` | boolean          | Detect models saved in meters or inches and convert them to millimeters.                                                                                                                                                               |                                                                                                               |
| `--repair`       | boolean          | Repair every part of the loaded models as [Fix Model](/broken/pages/022d6c93903041ffa5c75b47b4f686eb1f452832#fix-model) does: close holes and cracks, orient the meshes outward and remove local self-intersections. Painting is kept. | Disabled by default. A part the repair cannot turn into a solid is left as it was, with a warning in the log. |
| `--rotate`       | degrees (float)  | Rotate every loaded object around the Z axis. See [Rotate](/broken/pages/a691eabc04ab3934828d2bb55bd1e27f4b91c14d#rotate).                                                                                                             |                                                                                                               |
| `--rotate-x`     | degrees (float)  | Rotate every loaded object around the X axis.                                                                                                                                                                                          |                                                                                                               |
| `--rotate-y`     | degrees (float)  | Rotate every loaded object around the Y axis.                                                                                                                                                                                          |                                                                                                               |
| `--scale`        | `factor` (float) | Scale every loaded object by this factor. See [Scale](/broken/pages/a691eabc04ab3934828d2bb55bd1e27f4b91c14d#scale).                                                                                                                   | Must be greater than `0`.                                                                                     |

## Object Handling[¶](cli-transform.md#object-handling) <a href="#object-handling" id="object-handling"></a>

| Flag            | Input         | Description                                                                                              | Notes                                                                                                                                                              |
| --------------- | ------------- | -------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `--repetitions` | `count` (int) | Duplicate the whole model this many times on the plate.                                                  | Requires [`--slice`](/broken/pages/61ee1adbe009d97d3739836a2fa144a9f1598c07#slicing) to target a single plate (not `0`/all-plates). Cannot exceed the plate count. |
| `--assemble`    | boolean       | Merge all loaded models into a single object on one plate, so subsequent actions apply to it as a whole. | Cannot be combined with [`--clone-objects`](/broken/pages/207a72e3c325b6315929c4ce8e7ce061a1611fca#object-selection).                                              |
