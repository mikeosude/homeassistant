# Home Assistant Configuration

This repository contains my personal Home Assistant configuration, including dashboards, automations, scripts, integrations, and ESPHome device configurations.

It is shared as a reference for anyone building or improving their own Home Assistant setup.

## Important

This is a personal configuration. Before using any of it:

- Review every file and adapt it to your own devices.
- Replace personal entity IDs, names, network addresses, and paths.
- Create your own `secrets.yaml`.
- Never copy passwords, API keys, tokens, or encryption keys from a public repository.
- Check each integration’s current Home Assistant documentation before enabling it.

## Repository structure

- `configuration.yaml` — Main Home Assistant configuration
- `automations.yaml` — Automations
- `scripts.yaml` — Scripts
- `scenes.yaml` — Scenes
- `esphome/` — ESPHome device configurations
- `esp32/bluetooth-proxy/` — ESP32 Bluetooth proxy configuration

## Using this repository

The safest approach is to copy only the files or examples you need into your own Home Assistant configuration directory and customize them before restarting Home Assistant.

Home Assistant documentation:  
https://www.home-assistant.io/docs/

ESPHome documentation:  
https://esphome.io/

## Disclaimer

Use these files at your own risk. Hardware, integrations, entity names, and configuration options may differ between installations.
