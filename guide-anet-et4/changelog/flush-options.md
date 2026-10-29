# Flush Options¶

## Flush into objects' infill[¶](flush-options.md#flush-into-objects-infill) <a href="#flush-into-objects-infill" id="flush-into-objects-infill"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Simple`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `flush_into_infill`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--flush-into-infill=1`.\
Purging after a filament change will be done inside the objects' infill. This may lower the amount of waste and decrease the print time. If the walls are printed with transparent filament, the mixed color infill will be visible. It will not take effect unless the prime tower is enabled. With a Type 2 [wipe tower](/broken/pages/74f57ccd9ce07fa1f5a18d2766d92d9e5cb458ca), purging into objects is only used on single extruder multi-material printers with [Purge in prime tower](/broken/pages/74f57ccd9ce07fa1f5a18d2766d92d9e5cb458ca#purge-in-prime-tower) enabled.

## Flush into this object[¶](flush-options.md#flush-into-this-object) <a href="#flush-into-this-object" id="flush-into-this-object"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Simple`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `flush_into_objects`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--flush-into-objects=1`.\
Purging after a filament change will be done by printing this object's walls and infill with the new filament. This may lower the amount of waste and decrease the print time, but the colors of the object will be mixed as a result. Objects with this option are used for purging before the infill of other objects, and whatever they can't take is still purged on the prime tower. It will not take effect unless the prime tower is enabled. With a Type 2 [wipe tower](/broken/pages/74f57ccd9ce07fa1f5a18d2766d92d9e5cb458ca), purging into objects is only used on single extruder multi-material printers with [Purge in prime tower](/broken/pages/74f57ccd9ce07fa1f5a18d2766d92d9e5cb458ca#purge-in-prime-tower) enabled.

This is a per-object setting, so it isn't shown in the global process settings. Right-click the object in the object list or in the 3D view and check **Flush Options** > **Flush into this object**, or switch the process settings from **Global** to **Objects**, select the object and change it there. The **Flush Options** menu only appears when the plate uses more than one filament.

## Flush into objects' support[¶](flush-options.md#flush-into-objects-support) <a href="#flush-into-objects-support" id="flush-into-objects-support"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Simple`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `flush_into_support`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--flush-into-support=1`.\
Purging after a filament change will be done inside the objects' support. This may lower the amount of waste and decrease the print time. It will not take effect unless the prime tower is enabled. With a Type 2 [wipe tower](/broken/pages/74f57ccd9ce07fa1f5a18d2766d92d9e5cb458ca), purging into objects is only used on single extruder multi-material printers with [Purge in prime tower](/broken/pages/74f57ccd9ce07fa1f5a18d2766d92d9e5cb458ca#purge-in-prime-tower) enabled.
