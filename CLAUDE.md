# ESPHome Config

Personal ESPHome configuration repository using a package-based composition pattern.

## Structure

```
esphome-config/
├── <device-name>.yaml          # Top-level device configs (substitutions + board package include)
├── esphome-common/             # Shared components included by all devices
│   ├── base.yaml               # Pulls in api, diagnostics, esphome, time
│   ├── api.yaml
│   ├── diagnostics.yaml
│   ├── esphome.yaml
│   ├── time.yaml
│   └── wifi.yaml
├── m5stack-atom-lite/          # Board package: M5Stack Atom Lite (ESP32)
├── sonoff-nspanel/             # Board package: Sonoff NSPanel
├── open-air-mini/              # Board package: Open Air Mini
├── tuya-rsh-wifi-sky01/        # Board package: Tuya RSH WiFi Sky01
├── tuya-smart-valve/           # Board package: Tuya Smart Valve
└── waterp1meterkit-v3/         # Board package: WaterP1MeterKit v3
```

## Composition Pattern

Device configs declare substitutions and include a board package:

```yaml
substitutions:
  system_name: my-device
  host_name: my-device.home.econline.nl
  device_description: "Description"
  friendly_name: "Friendly Name"

packages:
  device: !include m5stack-atom-lite/base.yaml
```

Board packages set the ESP platform/board and pull in `esphome-common/` shared components plus board-specific entities:

```yaml
esp32:
  board: m5stack-atom
  framework:
    type: arduino

packages:
  common: !include ../esphome-common/base.yaml
  wifi: !include ../esphome-common/wifi.yaml
  entities: !include entities.yaml
```

## Active Devices

- `bedroom-job-rocket-atom-lite.yaml` — WS2812 wake-up alarm light (M5Stack Atom Lite)
- `bedroom-job-nebula.yaml` — Nebula light, bedroom Job
- `bedroom-eva-nebula.yaml` — Nebula light, bedroom Eva
- `kitchen-nspanel.yaml` — NSPanel touch display (Sonoff NSPanel)
- `attic-laundry-room-open-air-mini.yaml` — Open Air Mini, attic/laundry room
- `downstairs-hallway-sprinklers.yaml` — Sprinkler controller
- `downstairs-hallway-waterp1meter.yaml` — Dutch P1 smart meter reader
- `upstairs-office-speaker.yaml` — Office speaker

All devices integrate with Home Assistant via the ESPHome API at `*.home.econline.nl`.
