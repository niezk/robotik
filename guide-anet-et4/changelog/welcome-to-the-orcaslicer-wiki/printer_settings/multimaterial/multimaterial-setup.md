# Multimaterial setup¶

Basic setup for multimaterial printing.

## Single Extruder Multi Material[¶](multimaterial-setup.md#single-extruder-multi-material) <a href="#single-extruder-multi-material" id="single-extruder-multi-material"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `single_extruder_multi_material`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--single-extruder-multi-material=1`.\
Allow using a single extruder to print with multiple filaments.\
If your printer has an MultiMaterialUnit, this will run the [Change filament G-code](/broken/pages/8a0cca48a8cb689eb2e37db1bc877c26189bf981#change-filament-g-code) when changing filament is needed. If your printer does not have an MultiMaterialUnit, you will need to enable [Manual Filament Change](multimaterial-setup.md#manual-filament-change).

## Extruders[¶](multimaterial-setup.md#extruders) <a href="#extruders" id="extruders"></a>

Number of extruders of the printer.

## Manual Filament Change[¶](multimaterial-setup.md#manual-filament-change) <a href="#manual-filament-change" id="manual-filament-change"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `manual_filament_change`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--manual-filament-change=1`.\
Manual filament change is a feature that allows the user to change the filament during the print. This can be useful for multi-material prints or when changing colors. The user can specify the position and timing of the filament change, as well as the speed and distance of the ramming process.\
Enable this option to omit the custom Change filament G-code only at the beginning of the print. The tool change command (e.g., T0) will be skipped throughout the entire print. This is useful for manual multi-material printing, where we use M600/PAUSE to trigger the manual filament change action.
