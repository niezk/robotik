# Support¶

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Simple`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `enable_support`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--enable-support=1`.\
Support structures are used in 3D printing to provide stability to overhangs and complex geometries.

* [Type](support.md#type)
  * [Normal](support.md#normal)
  * [Tree](support.md#tree)
    * [Support critical regions only](support.md#support-critical-regions-only)
  * [Auto](support.md#auto)
  * [Manual](support.md#manual)
* [Style](support.md#style)
  * [Grid](support.md#grid)
  * [Snug](support.md#snug)
  * [Organic](support.md#organic)
  * [Tree Slim](support.md#tree-slim)
  * [Tree Strong](support.md#tree-strong)
  * [Tree Hybrid](support.md#tree-hybrid)
* [Threshold angle](support.md#threshold-angle)
* [Threshold overlap](support.md#threshold-overlap)
* [Initial layer density](support.md#initial-layer-density)
* [Initial layer expansion](support.md#initial-layer-expansion)
* [On build plate only](support.md#on-build-plate-only)
* [Ignore small overhangs](support.md#ignore-small-overhangs)

## Type[¶](support.md#type) <a href="#type" id="type"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Simple`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `support_type`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `Choice`.\
[Options](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `normal(auto), tree(auto), normal(manual), tree(manual)`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--support-type=normal(auto)`.\
There are several support types, each suited for different printing needs:

### Normal[¶](support.md#normal) <a href="#normal" id="normal"></a>

Normal support structures are projected straight down from the overhangs, providing a stable base for overhangs and complex geometries.

### Tree[¶](support.md#tree) <a href="#tree" id="tree"></a>

Tree-like support structures are designed to minimize material usage while still providing adequate support. They branch out from a central trunk, allowing for more efficient printing.

#### Support critical regions only[¶](support.md#support-critical-regions-only) <a href="#support-critical-regions-only" id="support-critical-regions-only"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `support_critical_regions_only`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--support-critical-regions-only=1`.\
Only creates support for critical regions, such as sharp tails and cantilevers. Available only with `Tree (auto)`.

### Auto[¶](support.md#auto) <a href="#auto" id="auto"></a>

Automatically generates support wherever the model's overhangs need it, as well as where support enforcers are placed in the Prepare view.

### Manual[¶](support.md#manual) <a href="#manual" id="manual"></a>

Only generates support where support enforcers are placed in the Prepare view.

## Style[¶](support.md#style) <a href="#style" id="style"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `support_style`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `Choice`.\
[Options](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `default, grid, snug, organic, tree_slim, tree_strong, tree_hybrid`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--support-style=default`.\
Style and shape of the support.\
Grid and Snug apply to normal supports, while Organic, Tree Slim, Tree Strong and Tree Hybrid apply to tree supports. `Default (Grid/Organic)` uses Grid for normal supports and Organic for tree supports.

### Grid[¶](support.md#grid) <a href="#grid" id="grid"></a>

Default for normal supports. Projecting the supports into a regular grid creates more stable supports.

### Snug[¶](support.md#snug) <a href="#snug" id="snug"></a>

Snug support towers save material and reduce object scarring.

### Organic[¶](support.md#organic) <a href="#organic" id="organic"></a>

Default style for tree supports. Like Tree Slim, it merges branches more aggressively and saves a lot of material.

### Tree Slim[¶](support.md#tree-slim) <a href="#tree-slim" id="tree-slim"></a>

Slim tree support branches are designed to be more delicate and use less material while still providing adequate support.

### Tree Strong[¶](support.md#tree-strong) <a href="#tree-strong" id="tree-strong"></a>

Strong tree support branches are designed to be more robust and provide additional support for heavier overhangs.

### Tree Hybrid[¶](support.md#tree-hybrid) <a href="#tree-hybrid" id="tree-hybrid"></a>

Creates a structure similar to normal support under large flat overhangs.

## Threshold angle[¶](support.md#threshold-angle) <a href="#threshold-angle" id="threshold-angle"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Simple`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `support_threshold_angle`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Integer`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--support-threshold-angle=1`.\
Support will be generated for overhangs whose slope angle is below the threshold. The smaller this value is, the steeper the overhang that can be printed without support.\
If set to `0`, normal supports use the [Threshold overlap](support.md#threshold-overlap) instead, while tree supports use 30°.

## Threshold overlap[¶](support.md#threshold-overlap) <a href="#threshold-overlap" id="threshold-overlap"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Simple`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `support_threshold_overlap`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float or Percentage`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--support-threshold-overlap=20%`.\
If [Threshold angle](support.md#threshold-angle) is zero, support will be generated for overhangs whose overlap with the layer below is below the threshold. A percentage is relative to the outer wall line width. The smaller this value is, the steeper the overhang that can be printed without support.\
Tree supports don't use this setting, so it is hidden for them.

## Initial layer density[¶](support.md#initial-layer-density) <a href="#initial-layer-density" id="initial-layer-density"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `raft_first_layer_density`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Percentage`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--raft-first-layer-density=20%`.\
Density of the first raft or support layer.

## Initial layer expansion[¶](support.md#initial-layer-expansion) <a href="#initial-layer-expansion" id="initial-layer-expansion"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `raft_first_layer_expansion`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--raft-first-layer-expansion=1`.\
Expands the first raft or support layer to improve build plate adhesion. It is disabled for the Tree Slim and Tree Strong styles unless a raft is used.

## On build plate only[¶](support.md#on-build-plate-only) <a href="#on-build-plate-only" id="on-build-plate-only"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Simple`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `support_on_build_plate_only`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--support-on-build-plate-only=1`.\
Don't create support on the model surface, only on the build plate.

## Ignore small overhangs[¶](support.md#ignore-small-overhangs) <a href="#ignore-small-overhangs" id="ignore-small-overhangs"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `support_remove_small_overhang`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--support-remove-small-overhang=1`.\
With this setting, small overhangs that possibly don't need support are ignored by support generation.
