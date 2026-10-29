# Material Basic Information¶

This section contains basic information about the filament material.

* [Type](material-basic-information.md#type)
* [Vendor](material-basic-information.md#vendor)
* [Soluble material](material-basic-information.md#soluble-material)
* [Support material](material-basic-information.md#support-material)
* [Filament ramming length](material-basic-information.md#filament-ramming-length)
* [Required nozzle HRC](material-basic-information.md#required-nozzle-hrc)
* [Default color](material-basic-information.md#default-color)
* [Diameter](material-basic-information.md#diameter)
* [Adhesiveness Category](material-basic-information.md#adhesiveness-category)
* [Density](material-basic-information.md#density)
* [Shrinkage (XY)](material-basic-information.md#shrinkage-xy)
* [Shrinkage (Z)](material-basic-information.md#shrinkage-z)
* [Price](material-basic-information.md#price)
* [Softening temperature](material-basic-information.md#softening-temperature)
* [Idle temperature](material-basic-information.md#idle-temperature)
* [Recommended nozzle temperature](material-basic-information.md#recommended-nozzle-temperature)

## Type[¶](material-basic-information.md#type) <a href="#type" id="type"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Simple`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `filament_type`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Text list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--filament-type=value`.\
Material base type (e.g., PLA, ABS, PETG, etc.).\
This setting affects coefficients used in various calculations, such as brim width or temperature warnings.

## Vendor[¶](material-basic-information.md#vendor) <a href="#vendor" id="vendor"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `filament_vendor`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Text list`.\
Not available via CLI — see [Setting Overrides](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides) for the full list of excluded keys.\
Vendor of filament. For show only.

## Soluble material[¶](material-basic-information.md#soluble-material) <a href="#soluble-material" id="soluble-material"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `filament_soluble`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Boolean list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--filament-soluble=1`.\
Soluble material is commonly used to print supports and support interfaces.

## Support material[¶](material-basic-information.md#support-material) <a href="#support-material" id="support-material"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `filament_is_support`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Boolean list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--filament-is-support=1`.\
Support material is commonly used to print supports and support interfaces.

## Filament ramming length[¶](material-basic-information.md#filament-ramming-length) <a href="#filament-ramming-length" id="filament-ramming-length"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `filament_change_length`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--filament-change-length=1`.\
When changing the extruder, it is recommended to extrude a certain length of filament from the original extruder. This helps minimize nozzle oozing.

## Required nozzle HRC[¶](material-basic-information.md#required-nozzle-hrc) <a href="#required-nozzle-hrc" id="required-nozzle-hrc"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Developer`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `required_nozzle_HRC`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Integer list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--required-nozzle-HRC=1`.\
Minimum HRC of nozzle required to print the filament. A value of 0 means no checking of the nozzle's HRC.

## Default color[¶](material-basic-information.md#default-color) <a href="#default-color" id="default-color"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `default_filament_colour`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Text list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--default-filament-colour=value`.\
Default filament color.\
Right click to reset value to system default.

## Diameter[¶](material-basic-information.md#diameter) <a href="#diameter" id="diameter"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Simple`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `filament_diameter`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--filament-diameter=1`.\
Filament diameter is used to calculate extrusion variables in G-code, so it is important that this is accurate and precise.

## Adhesiveness Category[¶](material-basic-information.md#adhesiveness-category) <a href="#adhesiveness-category" id="adhesiveness-category"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Developer`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `filament_adhesiveness_category`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Integer list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--filament-adhesiveness-category=1`.\
Filament category.

## Density[¶](material-basic-information.md#density) <a href="#density" id="density"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `filament_density`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--filament-density=1`.\
Filament density, for statistical purposes only.

## Shrinkage (XY)[¶](material-basic-information.md#shrinkage-xy) <a href="#shrinkage-xy" id="shrinkage-xy"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `filament_shrink`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Percentage list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--filament-shrink=20%`.\
Enter the shrinkage percentage that the filament will get after cooling (94% if you measure 94mm instead of 100mm).\
The part will be scaled in XY to compensate. Only the filament used for the perimeter is taken into account.\
Be sure to allow enough space between objects, as this compensation is done after the checks.

## Shrinkage (Z)[¶](material-basic-information.md#shrinkage-z) <a href="#shrinkage-z" id="shrinkage-z"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `filament_shrinkage_compensation_z`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Percentage list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--filament-shrinkage-compensation-z=20%`.\
Enter the shrinkage percentage that the filament will get after cooling (94% if you measure 94mm instead of 100mm). The part will be scaled in Z to compensate.

## Price[¶](material-basic-information.md#price) <a href="#price" id="price"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `filament_cost`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Float list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--filament-cost=1`.\
Filament price, for statistical purposes only.

## Softening temperature[¶](material-basic-information.md#softening-temperature) <a href="#softening-temperature" id="softening-temperature"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Simple`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `temperature_vitrification`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Integer list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--temperature-vitrification=1`.\
The material softens at this temperature, so when the bed temperature is equal to or greater than this, it's highly recommended to open the front door and/or remove the upper glass to avoid clogs.

## Idle temperature[¶](material-basic-information.md#idle-temperature) <a href="#idle-temperature" id="idle-temperature"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Simple`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `idle_temperature`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Integer list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--idle-temperature=1`.\
Nozzle temperature when the tool is currently not used in multi-tool setups. This is only used when 'Ooze prevention' is active in Print Settings. Set to 0 to disable.

## Recommended nozzle temperature[¶](material-basic-information.md#recommended-nozzle-temperature) <a href="#recommended-nozzle-temperature" id="recommended-nozzle-temperature"></a>

Min and max recommended nozzle temperature for this filament.
