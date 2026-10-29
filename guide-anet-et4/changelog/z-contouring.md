# Z Contouring¶

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Expert`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `zaa_enabled`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--zaa-enabled=1`.\
Z contouring, also called Z-layer anti-aliasing or ZAA, reduces visible stair-stepping on curved and sloped top surfaces by adjusting the Z height of individual extrusion points so the toolpath follows the original model surface more closely.

![z-contouring](<.gitbook/assets/z contouring.jpg>)

Instead of keeping every move at a single flat Z for the whole layer, OrcaSlicer processes eligible top-surface toolpaths and emits varying Z values inside the affected layer.\
This can noticeably smooth domes, chamfers, shallow slopes, and similar top-facing geometry without changing the nominal layer height of the rest of the print.

![z-contouring](<.gitbook/assets/z contouring.gif>)

Note

Current implementation targets top-facing curved or sloped surfaces.\
**Downward-facing or upside-down curves are not handled.**

* [Minimize wall height angle](z-contouring.md#minimize-wall-height-angle)
* [Minimum z height](z-contouring.md#minimum-z-height)
* [Don't alternate fill direction](z-contouring.md#dont-alternate-fill-direction)

## Minimize wall height angle[¶](z-contouring.md#minimize-wall-height-angle) <a href="#minimize-wall-height-angle" id="minimize-wall-height-angle"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Expert`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `zaa_minimize_perimeter_height`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--zaa-minimize-perimeter-height=1`.\
Reduce the height of top-surface perimeters so they better match the model edge on slopes steeper than this angle.\
This setting affects both internal and external perimeters.\
Set `0` to disable it.

The default of 35 degrees is a reasonable starting point.

## Minimum z height[¶](z-contouring.md#minimum-z-height) <a href="#minimum-z-height" id="minimum-z-height"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Expert`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `zaa_min_z`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--zaa-min-z=1`.\
Minimum local layer height allowed for contoured toolpaths. This setting also controls the slicing plane used for contoured layers.

* Lower values allow stronger contouring but leave less minimum layer thickness.
* Higher values move the slicing plane up (it sits this far above the bottom of the layer), and paths are never lowered below it, so walls and top surface infill can drop less. Top surface infill can also rise up to this amount above the nominal layer height, while walls are never raised.

## Don't alternate fill direction[¶](z-contouring.md#dont-alternate-fill-direction) <a href="#dont-alternate-fill-direction" id="dont-alternate-fill-direction"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Expert`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `zaa_dont_alternate_fill_direction`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--zaa-dont-alternate-fill-direction=1`.\
Keep the fill direction consistent from layer to layer instead of alternating it.\
This can help produce a more consistent surface pattern on curved top surfaces. It only has an effect when Z contouring is enabled for that region.
