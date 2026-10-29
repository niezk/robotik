# Line Width¶

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `line_width`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float or Percentage`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--line-width=20%`.\
These settings define how wide each extruded line of filament will be.\
Line width can be configured in two ways:

* Fixed value in millimeters (mm)
* Percentage of the nozzle diameter

Tip

Using percentages allows the slicer to automatically adjust the line width when the nozzle size changes, helping maintain consistent print quality across different nozzle sizes.

A good starting point is setting the line width to **100% of the nozzle diameter**. Values below this may lead to poor adhesion, while values above **150%** can cause **over-extrusion**, resulting in blobs or poor surface quality.\
However, slightly wider lines generally improve **layer bonding** and **print strength**, especially for internal features like walls and infill.

Note

**Line width is the width of the line as laid on the layer.** Orca calculates the extruded volume from the line width and layer height, so a 100% line width gives a line as wide as the nozzle, and higher values squish the line wider than the nozzle opening.\
You can read more on the flow math here: [Flow Math](https://manual.slic3r.org/advanced/flow-math).

Important

This will match only if using the [**Classic** wall generator](/broken/pages/54a6fe288c2767d758a6868ebef10f327f69163c#classic).\
[**Arachne**](/broken/pages/54a6fe288c2767d758a6868ebef10f327f69163c#arachne) will adjust the line width dynamically based on the model's geometry, using these values as a reference.

## Line Types[¶](line-width.md#line-types) <a href="#line-types" id="line-types"></a>

In OrcaSlicer, you can assign different line widths to specific parts of the print. Each type can be customized:

### Default[¶](line-width.md#default) <a href="#default" id="default"></a>

Fallback value used when a specific line width is not set (set to `0`).

### First Layer[¶](line-width.md#first-layer) <a href="#first-layer" id="first-layer"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `initial_layer_line_width`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float or Percentage`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--initial-layer-line-width=20%`.\
A wider first layer (with a higher [first layer height](/broken/pages/2c08bb28e128ee0601904ad0a628782951bc11ea#first-layer-height)) improves bed adhesion and compensates for uneven build surfaces.\
First layer line width also overrides [Brim's](/broken/pages/8f34753934cc3186e335ccb9927588ff743c306a) and [Skirt's](/broken/pages/c1db5ba9eabdd3f5539eaecc05b5a6c1efdeac1b) line width.

### Outer Wall[¶](line-width.md#outer-wall) <a href="#outer-wall" id="outer-wall"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `outer_wall_line_width`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float or Percentage`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--outer-wall-line-width=20%`.\
Controls dimensional accuracy and surface finish.\
Recommended: **105%–120%** of the nozzle diameter for clean overhangs and detail.

### Inner Wall[¶](line-width.md#inner-wall) <a href="#inner-wall" id="inner-wall"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `inner_wall_line_width`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float or Percentage`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--inner-wall-line-width=20%`.\
Can be set wider than the outer wall to enhance structural strength.\
Typical value: **≥120%**.

### Top Surface[¶](line-width.md#top-surface) <a href="#top-surface" id="top-surface"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `top_surface_line_width`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float or Percentage`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--top-surface-line-width=20%`.\
Affects the quality of visible top layers.\
Recommended: **100%–105%** for smooth results without over-extrusion.

### Sparse Infill[¶](line-width.md#sparse-infill) <a href="#sparse-infill" id="sparse-infill"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `sparse_infill_line_width`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float or Percentage`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--sparse-infill-line-width=20%`.\
Recommended to use a conservative value, typically around 115% to improve layer adhesion without getting near volumetric flow limitations.\
If you need stronger infill, it's recommended to use [infill line multiplier](/broken/pages/da1f51648c030aebc578bfec4de7c7b47ec7ddd2#fill-multiline) when possible.

### Internal Solid Infill[¶](line-width.md#internal-solid-infill) <a href="#internal-solid-infill" id="internal-solid-infill"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `internal_solid_infill_line_width`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float or Percentage`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--internal-solid-infill-line-width=20%`.\
Used for internal solid infill, bottom surfaces, and [100% infill](/broken/pages/da1f51648c030aebc578bfec4de7c7b47ec7ddd2#sparse-infill-density).\
Recommended: **\~110%** for good layer adhesion and visual quality.

### Support[¶](line-width.md#support) <a href="#support" id="support"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `support_line_width`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float or Percentage`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--support-line-width=20%`.\
Typically set to **100%** to balance material usage and functionality. Reducing it too much can lead to weak support structures that may not hold up during printing or break easily during removal, leaving debris on the model.

### Bridge[¶](line-width.md#bridge) <a href="#bridge" id="bridge"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `bridge_line_width`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float or Percentage`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--bridge-line-width=20%`.\
Bridges are printed in mid-air, so the bridge line width can't exceed the nozzle diameter.\
To make adjacent bridge lines bond properly and reduce sagging, it's recommended to use **\~100%** of the nozzle diameter and increase [Bridge density](/broken/pages/c75388588c69e1995ba54b2c63be4b08ee7e271f#bridge-density).

![bridge\_line\_width\_1](https://www.orcaslicer.com/wiki/images/bridging/bridge_line_width_1.svg?raw=true) ![bridge\_line\_width\_2](https://www.orcaslicer.com/wiki/images/bridging/bridge_line_width_2.svg?raw=true)

Tip

If disabled (set to 0), [Internal Solid Infill](line-width.md#internal-solid-infill) line width will be used for bridges (thick bridges use the nozzle diameter instead).\
This allows you to use a theoretically wider line width for bridges.\
However, it is recommended to use [thick bridges](/broken/pages/c75388588c69e1995ba54b2c63be4b08ee7e271f#thick-bridges) or a [bridge flow adjustment](/broken/pages/c75388588c69e1995ba54b2c63be4b08ee7e271f#flow-ratio) instead.
