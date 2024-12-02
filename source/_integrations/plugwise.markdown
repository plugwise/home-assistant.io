---
title: Plugwise
description: Plugwise Smile platform integration.
ha_category:
  - Binary sensor
  - Button
  - Climate
  - Number
  - Select
  - Sensor
  - Switch
ha_iot_class: Local Polling
ha_release: 0.98
ha_codeowners:
  - '@CoMPaTech'
  - '@bouwew'
  - '@frenck'
ha_config_flow: true
ha_domain: plugwise
ha_zeroconf: true
ha_platforms:
  - binary_sensor
  - button
  - climate
  - diagnostics
  - number
  - select
  - sensor
  - switch
ha_integration_type: hub
---

[Plugwise](https://www.plugwise.com) provides smart home Climate and power monitoring equipment. You can acquire one of their network attached hubs, called Smiles, to monitor and/or control your home. 

This integration supports Plugwise equipment connected through a **Smile**. The smile functions as a hub where you can connect to from either their Plugwise App or using this Home Assistant integration. There are 4 types of Smiles provding:

- Full zonecontrol using the [Adam](https://www.plugwise.com/en_US/zonecontrol) and additional devices, or
- A stand-alone smart thermostat called [Anna](https://www.plugwise.com/en_US/products/anna).
- For power monitoring there is one simply called the [P1](https://www.plugwise.com/en_US/products/smile-p1).
- Although no longer sold, there also is the Stretch, a gateway to create network connectivity for their older power products.

For zonecontrol there are additional devices available, including smart valves and smart plugs, see [Supported devices](#supported-devices) for a complete overview.

{% note %}
Plugwise formerly sold Power based products comprised of a USB stick and smart plugs (amongst a few other items). This integration does **not** support the USB-stick. Re-use of the these products using a Stretch or an Adam is supported. Work for USB support is in development but not ready to become a formal Home Assistant integration yet. 
{% endnote %}

## Platforms

Depending on your specific Smile and available devices, the following platforms are available:

 - `climate` (for the stand-alone Anna, for Adam, a climate entity is shown for each zone containing devices like an Anna or another type of wired-thermostat, Jip or Lisa combined with one or more Tom/Floor devices)
 - `binary_sensor` (for showing the status of e.g. domestic hot water heating or secondary heater)
 - `button` (for the Adam and the non-legacy Anna and P1 gateways)
 - `number` (for changing a boiler setpoint, a temperature offset)
 - `sensor` (for all relevant products including the Smile P1)
 - `select` (for changing a thermostat schedule, a regulation mode (Adam only))
 - `switch` (for Plugs connected to Adam, or Circles and Stealths connected to a Stretch)

## Pre-requisites

The Plugwise Smile(s) in your network will be automatically discovered and shown on the integrations dashboard. All you need is the Smile ID as its password, which is an 8-character string printed on the sticker on the bottom of your Smile. Repeat this for each individual Smile.

{% include integrations/config_flow.md %}

{% configuration_basic %}
Host:
  description: "The hostname or IP address of your Smile. For example: `192.168.1.25`. You can find it in your router or in the Plugwise app using the **Settings** icon (&#9776;) -> **System** -> **Network**. If you are looking for a different device in the Plugwise App, on the main screen first select **Gateways** -> the Smile of your choice, and then follow the previous instruction. Normally, the Smile(s) are automatically discovered, and you don't have to provide the hostname or IP address."
Username:
  description: "Username to log in to the Smile. This should be just `smile` - or `stretch` for a Stretch."
Password:
  description: "This is the password (i.e. Smile ID) printed on the sticker on the back of your Smile (i.e. Adam, Smile-T, or P1) and should be 8 characters long."
{% endconfiguration_basic %}

### Further configuration

For a thermostat, the active schedule can be deactivated or reactivated via the climate card. Please note, that when no schedule is active, one must first be activated in the Plugwise App. Once that has been done, the Plugwise Integration can manage future operations.

Auto means the schedule is active, and Heat means it's not active. The active thermostat schedule can be changed via the connected thermostat select entity. Please note that only schedules with two or more schedule points will be shown as select options.

## Configuration

{% important %}
 - When you have an Anna and an Adam, only the Adam will be shown as discovered. Make sure to **only** configure the Adam integration, do **not** manually configure the Anna.
 - If you have an Elga connected to an Anna, please check the note in [Supported devices](#supported-devices)
{% endimportant %}

The Plugwise Smile(s) present in your network will be automatically discovered via Zeroconf discovery and will be shown on the Integrations-page. All you need is the Smile ID as its password, which is an 8 character string printed on the sticker on the bottom of your Smile. Repeat this for each individual Smile.

{% include integrations/config_flow.md %}

{% configuration_basic %}
Host:
  description: "The hostname or IP address of your Smile. For example: `192.168.1.25`. You can find it in your router or in the Plugwise app using the **Settings** icon (&#9776;) -> **System** -> **Network**. If you are looking for a different device in the Plugwise App, on the main screen first select **Gateways** -> the Smile of your choice, and then follow the previous instruction. Normally, the Smile(s) are automatically discovered, and you don't have to provide the hostname or IP address."
Username:
  description: "Username to log in to the Smile. This should be just 'smile' - or 'stretch' for a Stretch'."
Password:
  description: "This is the password (i.e. Smile ID) printed on the sticker on the back of your Smile (i.e. Adam, Smile-T, or P1) and should be 8 characters long."
{% endconfiguration_basic %}

### Further configuration

For a thermostat, the active schedule can be deactivated or reactivated via the climate card. Please note, that when no schedule is active, one must first be activated in the Plugwise App. Once that has been done the Plugwise Integration can manage future operations.

`Auto` means the schedule is active, while `Heat` means it's not active. The active thermostat schedule can be changed via the connected thermostat select-entity. Please note that only schedules with two or more schedule points will be shown as select options.

## Before configuring

{% important %}
When you have an Anna and an Adam, make sure to **only** configure the Adam integration. You can press the "IGNORE" button on the auto-discovered Anna integration to hide this integration. In case you need to rediscover the Anna integration, make sure to click the "STOP IGNORING" button on the Plugwise integration first, available via "show ignored integrations".
{% endimportant %}

The Plugwise Smile(s) present in your network will be automatically detected via Zeroconf discovery and will be shown on the Integrations-page. All you need is the Smile ID as it's password, which is an 8 character string printed on the sticker on the bottom of you smile. To set up Plugwise when a Smile is not auto-discovered you can use this My Button:

{% include integrations/config_flow.md %}
{% configuration_basic %}
Host:
    description: "The hostname or IP address of your Smile. For example: '192.168.1.25'. You can find it in your router or in the Plugwise app using the **Settings** icon (&#9776;) -> **System** -> **Network **. If you are looking for a different device in the Plugwise App, on the main screen first select **Gateways** -> the Smile of your choice, and then follow the previous instruction. Normally the Smile(s) are automatically discovered and you don't have to provide the hostname or IP address."
    required: true
    type: string
Username:
    description: "Username to log in to the Smile. This should be just 'smile' - or 'stretch' for a Stretch'."
    required: true
    type: string
Password:
    description: "This is the password (i.e. Smile ID) printed on the sticker on the bottom of your Smile and should be 8 characters long".
    required: true
    type: string
{% endconfiguration_basic %}

Repeat the above procedure for each Smile gateway (i.e., if you have an Adam setup and a P1 DSMR you'll have to add two integrations).

### Further configuration

For a thermostat, the active schedule can be deactivated or reactivated via the climate card. Please note, that when no schedule is active, one must first be activated in the Plugwise App. Once that has been done the Plugwise Integration can manage future operations.

Auto means the schedule is active, Heat means it's not active. The active thermostat schedule can be changed via the connected thermostat select-entity. Please note: that only schedules that have two or more schedule points will be shown as select options.

## Entities

This integration will show all Plugwise devices (like hardware devices, multi-thermostat climate-zones, and virtual switchgroups) present in your Plugwise configuration. In addition, you will see a Gateway device representing your central Plugwise gateway (i.e., the Smile Anna, Smile P1, Adam or Stretch).

For example, if you have an Adam setup with a Lisa named 'Living' and a Tom named 'Bathroom', these will show up as individual devices. The heating/cooling device connected to your Smile will be shown as 'OpenTherm' or 'OnOff', depending on how the Smile communicates with the device. If you have Plugs (as in, pluggable switches connecting to an Adam) those will be shown as devices as well.

Under each device there will be entities shown like binary_sensors, sensors, etc. depending on the capabilities of the device: for instance centralized measurements such as 'power' for a P1, 'outdoor_temperature' on Anna or Adam will be assigned to your gateway device. Heating/cooling device measurements such as 'boiler_temperature' will be assigned to the OpenTherm/OnOff device.

## Data updates

The interval which the integration fetches data from the Smile depends on the device:

- 10 seconds for power entities, such as the P1 and plugs.
- 60 seconds for all climate entities.
- 60 seconds for all Stretch entities.

## Removing the integration

This integration follows standard integration removal. No extra steps are required within Home Assistant or on your Plugwise devices.

{% include integrations/remove_device_service.md %}

This will also remove all connected Adam devices (such as Anna, Tom or Lisa) or connected Adam/Stretch plugs.

## Examples 

### Actions

#### Set HVAC mode

action: `climate.set_hvac_mode`

Available options include `off` (Adam only) `auto`, `cool`, `heat`, and `heat_cool` (Anna with Elga only).

The meaning of `off` is that the Adam regulation is set to off. This means that the connected HVAC-system does not heat or cool, only the domestic hot water heating function, when available, is active.

The meaning of `cool` or `heat` is that there is no schedule active. For example, if the system is manually set to cooling- or heating-mode, the system will be active if the room temperature is above/below the thermostat setpoint.

The meaning of `heat/cool` is that there is no schedule active. For example, if the system is in automatic cooling- or heating-mode, the active preset or manually set temperature is used to control the HVAC system.

The meaning of `auto` is that a schedule is active and the thermostat will change presets/setpoints accordingly.

The last schedule that was active is determined the same way long-tapping the top of Anna works.

Example:

```yaml
# Example script climate.set_hvac_mode to auto = schedule active
script:
  lisa_reactivate_last_schedule:
    sequence:
      - action: climate.set_hvac_mode
        target:
          entity_id: climate.living_room
        data:
          hvac_mode: auto
```

#### Turn on / turn off

action: `climate.turn_off`, `climate.turn_on` (Adam only)

These actions will switch the Adam regulation mode (= HVAC system mode) to off or on, affecting the operation of all connected thermostats.
`climate.turn_on` will activate the previously selected heating or cooling mode.

Example:

```yaml
# Example script climate.turn_off
script:
  turn_heating_on:
    sequence:
      - action: climate.turn_off
        target:
          entity_id: climate.bios
```

#### Change climate schedule

action: `select.select_option`

```yaml
# Example script change the thermostat schedule
script:
  lisa_change_schedule:
    sequence:
      - action: select.select_option
        target:
          entity_id: select.bios_thermostat_schedule
        data:
          option: "Regulier"
```

#### Change boiler setpoint

action: `number.set_value`

```yaml
# Example script change the boiler setpoint
script:
  change_max_boiler_tempeture_setpoint:
    sequence:
      - action: number.set_value
        target:
          entity_id: number.opentherm_max_boiler_temperature_setpoint
        data:
          value: 60
```

#### Set temperature

action: `climate.set_temperature`

Example:

```yaml
# Example script change the temperature
script:
  anna_set_predefined_temperature:
    sequence:
      - action: climate.set_temperature
        target:
          entity_id: climate.anna
        data:
          temperature: 19.5
```

#### Set preset mode

action: `climate.set_preset_mode`

Available options include: `home`, `vacation` (Anna only), `no_frost`, `asleep` & `away`.

Example:

```yaml
# Example script changing the active (or currently set by schedule) preset
script:
  anna_activate_preset_asleep:
    sequence:
      - action: climate.set_preset_mode
        data:
          preset_mode: asleep
```

### Troubleshooting

#### Modify the Smile update interval

{% include common-tasks/define_custom_polling.md %}

#### Diagnostic data

If you need to create an issue to report a bug or want to inspect diagnostic data use the below method

To retrieve diagnostics:

1. Go to {% my integrations title="**Settings** > **Devices & services**" %}, and select your integration.
2. If you have more than one Plugwise Smile, select the gateway that is experiencing issues.
3. Select the device with 'Smile' in it's name.
4. On the integration entry, select the {% icon "mdi:dots-vertical" %}.
   - Then, select **Download diagnostics** and a JSON file will be downloaded.
5. You can inspect the downloaded file or, when requested, upload it to your issue report.

#### Adding a Smile reboot button

action: `button.press`

```yaml
# Example script change the thermostat schedule
script:
  reboot_gateway:
    sequence:
      - action: button.press
        target:
          entity_id: button.adam_reboot
```

## Supported devices

The Plugwise integration relies on the [plugwise](https://pypi.org/project/plugwise/) module for Python. It currently provides support for:

- Adam (a complete zone control system) also known as Adam HA.
  - On/Off, OpenTherm or Loria/Thermastage heating and cooling support.
  - Running firmwares v3.x or v2.3
  - Additional devices:
    - Zone thermostats such as Lisa or Anna (see warning below on Anna),
    - A temperature sensor, Jip,
    - Valve controllers called Floor or Tom,
    - An under-floor heating controler Koen (always comes with a Plug as the active part),
    - And smart switches, either Plug or Aquara Smart Plug,
- Anna (a smart thermostat).
  - OnOff, OpenTherm heating and Elga or Loria/Thermastage with heating and cooling support. (see note below on Elga)
  - Running firmware v4.x, v3.x or v1.x
- P1 (DSMR, smart meter) monitor.
  - Running firmware v4.x, v3.x or v2.x
- Stretch (for power switches).
  - Running firmware v3.x or v2.x

{% warning %}
Anna When Anna is used as a Zone Thermostat you should not configure it separately, as indicated in the [Configuration](#configuration)-section.
{% endwarning %}

{% note %}
For Elga devices:

- The cooling mode can only be toggled via a physical switch on the device (not through the Plugwise App)
- After changing the cooling mode switch position, you must reload the Plugwise integration for the changes to take effect

{% endnote %}

