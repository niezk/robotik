# Support Ironing¶

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `support_ironing`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--support-ironing=1`.\
Ironing uses a small flow to print over the top support interface again at the same height to make it smoother. This setting controls whether the support interface is ironed. When enabled, the top support interface and the raft interface are also printed solid.

This option is available only when the support has [top interface layers](/broken/pages/3f8a8399cbd6c2877a5fa0209e485a798a78d168#interface-layers) or a [raft](/broken/pages/95f71e091ed1cc246f563f406e1b5624bec1bd46) is used.

## Pattern[¶](support-ironing.md#pattern) <a href="#pattern" id="pattern"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `support_ironing_pattern`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `Choice`.\
[Options](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `rectilinear, concentric`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--support-ironing-pattern=rectilinear`.\
Select the ironing pattern to use.

## Flow[¶](support-ironing.md#flow) <a href="#flow" id="flow"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `support_ironing_flow`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Percentage`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--support-ironing-flow=20%`.\
The amount of material to extrude during ironing, relative to the flow of a normal support interface layer. Too high a value results in over-extrusion on the surface.

## Line Spacing[¶](support-ironing.md#line-spacing) <a href="#line-spacing" id="line-spacing"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `support_ironing_spacing`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--support-ironing-spacing=1`.\
The distance between the lines of ironing.
