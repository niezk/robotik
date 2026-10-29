# Cooling Fan¶

Machine cooling fan settings.

* [Fan speed-up time](cooling-fan.md#fan-speed-up-time)
  * [Only overhangs](cooling-fan.md#only-overhangs)
* [Fan kick-start time](cooling-fan.md#fan-kick-start-time)
* [Minimum non-zero part cooling fan speed](cooling-fan.md#minimum-non-zero-part-cooling-fan-speed)

## Fan speed-up time[¶](cooling-fan.md#fan-speed-up-time) <a href="#fan-speed-up-time" id="fan-speed-up-time"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variables](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `fan_speedup_time`, `fan_speedup_overhangs`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb): `fan_speedup_time` (Float), `fan_speedup_overhangs` (Boolean).\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--fan-speedup-time=1` (`fan_speedup_time` shown; other variables above follow their own type).\
Start the fan this number of seconds earlier than its target start time (you can use fractional seconds). It assumes infinite acceleration for this time estimation, and will only take into account G1 and G0 moves (arc fitting is unsupported). It won't move fan commands from custom G-code (they act as a sort of 'barrier'). It won't move fan commands into the start G-code if the 'only custom start G-code' is activated. Use 0 to deactivate.

### Only overhangs[¶](cooling-fan.md#only-overhangs) <a href="#only-overhangs" id="only-overhangs"></a>

Will only take into account the delay for the cooling of overhangs.

## Fan kick-start time[¶](cooling-fan.md#fan-kick-start-time) <a href="#fan-kick-start-time" id="fan-kick-start-time"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `fan_kickstart`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Float`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--fan-kickstart=1`.\
Emit a max fan speed command for this amount of seconds before reducing to target speed to kick-start the cooling fan. This is useful for fans where a low PWM/power may be insufficient to get the fan started spinning from a stop, or to get the fan up to speed faster. Set to 0 to deactivate.

## Minimum non-zero part cooling fan speed[¶](cooling-fan.md#minimum-non-zero-part-cooling-fan-speed) <a href="#minimum-non-zero-part-cooling-fan-speed" id="minimum-non-zero-part-cooling-fan-speed"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `part_cooling_fan_min_pwm`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Integer`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--part-cooling-fan-min-pwm=1`.\
Some part-cooling fans cannot start spinning when commanded below a certain PWM duty cycle. When set above 0, any non-zero part-cooling fan command will be raised to at least this percentage so the fan reliably starts.\
A fan command of 0 (fan off) is always honoured exactly.\
This clamp is applied after every other fan calculation (first-layer ramp, layer-time interpolation, overhang/bridge/support-interface/ironing overrides), so scaling still operates within the range \[this value, 100%].\
If your firmware already disables the fan below a threshold (for example Klipper's \[fan] off\_below: 0.10 shuts the fan off whenever the commanded duty cycle is below 10%), this option and the firmware threshold should ideally be set to the same value.\
Matching them (e.g. off\_below: 0.10 in Klipper and 10% here) guarantees the slicer never emits a non-zero value that the firmware would silently drop, and the fan never receives a value below the one you know it can actually spool at.\
Set to 0 to deactivate.
