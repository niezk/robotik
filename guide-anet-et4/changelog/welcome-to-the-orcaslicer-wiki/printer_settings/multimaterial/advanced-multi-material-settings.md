# Advanced Multi-Material Settings¶

This section describes advanced settings for multi-material printing.

## Filament load time[¶](advanced-multi-material-settings.md#filament-load-time) <a href="#filament-load-time" id="filament-load-time"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `machine_load_filament_time`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--machine-load-filament-time=1`.\
Time to load new filament when switch filament. It's usually applicable for single-extruder multi-material machines. For tool changers or multi-tool machines, it's typically 0. For statistics only.

## Filament unload time[¶](advanced-multi-material-settings.md#filament-unload-time) <a href="#filament-unload-time" id="filament-unload-time"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `machine_unload_filament_time`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--machine-unload-filament-time=1`.\
Time to unload old filament when switch filament. It's usually applicable for single-extruder multi-material machines. For tool changers or multi-tool machines, it's typically 0. For statistics only.

## Tool change time[¶](advanced-multi-material-settings.md#tool-change-time) <a href="#tool-change-time" id="tool-change-time"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `machine_tool_change_time`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--machine-tool-change-time=1`.\
Time taken to switch tools. It's usually applicable for tool changers or multi-tool machines. For single-extruder multi-material machines, it's typically 0. For statistics only.
