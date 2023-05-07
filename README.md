# ld2420
esphome -ld2420 -newhardwave 115200
ESPHome Configuration
=====================

The following example configuration file can be used to connect up the GRGC1
Geiger Counter. The unit is preloaded with the captive portal enabled. It
will host an AP SSID of GRCG1 with no password allowing you to conviently
connect to your WiFi with a phone etc. Always use the api and ota passwords generated
by ESPHome's code. The sample value is for clarity only.

![GRPS1 - ESPHome](./grps1.web.jpg)

```
external_components:
  # pull geiger from Github @descipher branch in GitHub
  - source: github://GelidusResearch/grps1@current
    components: [ ld2420 ]
    refresh: 0s
esphome:
  name: presence-1
  friendly_name: presence-1
esp32:
  board: esp32dev
  framework:
    type: arduino
# Enable logging
logger:
# Enable Home Assistant API
api:
  encryption:
    key: "<your.api.key>"
ota:
  password: "<your.ota.password>"
wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password
  # Enable fallback hotspot (captive portal) in case wifi connection fails
 ap:
    ssid: GRPS1
    password: !secret captive_password
captive_portal:
web_server:
  port: 80
uart:
  id: ubus
  tx_pin: GPIO16
  rx_pin: GPIO17
  baud_rate: 115200
  parity: NONE
  stop_bits: 1
# The LD2420 has 16 sense gates 0-15 and each gate detects 0.6 meters 15th gate = 9m
ld2420:
  presence_time_window: 10s
  detection_gate_minimum : 1
  detection_gate_maximum: 9
  g0_move_threshold: 60000
  g0_still_threshold: 60000
  g1_move_threshold: 60000
  g1_still_threshold: 60000
  g2_move_threshold: 50000
  g2_still_threshold: 50000
  g3_move_threshold: 50000
  g3_still_threshold: 50000
  g4_move_threshold: 40000
  g4_still_threshold: 40000
  g5_move_threshold: 40000
  g5_still_threshold: 40000
  g6_move_threshold: 40000
  g6_still_threshold: 40000
  g7_move_threshold: 40000
  g7_still_threshold: 40000
  g8_move_threshold: 40000
  g8_still_threshold: 40000
  g9_move_threshold: 30000
  g9_still_threshold: 30000
  g10_move_threshold: 30000
  g10_still_threshold: 30000
  g11_move_threshold: 30000
  g11_still_threshold: 30000
  g12_move_threshold: 30000
  g12_still_threshold: 30000
  g13_move_threshold: 20000
  g13_still_threshold: 20000
  g14_move_threshold: 20000
  g14_still_threshold: 20000
  g15_move_threshold: 10000
  g15_still_threshold: 10000
sensor:
  - platform: ld2420
    moving_distance:
      name : Moving Distance
binary_sensor:
  - platform: ld2420
    has_target:
      name: Presence
switch:
  - platform: restart
    name: Restart    
