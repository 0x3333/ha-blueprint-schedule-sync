# Schedule Sync – Home Assistant Blueprint

An automation blueprint for [Home Assistant](https://www.home-assistant.io/) that keeps one or more devices in sync with the state of a **Schedule** entity.

- Schedule turns on → devices turn on (`turn_on`)
- Schedule turns off → devices turn off (`turn_off`)
- Optional **invert** mode (schedule ON = devices OFF)
- Optional **sync on startup**, restoring the correct device state after a Home Assistant restart

Works with any entity, device or area that supports `turn_on` / `turn_off`: lights, switches, fans, media players, `input_boolean`, and more.

## Installation

### Import via Home Assistant (recommended)

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2F0x3333%2Fha-blueprint-schedule-sync%2Fblob%2Fmain%2Fschedule_sync.yaml)

Or go to **Settings → Automations & Scenes → Blueprints → Import Blueprint** and paste the URL of `schedule_sync.yaml` from this repository.

### Manual

1. Copy `schedule_sync.yaml` to `config/blueprints/automation/schedule_sync/`.
2. Reload automations from **Developer Tools → YAML** (or restart Home Assistant).

## Usage

1. Create a Schedule under **Settings → Devices & Services → Helpers → Create Helper → Schedule**.
2. Create a new automation from the **Sync devices with Schedule** blueprint.
3. Fill in the inputs:

| Input | Description | Default |
|---|---|---|
| **Schedule** | The `schedule.*` entity that controls the devices | — |
| **Devices** | Entities, devices or areas to control | — |
| **Invert** | Schedule ON turns devices OFF, and vice versa | `false` |
| **Sync on startup** | Run the sync when Home Assistant starts | `true` |

## How it works

The automation triggers whenever the Schedule changes to `on` or `off` (ignoring `unknown` / `unavailable`) and, optionally, on the Home Assistant start event. The desired device state is computed as:

```
desired_on = (schedule == 'on') XOR invert
```

It then calls `homeassistant.turn_on` or `homeassistant.turn_off` on the selected target.

## Requirements

- Home Assistant **2024.10** or newer (uses the `triggers` / `actions` syntax).

## Disclaimer

This blueprint and its documentation were generated with the help of an AI assistant (Claude by Anthropic) and reviewed by the repository maintainer. Use at your own risk and test it in your own setup before relying on it. Issues and pull requests are welcome.

## License

MIT
