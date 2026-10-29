# Extruder Clearance¶

Extruder clearance settings define the minimum distances required around the extruder to avoid collisions with the print bed, rods, or lid during printing. These settings are particularly important for printers with complex geometries or when using by-object printing modes.

## Radius[¶](extruder-clearance.md#radius) <a href="#radius" id="radius"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `extruder_clearance_radius`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--extruder-clearance-radius=1`.\
Clearance radius around extruder: used for collision avoidance in by-object printing.

## Distance to rod[¶](extruder-clearance.md#distance-to-rod) <a href="#distance-to-rod" id="distance-to-rod"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `extruder_clearance_dist_to_rod`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--extruder-clearance-dist-to-rod=1`.

Horizontal distance from the nozzle tip to the rod's farther edge. Besides by-object printing, it sizes the keep-out band the gantry rod sweeps around a prime tower printed with [no sparse layers](/broken/pages/5aa3302c55047356a98465bb114707e629d121d9#no-sparse-layers).

## Height to rod[¶](extruder-clearance.md#height-to-rod) <a href="#height-to-rod" id="height-to-rod"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `extruder_clearance_height_to_rod`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--extruder-clearance-height-to-rod=1`.\
Distance from the nozzle tip to the lower rod. Used for collision avoidance in by-object printing.

## Height to lid[¶](extruder-clearance.md#height-to-lid) <a href="#height-to-lid" id="height-to-lid"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `extruder_clearance_height_to_lid`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--extruder-clearance-height-to-lid=1`.\
Distance from the nozzle tip to the lid. Used for collision avoidance in by-object printing.
