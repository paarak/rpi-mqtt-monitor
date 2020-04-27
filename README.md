# Rapsberry Pi MQTT monitor
Python script to check cpu load, cpu temperature, free space, voltage and system clock speed
on a Raspberry Pi computer and publish the data to a MQTT server.

I wrote this so I can monitor my raspberries at home with [home assistant](https://www.home-assistant.io/). The script was written and tested on Python 2 but it should work fine on Python 3.
The script if very light, it takes 4 seconds as there are 4 one second sleeps in the code - due to mqtt have problems if I shoot the messages with no delay.

# Installation:

If you don't have pip installed:

$ sudo apt install python-pip

Then install this module needed for the script:

$ pip install paho-mqtt

Rename config.py.example to config.py and populate the needed variables

Test the script.

$ /usr/bin/python /home/pi/scripts/rpi-cpu2mqtt.py

Create a cron entry like this (you might need to update the path on the cron entry below, depending on where you put the script):

*/2 * * * * /usr/bin/python /home/pi/scripts/rpi-cpu2mqtt.py

# Home Assistant Integration

![Rapsberry Pi MQTT monitor in Home Assistant](images/rpi-cpu2mqtt-hass.jpg)

Once you installed the script on your raspberry you need to create some sensors in home assistant.

This is the sensors configuration assuming your sensors are separated in sensors.yaml file.
```yaml
  - platform: mqtt
    state_topic: "masoko/rpi4/cpuload"
    name: rpi 4 cpu load
    unit_of_measurement: "%"

  - platform: mqtt
    state_topic: "masoko/rpi4/cputemp"
    name: rpi 4 cpu temp
    unit_of_measurement: "°C"

  - platform: mqtt
    state_topic: "masoko/rpi4/diskusage"
    name: rpi 4 diskusage
    unit_of_measurement: "%"

  - platform: mqtt
    state_topic: "masoko/rpi4/voltage"
    name: rpi 4 voltage
    unit_of_measurement: "V"

  - platform: mqtt
    state_topic: "masoko/rpi4/sys_clock_speed"
    name: rpi 4 sys clock speed
    unit_of_measurement: "hz"
```