This is just a simple environment with:

* zigbee2mqtt: a bridge from zigbee (through a zigbee USB stick) to MQTT
* mosquitto: an MQTT server
* home assistant: a home automation platform, with MQTT support.
zigbee2mqtt also supports auto discovery for home assistant.


You'll need to configure zigbee2mqtt with a `z2m-data/configuration.yaml` file like this:

```
homeassistant: true
permit_join: true
mqtt:
  base_topic: zigbee2mqtt
    server: 'mqtt://mqtt' # The mosquitto server in this case.
    serial:
      port: /dev/ttyACM0  # The serial device. It should be the same as the device entry in docker-compose.yml.
```


After running home assistant the first time, you will have to add the mqtt configuration to the config file:

```
mqtt:
   broker: mqtt
   discovery: true
   birth_message:
     topic: 'hass/status'
     payload: 'online'
   will_message:
     topic: 'hass/status'
     payload: 'offline'
```

More info here: http://balkian.com/controlling-zigbee-devices-with-mqtt.html
