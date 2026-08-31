# ESP32 Bluetooth Proxy

This project turns a standard ESP32 development board into a Bluetooth Low Energy (BLE) proxy for Home Assistant.

The ESP32 is placed closer to Bluetooth devices around the house and communicates with Home Assistant over Wi-Fi. This bridges the distance between the Home Assistant server and devices that are too far away for the server’s local Bluetooth adapter to reach reliably.

```text
Bluetooth device
       │
       │ BLE
       ▼
ESP32 Bluetooth Proxy
       │
       │ Wi-Fi / ESPHome API
       ▼
Home Assistant
```

## What it does

The proxy can forward:

- BLE advertisements from nearby sensors and beacons
- Bluetooth device discovery data
- Supported active Bluetooth connections
- GATT reads and writes for compatible Home Assistant integrations

Home Assistant remains responsible for interpreting and managing the Bluetooth devices. The ESP32 acts as the remote Bluetooth bridge.

A Bluetooth proxy supports Bluetooth Low Energy devices. It does not provide a general-purpose bridge for every classic Bluetooth device.

## Hardware

This configuration is intended for a standard ESP32 board, such as an ESP32-DevKitC-32 or compatible ESP32-WROOM-32 development board.

The board needs:

- ESP32 Bluetooth support
- Wi-Fi connectivity
- A USB data cable for the initial flash
- Reliable 2.4 GHz Wi-Fi coverage
- USB power at its installation location

ESP32-C3, ESP32-S3, and other ESP32 variants may require a different board configuration.

## ESPHome configuration

Create a separate configuration for each proxy and give every board a unique name:

```yaml
esphome:
  name: bluetooth-proxy-living-room
  friendly_name: Bluetooth Proxy Living Room
  name_add_mac_suffix: false

esp32:
  board: esp32dev
  framework:
    type: esp-idf

wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password

logger:

api:

mqtt:
  broker: !secret mqtt_broker
  port: 1883
  username: !secret mqtt_username
  password: !secret mqtt_password

esp32_ble_tracker:

bluetooth_proxy:
  active: true
```

Example `secrets.yaml`:

```yaml
wifi_ssid: "YOUR_WIFI_NETWORK"
wifi_password: "YOUR_WIFI_PASSWORD"

mqtt_broker: "YOUR_MQTT_BROKER_ADDRESS"
mqtt_username: "YOUR_MQTT_USERNAME"
mqtt_password: "YOUR_MQTT_PASSWORD"
```

Do not commit `secrets.yaml` or any file containing real credentials.

## Flashing

1. Install or open the ESPHome add-on in Home Assistant.
2. Create a new ESPHome device.
3. Use the configuration above.
4. Connect the ESP32 with a USB data cable.
5. Flash the device over USB.
6. Add or adopt the device in ESPHome if prompted.
7. Confirm that it appears under **Settings → Devices & services** in Home Assistant.
8. Place it near the Bluetooth devices it should serve.

The first flash normally requires USB. Later updates can generally be performed over the network using ESPHome OTA.

## Placement

For better coverage:

- Place the proxy near the Bluetooth devices.
- Keep it in an open area.
- Avoid metal enclosures.
- Keep it away from routers, switches, computers, and other sources of radio interference.
- Use multiple proxies when one device cannot cover the whole house.

## Connection limits

Active Bluetooth connections use a limited number of connection slots. Passive BLE advertisements are handled separately and are not limited in the same way.

Not every Bluetooth device is supported by Home Assistant. The required Home Assistant integration must support the specific device and its Bluetooth protocol.

## References

- [ESPHome Bluetooth Proxy](https://esphome.io/components/bluetooth_proxy/)
- [ESPHome MQTT Client](https://esphome.io/components/mqtt/)
- [Home Assistant Bluetooth integration](https://www.home-assistant.io/integrations/bluetooth/)
- [ESPHome Bluetooth Proxy installer](https://esphome.io/projects/?type=bluetooth)

## Disclaimer

This configuration is provided as a starting point. Review and customize it for your own network, hardware, Home Assistant installation, and Bluetooth devices.