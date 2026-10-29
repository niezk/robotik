# Z Hop¶

Z-Hop is a feature that lifts the nozzle slightly during travel moves to avoid collisions with the printed object. This is particularly useful for prints with tall, thin features or when printing multiple objects on the build plate.

## On surfaces[¶](z-hop.md#on-surfaces) <a href="#on-surfaces" id="on-surfaces"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `retract_lift_enforce[extruder_idx]`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Choice list`.\
[Options](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `All Surfaces, Top Only, Bottom Only, Top and Bottom`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--retract-lift-enforce="All Surfaces"`.\
Enforce Z-Hop behavior. This setting is impacted by the above settings (Only lift Z above/below).

## Z-hop type[¶](z-hop.md#z-hop-type) <a href="#z-hop-type" id="z-hop-type"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `z_hop_types[extruder_idx]`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Choice list`.\
[Options](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `Auto Lift, Normal Lift, Slope Lift, Spiral Lift`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--z-hop-types="Auto Lift"`.\
\- Auto: Selects automatically between Spiral based on whether the travel move crosses over overhang areas - Normal Lift: The nozzle is lifted vertically during retraction and lowered back down before resuming printing. - Slope: The nozzle moves diagonally (at an angle) during retraction, creating a sloped path. - Spiral: The nozzle moves in a spiral pattern while lifting, which can help reduce stringing and improve print quality.

## Z-hop height[¶](z-hop.md#z-hop-height) <a href="#z-hop-height" id="z-hop-height"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Simple`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `z_hop[extruder_idx]`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--z-hop=1`.\
Whenever there is a retraction, the nozzle is lifted a little to create clearance between the nozzle and the print. This prevents the nozzle from hitting the print when traveling more. Using spiral lines to lift z can prevent stringing.

## Traveling angle[¶](z-hop.md#traveling-angle) <a href="#traveling-angle" id="traveling-angle"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `travel_slope[extruder_idx]`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--travel-slope=1`.\
Traveling angle for Slope and Spiral Z-hop type. Setting it to 90° results in Normal Lift.

## Only lift Z above[¶](z-hop.md#only-lift-z-above) <a href="#only-lift-z-above" id="only-lift-z-above"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `retract_lift_above[extruder_idx]`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--retract-lift-above=1`.\
If you set this to a positive value, Z lift will only take place above the specified absolute Z.

## Only lift Z below[¶](z-hop.md#only-lift-z-below) <a href="#only-lift-z-below" id="only-lift-z-below"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `retract_lift_below[extruder_idx]`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--retract-lift-below=1`.\
If you set this to a positive value, Z lift will only take place below the specified absolute Z.
