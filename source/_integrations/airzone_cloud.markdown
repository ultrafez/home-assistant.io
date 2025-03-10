---
title: Airzone Cloud
description: Instructions on how to integrate Airzone Cloud within Home Assistant.
ha_release: 2023.6
ha_category:
  - Sensor
ha_iot_class: Cloud Polling
ha_config_flow: true
ha_domain: airzone_cloud
ha_platforms:
  - diagnostics
  - sensor
ha_codeowners:
  - '@Noltari'
ha_integration_type: integration
---

This integration interacts with the Cloud API of [Airzone devices](https://www.airzone.es/en/).

There are two main types of Airzone devices:
- [Aidoo](https://www.airzonecontrol.com/aa/en/control-solutions/aidoo/wi-fi/) / [Aidoo Pro](https://www.airzonecontrol.com/aa/en/control-solutions/aidoo/pro/)
- [Easyzone (US)](https://www.airzonecontrol.com/aa/en/control-solutions/easyzone/) / [Flexa (EU)](https://www.airzonecontrol.com/ib/es/soluciones-de-control/flexa/)

## Aidoo / Aidoo Pro

These devices are Wi-Fi controllers that are normally connected to a single air conditioner split system.

## Easyzone (US) / Flexa (EU)

These devices are connected to ducted air conditioners, motorized grilles, and individual thermostats for every room (zone). Therefore, with a single ducted air conditioning system, the user can turn on and off the air conditioner and set different desired temperatures in each room.

A typical Airzone HVAC system consists of a parent device (called *master zone* in Airzone terminology) and child devices (called *slave zones* in Airzone terminology). The [HVAC mode](https://www.home-assistant.io/integrations/climate/#service-climateset_hvac_mode) can only be changed on the parent device. On child devices, you can only enable or disable the HVAC and adjust the desired temperature for that specific device.

Note that multiple HVAC systems can be connected to the same Airzone web server. In this case, there will be one *parent zone* per HVAC system and there may also be *child zones* for each HVAC system.

{% include integrations/config_flow.md %}

{% configuration_basic %}
Username:
  description: "Cloud API username"
Password:
  description: "Cloud API password"
{% endconfiguration_basic %}

## Sensors

For each Airzone Aidoo (HVAC Wi-Fi controller), the following *sensors* are created:

| Condition           | Description                                        |
| :------------------ | :------------------------------------------------- |
| temperature         | Measures the temperature from the HVAC thermostat. |

For each Airzone zone (thermostat), the following *sensors* are created:

| Condition           | Description                                         |
| :------------------ | :-------------------------------------------------- |
| humidity            | Measures the relative humidity in the current zone. |
| temperature         | Measures the temperature in the current zone.       |

For each Airzone WebServer (HVAC Wi-Fi controller), the following *sensors* are created:

| Condition           | Description                                        |
| :------------------ | :------------------------------------------------- |
| rssi                | Wi-Fi RSSI.                                        |
