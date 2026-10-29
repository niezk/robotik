# Printer Accessory¶

* [Nozzle type](printer-accessory.md#nozzle-type)
* [Nozzle HRC](printer-accessory.md#nozzle-hrc)
* [Auxiliary Part Cooling Fan](printer-accessory.md#auxiliary-part-cooling-fan)
  * [Auxiliary Fan](printer-accessory.md#auxiliary-fan)
    * [Simple option (indexes only → fan0, fan2, fan3)](printer-accessory.md#simple-option-indexes-only--fan0-fan2-fan3)
    * [Advanced option (Index ⇄ Name mapping)](printer-accessory.md#advanced-option-index--name-mapping)
      * [Quick customization](printer-accessory.md#quick-customization)
      * [Usage](printer-accessory.md#usage)
* [Support controlling chamber temperature](printer-accessory.md#support-controlling-chamber-temperature)
  * [Using Chamber Temperature Variables in Machine G-code](printer-accessory.md#using-chamber-temperature-variables-in-machine-g-code)
  * [Klipper Chamber Temperature](printer-accessory.md#klipper-chamber-temperature)
* [Support air filtration](printer-accessory.md#support-air-filtration)

## Nozzle type[¶](printer-accessory.md#nozzle-type) <a href="#nozzle-type" id="nozzle-type"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `nozzle_type[extruder_idx]`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Choice list`.\
[Options](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#choice): `undefine, hardened_steel, stainless_steel, tungsten_carbide, brass`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--nozzle-type=undefine`.\
The metallic material of the nozzle: This determines the abrasive resistance of the nozzle and what kind of filament can be printed.

## Nozzle HRC[¶](printer-accessory.md#nozzle-hrc) <a href="#nozzle-hrc" id="nozzle-hrc"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Developer`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `nozzle_hrc`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Integer`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--nozzle-hrc=1`.\
The Nozzle Hardness ([Hardness Rockwell C](https://en.wikipedia.org/wiki/Rockwell_hardness_test)) value is used in OrcaSlicer to validate nozzle compatibility with abrasive filaments and prevent nozzle damage during printing.

| Material         | Value |
| ---------------- | ----- |
| Disable Check    | 0     |
| Brass            | 2     |
| Stainless Steel  | 20    |
| Hardened Steel   | 55    |
| Tungsten Carbide | 85    |

## Auxiliary Part Cooling Fan[¶](printer-accessory.md#auxiliary-part-cooling-fan) <a href="#auxiliary-part-cooling-fan" id="auxiliary-part-cooling-fan"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `auxiliary_fan`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--auxiliary-fan=1`.\
Enable this option if machine has auxiliary part cooling fan.\
The speed will be set for each material in the [material cooling settings](/broken/pages/d7c372477cc904769ba325c42008522f74ffec75#auxiliary-part-cooling-fan).

G-code command:

```
M106 P2 S(0-255)
```

### Auxiliary Fan[¶](printer-accessory.md#auxiliary-fan) <a href="#auxiliary-fan" id="auxiliary-fan"></a>

OrcaSlicer uses `M106 P#` (Set Fan Speed) / `M107 P#` (Fan Off) to control any fans managed by the slicer. The `P` parameter indicates the fan index as defined by OrcaSlicer:

* `P0`: part cooling fan (default layer fan)
* `P1` (if present): an additional fan
* `P2`: often used as Aux / CPAP / Booster
* `P3` (and higher): sometimes Exhaust / Enclosure, etc.

With Klipper you can create macros that translate both the OrcaSlicer numeric fan index `P` and **human‑readable names** for your physical fans. This keeps compatibility with generated G‑code (M106 P0 / M106 P2 …) while letting you address fans by name internally.

Warning

Adjust pin names and parameters (power, cycle\_time, etc.) to match your hardware.

* [Nozzle type](printer-accessory.md#nozzle-type)
* [Nozzle HRC](printer-accessory.md#nozzle-hrc)
* [Auxiliary Part Cooling Fan](printer-accessory.md#auxiliary-part-cooling-fan)
  * [Auxiliary Fan](printer-accessory.md#auxiliary-fan)
    * [Simple option (indexes only → fan0, fan2, fan3)](printer-accessory.md#simple-option-indexes-only--fan0-fan2-fan3)
    * [Advanced option (Index ⇄ Name mapping)](printer-accessory.md#advanced-option-index--name-mapping)
      * [Quick customization](printer-accessory.md#quick-customization)
      * [Usage](printer-accessory.md#usage)
* [Support controlling chamber temperature](printer-accessory.md#support-controlling-chamber-temperature)
  * [Using Chamber Temperature Variables in Machine G-code](printer-accessory.md#using-chamber-temperature-variables-in-machine-g-code)
  * [Klipper Chamber Temperature](printer-accessory.md#klipper-chamber-temperature)
* [Support air filtration](printer-accessory.md#support-air-filtration)

#### Simple option (indexes only → fan0, fan2, fan3)[¶](printer-accessory.md#simple-option-indexes-only-fan0-fan2-fan3) <a href="#simple-option-indexes-only-fan0-fan2-fan3" id="simple-option-indexes-only-fan0-fan2-fan3"></a>

This is the original basic example where the `P` index is concatenated (`fan0`, `fan2`, `fan3`). Use it if you don't need custom names:

```
# Part cooling fan
[fan_generic fan0]
pin: PA7
cycle_time: 0.01
hardware_pwm: false

# Auxiliary fan (comment out if you don't have it)
[fan_generic fan2]
pin: PA8
cycle_time: 0.01
hardware_pwm: false

# Exhaust / enclosure fan (comment out if you don't have it)
[fan_generic fan3]
pin: PA9
cycle_time: 0.01
hardware_pwm: false

[gcode_macro M106]
gcode:
    {% set fan = 'fan' + (params.P|int if params.P is defined else 0)|string %}
    {% set speed = (params.S|float / 255 if params.S is defined else 1.0) %}
    SET_FAN_SPEED FAN={fan} SPEED={speed}

[gcode_macro M107]
gcode:
    {% set fan = 'fan' + (params.P|int if params.P is defined else 0)|string %}
    {% if params.P is defined %}
    SET_FAN_SPEED FAN={fan} SPEED=0
    {% else %}
    # No P -> turn off typical defined fans
    SET_FAN_SPEED FAN=fan0 SPEED=0
    SET_FAN_SPEED FAN=fan2 SPEED=0
    SET_FAN_SPEED FAN=fan3 SPEED=0
    {% endif %}
```

#### Advanced option (Index ⇄ Name mapping)[¶](printer-accessory.md#advanced-option-index-name-mapping) <a href="#advanced-option-index-name-mapping" id="advanced-option-index-name-mapping"></a>

Lets you use descriptive names like `CPAP`, `EXHAUST`, etc. Useful if you re‑wire or repurpose fans without changing slicer output. Just keep `fan_map` updated.

```
# Example with friendly names + comments showing OrcaSlicer index

[fan_generic CPAP]        # fan 0 OrcaSlicer
pin: PB7
max_power: 0.8
shutdown_speed: 0
kick_start_time: 0.100
cycle_time: 0.005
hardware_pwm: False
off_below: 0.10

[fan_generic EXHAUST]     # fan 3 OrcaSlicer
pin: PE5
#max_power:
#shutdown_speed:
cycle_time: 0.01
hardware_pwm: False
#kick_start_time:
off_below: 0.2

# If you had another (e.g. P2) add here:
# [fan_generic AUX]
# pin: PXn

[gcode_macro M106]
description: "Set fan speed (Orca compatible)"
gcode:
    {% set fan_map = {
        0: "CPAP",      # Orca P0 → CPAP blower
        3: "EXHAUST",   # Orca P3 → Exhaust
        # 2: "AUX",     # Uncomment if you define AUX
    } %}
    {% set p = params.P|int if 'P' in params else 0 %}
    {% set fan = fan_map[p] if p in fan_map else fan_map[0] %}
    {% set speed = (params.S|float / 255 if 'S' in params else 1.0) %}
    SET_FAN_SPEED FAN={fan} SPEED={speed}

[gcode_macro M107]
description: "Turn off fans. No P = all, P# = specific"
gcode:
    {% set fan_map = {
        0: "CPAP",
        3: "EXHAUST",
        # 2: "AUX",
    } %}
    {% if 'P' in params %}
        {% set p = params.P|int %}
        {% if p in fan_map %}
            SET_FAN_SPEED FAN={fan_map[p]} SPEED=0
        {% else %}
            RESPOND PREFIX="warn" MSG="Unknown fan index P{{p}}"
        {% endif %}
    {% else %}
        # No P -> turn off all mapped fans
        {% for f in fan_map.values() %}
            SET_FAN_SPEED FAN={f} SPEED=0
        {% endfor %}
    {% endif %}
```

**Quick customization**[**¶**](printer-accessory.md#quick-customization)

1. Add / remove entries in `fan_map` to reflect the indexes the slicer may use.
2. Keep comments like `# fan X OrcaSlicer` next to each `[fan_generic]` for easy correlation.
3. Tune `max_power`, `off_below`, `cycle_time` according to fan type (CPAP blower vs axial exhaust).

**Usage**[**¶**](printer-accessory.md#usage)

* From OrcaSlicer: `M106 P0 S255` (100% CPAP), `M106 P3 S128` (\~50% EXHAUST).
* Turn one off: `M107 P3`. Turn all off: `M107`.
* You can still manually use `SET_FAN_SPEED FAN=CPAP SPEED=0.7` in the Klipper console.

***

Pick the variant that best fits your workflow; the advanced version provides extra clarity and flexibility while remaining fully compatible with standard OrcaSlicer G-code output.

## Support controlling chamber temperature[¶](printer-accessory.md#support-controlling-chamber-temperature) <a href="#support-controlling-chamber-temperature" id="support-controlling-chamber-temperature"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `support_chamber_temp_control`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--support-chamber-temp-control=1`.\
OrcaSlicer use `M141/M191` command to control active chamber heater.

If your Filament's [Activate temperature control](/broken/pages/68b6b7d711b5de8eafb31dd2591fd5e4242529b5#print-chamber-temperature) and your printer `Support control chamber temperature` option are checked , OrcaSlicer will insert `M191` command at the beginning of the gcode (before `Machine G-code`).

![Chamber-Temperature-Control-Printer](<../../../.gitbook/assets/Chamber Temperature Control Printer.png>) ![Chamber-Temperature-Control-Material](<../../../.gitbook/assets/Chamber Temperature Control Material.png>)

Note

If the machine is equipped with an auxiliary fan, OrcaSlicer will automatically activate the fan during the heating period to help circulate air in the chamber.

### Using Chamber Temperature Variables in Machine G-code[¶](printer-accessory.md#using-chamber-temperature-variables-in-machine-g-code) <a href="#using-chamber-temperature-variables-in-machine-g-code" id="using-chamber-temperature-variables-in-machine-g-code"></a>

You can use chamber temperature variables in your `Machine G-code` to control the chamber temperature manually, if desired:

* To set the chamber temperature to the value specified for the first filament:

```
M191 S{chamber_temperature[0]}
```

* To set the chamber temperature to the highest value specified across all filaments:

```
M191 S{overall_chamber_temperature}
```

### Klipper Chamber Temperature[¶](printer-accessory.md#klipper-chamber-temperature) <a href="#klipper-chamber-temperature" id="klipper-chamber-temperature"></a>

If you are using Klipper, you can define these macros to control the active chamber heater. Bellow is a reference configuration for Klipper.

Important

Don't forget to change the pin name/values to the actual values you are using in the configuration.

```
[heater_generic chamber_heater]
heater_pin:PB10
max_power:1.0
# Orca note: here the temperature sensor should be the sensor you are using for chamber temperature, not the PTC sensor
sensor_type:NTC 100K MGB18-104F39050L32
sensor_pin:PA1
control = pid
pid_Kp = 63.418
pid_ki = 0.960
pid_kd = 1244.716
min_temp:0
max_temp:70

[gcode_macro M141]
gcode:
    SET_HEATER_TEMPERATURE HEATER=chamber_heater TARGET={params.S|default(0)}

[gcode_macro M191]
gcode:
    {% set s = params.S|float %}
    {% if s == 0 %}
        # If target temperature is 0, do nothing
        M117 Chamber heating cancelled
    {% else %}
        SET_HEATER_TEMPERATURE HEATER=chamber_heater TARGET={s}
        # Orca: uncomment the following line if you want to use heat bed to assist chamber heating
        # M140 S100
        TEMPERATURE_WAIT SENSOR="heater_generic chamber_heater" MINIMUM={s-1} MAXIMUM={s+1}
        M117 Chamber at target temperature
    {% endif %}
```

## Support air filtration[¶](printer-accessory.md#support-air-filtration) <a href="#support-air-filtration" id="support-air-filtration"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Developer`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `support_air_filtration`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--support-air-filtration=1`.\
Air Filtration/Exhaust Fan Control in OrcaSlicer.\
OrcaSlicer use `M106 P3` command to control air-filtration/exhaust fan.

If you are using Klipper, you can define a `M106` macro to control both the normal part cooling fan, auxiliary fan, and exhaust fan.

Below is a reference configuration for Klipper.

Note

Don't forget to change the pin name to the actual pin name you are using in the configuration.

```
# instead of using [fan], we define the default part cooling fan with [fan_generic] here
# this is the default part cooling fan
[fan_generic fan0]
pin: PA7
cycle_time: 0.01
hardware_pwm: false

# this is the auxiliary fan
# comment out it if you don't have auxiliary fan
[fan_generic fan2]
pin: PA8
cycle_time: 0.01
hardware_pwm: false

# this is the exhaust fan
# comment out it if you don't have exhaust fan
[fan_generic fan3]
pin: PA9
cycle_time: 0.01
hardware_pwm: false

[gcode_macro M106]
gcode:
    {% set fan = 'fan' + (params.P|int if params.P is defined else 0)|string %}
    {% set speed = (params.S|float / 255 if params.S is defined else 1.0) %}
    SET_FAN_SPEED FAN={fan} SPEED={speed}
```
