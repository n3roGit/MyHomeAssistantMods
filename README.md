# My Home Assistant Mods

A collection of Home Assistant automation blueprints and custom components.

## Available Blueprints

### 🌡️ Better Thermostat Control

**Better Thermostat – Raumheizungssteuerung (Lean)**

A minimal, room-based heating control for Better Thermostat. This blueprint deliberately omits window/outdoor/min-temp logic since Better Thermostat already covers these scenarios.

The climate entity is taken automatically from the selected Better Thermostat **device** (`device_entities` → first `climate.*`).

**Preset changes:** `climate.set_preset_mode` runs only when the computed target preset differs from the thermostat’s current `preset_mode`. That way a manual target temperature is not overwritten every poll cycle; it stays until another preset becomes active (then Better Thermostat applies that preset’s stored temperature).

**Triggers:** state changes on presence, motion, and night-mode entities, plus a **once-per-minute** time pattern (keeps state in sync without hammering the device).

**Features:**
- Priority-based preset system (boost → sleep → away → eco → activity → comfort → home)
- Motion detection integration
- Presence-based control
- Night mode support
- Master **enable** input to turn the automation on/off
- Optional boost, eco, and activity triggers
- Optional **temperature writeback**: when enabled, manual changes to the target temperature can be written to the matching Better Thermostat preset `number.*` entity for the current preset (only while `preset_mode` already matches the computed target)
- Optional **writeback bounds**: if enabled, writeback only happens when the manual temperature lies within fixed min/max ranges per preset (see table below); otherwise the thermostat keeps the manual value until the preset changes

#### Import (My Home Assistant)

The easiest way to add this blueprint is a **one-click import** via [My Home Assistant](https://my.home-assistant.io/): it opens your instance’s blueprint import dialog with the blueprint URL already filled in—you do not need to browse the GitHub folder structure or copy paths manually.

[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A//raw.githubusercontent.com/n3roGit/MyHomeAssistantMods/main/automation/BetterThermostatControl/BetterThermostat_RoomHeatControl_Lean.yaml)

- **Raw YAML** (for manual import or validation): `https://raw.githubusercontent.com/n3roGit/MyHomeAssistantMods/main/automation/BetterThermostatControl/BetterThermostat_RoomHeatControl_Lean.yaml`
- **Build your own redirect** (e.g. after forking or changing branches): [Create a link – My Home Assistant](https://my.home-assistant.io/create-link/?redirect=blueprint_import) — choose redirect **blueprint_import** and paste the raw GitHub URL of the `.yaml` file.

## 🔧 Requirements

- Home Assistant 2023.1 or later
- [Better Thermostat](https://github.com/KartoffelToby/better_thermostat) integration installed and configured
- Presence detection entities (person, device_tracker, or input_boolean)
- Motion sensors for room detection

## 📋 Usage

After importing the blueprint:

1. Create a new automation using the imported blueprint
2. Configure the required inputs:
   - **Climate Device**: Select your Better Thermostat device
   - **Presence Group**: Entity that indicates if someone is home (`on` / `home` / occupied-style states)
   - **Motion Group**: Binary sensor for room motion detection
   - **Night Mode**: Boolean entity for night mode activation
   - **Enable Switch**: Boolean entity to enable/disable the automation
3. Optional:
   - **Boost / Eco / Activity** triggers
   - **Temperature writeback**: sync manual `temperature` to the preset’s `number.<climate>_<preset>` entity
   - **Writeback bounds**: limit writeback to the ranges in the table below
4. Save and activate the automation

## 🎯 Preset Priority

The automation uses the following priority order:

1. **boost** - Highest priority, activated by boost trigger
2. **sleep** - When night mode is active
3. **away** - When no one is home
4. **eco** - When eco trigger is active (optional)
5. **activity** - When activity trigger is active (optional)
6. **comfort** - When motion is detected in the room
7. **home** - Default preset for normal presence

## Optional writeback temperature bounds (°C)

When **Writeback bounds** is enabled, manual temperatures outside these ranges are not written to the preset `number` entity (preset entity and manual setpoint can differ until the preset changes).

| Preset   | Min | Max |
|----------|-----|-----|
| away     | 16  | 19  |
| sleep    | 16  | 19  |
| eco      | 16  | 20  |
| home     | 19  | 23  |
| comfort  | 20  | 25  |
| activity | 20  | 25  |
| boost    | 22  | 26  |

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🔗 Links

- [Home Assistant](https://www.home-assistant.io/)
- [My Home Assistant](https://my.home-assistant.io/) — one-click deep links into your instance (e.g. blueprint import)
- [Better Thermostat](https://github.com/KartoffelToby/better_thermostat)
- [HACS](https://hacs.xyz/)

---

**Note**: This repository contains automation blueprints for Home Assistant. Make sure to review and test all automations before deploying them in your production environment.
