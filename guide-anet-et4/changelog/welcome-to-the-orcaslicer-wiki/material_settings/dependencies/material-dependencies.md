# Material Dependencies¶

Material dependencies help ensure that a material profile is only used with compatible printer and process profiles, preventing potential printing issues.

## Compatible printers[¶](material-dependencies.md#compatible-printers) <a href="#compatible-printers" id="compatible-printers"></a>

Set of printers that this material profile is compatible with if you want to limit its usage to specific printers.

### Printer Condition[¶](material-dependencies.md#printer-condition) <a href="#printer-condition" id="printer-condition"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `compatible_printers_condition`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#text): `Text`.\
Not available via CLI — see [Setting Overrides](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides) for the full list of excluded keys.\
boolean expression using the configuration values of an active printer profile.\
If this expression evaluates to true, this profile is considered compatible with the active printer profile.

## Compatible process profiles[¶](material-dependencies.md#compatible-process-profiles) <a href="#compatible-process-profiles" id="compatible-process-profiles"></a>

Set of process profiles that this material profile is compatible with if you want to limit its usage to specific process profiles.

### Process Condition[¶](material-dependencies.md#process-condition) <a href="#process-condition" id="process-condition"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `compatible_prints_condition`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#text): `Text`.\
Not available via CLI — see [Setting Overrides](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides) for the full list of excluded keys.\
A boolean expression using the configuration values of an active print profile.\
If this expression evaluates to true, this profile is considered compatible with the active print profile.
