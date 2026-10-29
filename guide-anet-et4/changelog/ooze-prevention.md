# Ooze prevention¶

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `ooze_prevention`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--ooze-prevention=1`.\
This option will drop the temperature of the inactive extruders to prevent oozing.

## Temperature variation[¶](ooze-prevention.md#temperature-variation) <a href="#temperature-variation" id="temperature-variation"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `standby_temperature_delta`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Integer`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--standby-temperature-delta=1`.\
Temperature difference to be applied when an extruder is not active. The value is not used when [Idle temperature](/broken/pages/517fb235be4603cea00c908adde9ed8048ec88d6#idle-temperature) in the filament settings is set to a non-zero value.

## Preheat time[¶](ooze-prevention.md#preheat-time) <a href="#preheat-time" id="preheat-time"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `preheat_time`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--preheat-time=1`.\
To reduce the waiting time after tool change, Orca can preheat the next tool while the current tool is still in use. This setting specifies the time in seconds to preheat the next tool. Orca will insert an M104 command to preheat the tool in advance.

## Preheat steps[¶](ooze-prevention.md#preheat-steps) <a href="#preheat-steps" id="preheat-steps"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Developer`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `preheat_steps`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Integer`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--preheat-steps=1`.\
Inserts multiple preheat commands (e.g. M104.1). Only useful for the Prusa XL. For other printers, set it to 1.
