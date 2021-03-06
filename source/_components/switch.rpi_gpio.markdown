---
layout: page
title: "Raspberry PI GPIO Switch"
description: "Instructions how to integrate the GPIO of a Raspberry PI into Home Assistant as a switch."
date: 2015-08-07 14:00
sidebar: true
comments: false
sharing: true
footer: true
logo: raspberry-pi.png
ha_category: Switch
ha_release: pre 0.7
ha_iot_class: "Local Push"
---


The `rpi_gpio` switch platform allows you to control the GPIOs of your [Raspberry Pi](https://www.raspberrypi.org/).

To use your Raspberry Pi's GPIO in your installation, add the following to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
switch:
  - platform: rpi_gpio
    ports:
      11: Fan Office
      12: Light Desk
```

Configuration variables:

- **ports** array (*Required*): Array of used ports.
  - **port: name** (*Required*): Port numbers and corresponding names (GPIO #).
- **invert_logic** (*Optional*): If true, inverts the output logic to ACTIVE LOW. Default is false (ACTIVE HIGH).
- **shared_gpio** (*Optional*): If true, forces a GPIO.setup() before each write. Default is false.

For more details about the GPIO layout, visit the Wikipedia [article](https://en.wikipedia.org/wiki/Raspberry_Pi#GPIO_connector) about the Raspberry Pi.

A common question is what does Port refer to, this number is the actual GPIO # not the pin #.
For example, if you have a relay connected to pin 11 its GPIO # is 17.

```yaml
# Example configuration.yaml entry
switch:
  - platform: rpi_gpio
    ports:
      17: Speaker Relay
```

In case you have any other python scripts running that use RPi.GPIO no values will be written after the initial HASS-start.
Setting **shared_gpio** to true will reinit the pin before each write, working around this issue.
```yaml
# Example configuration.yaml entry
switch:
  - platform: rpi_gpio
    shared_gpio: true
    ports:
      19: LED-Red
```

