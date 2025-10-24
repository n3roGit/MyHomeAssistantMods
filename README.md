# My Home Assistant Mods

A collection of Home Assistant automation blueprints and custom components.

## 🏠 Available Blueprints

### Better Thermostat Control

**Better Thermostat – Raumheizungssteuerung (Lean)**

A minimal, room-based heating control for Better Thermostat. This blueprint deliberately omits window/outdoor/min-temp logic since Better Thermostat already covers these scenarios.

**Features:**
- Priority-based preset system (boost → sleep → away → eco → activity → comfort → home)
- Motion detection integration
- Presence-based control
- Night mode support
- Optional boost, eco, and activity triggers

## 📥 Installation

### Method 1: Direct Import (Recommended)

1. Go to **Settings** → **Automations & Scenes** → **Blueprints**
2. Click **Import Blueprint**
3. Copy and paste this URL:
   ```
   https://raw.githubusercontent.com/n3roGit/MyHomeAssistantMods/main/automation/BetterThermostatControl/BetterThermostat_RoomHeatControl_Lean.yaml
   ```
4. Click **Import**

### Method 2: HACS (Community Store)

1. Install [HACS](https://hacs.xyz/) if not already installed
2. Go to **HACS** → **Frontend** → **Explore & Download Repositories**
3. Search for "My Home Assistant Mods" or add this repository manually
4. Install and restart Home Assistant

### Method 3: Manual Download

1. Download the blueprint file from this repository
2. Go to **Settings** → **Automations & Scenes** → **Blueprints**
3. Click **Import Blueprint**
4. Upload the downloaded file

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
   - **Presence Group**: Entity that indicates if someone is home
   - **Motion Group**: Binary sensor for room motion detection
   - **Night Mode**: Boolean entity for night mode activation
   - **Enable Switch**: Boolean entity to enable/disable the automation
3. Optionally configure boost, eco, and activity triggers
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

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🔗 Links

- [Home Assistant](https://www.home-assistant.io/)
- [Better Thermostat](https://github.com/KartoffelToby/better_thermostat)
- [HACS](https://hacs.xyz/)

---

**Note**: This repository contains automation blueprints for Home Assistant. Make sure to review and test all automations before deploying them in your production environment.
