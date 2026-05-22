# Hydroponic Tower Automation Blueprint

This repository contains an importable Home Assistant automation blueprint for a hydroponic tower.

## What It Does

The blueprint automates irrigation with a day/night strategy:

- Night: exactly one watering at a fixed time.
- Day: repeated watering based on weather-derived sun intensity.
- Safety gap: enforces a minimum time between waterings.

All timing values are derived from a normal watering profile:

- Normal watering duration (seconds)
- Normal interval (minutes)
- Multipliers for low/high sun, night duration, and safety gap

## How Sun Intensity Is Estimated

The blueprint uses a Weather entity state to determine intensity levels:

- High intensity:
  - sunny
  - clear
  - clear-night
- Low intensity:
  - cloudy
  - fog
  - hail
  - lightning
  - lightning-rainy
  - pouring
  - rainy
  - snowy
  - snowy-rainy
  - windy
  - windy-variant
  - exceptional
- Medium intensity:
  - all other weather states (including partlycloudy)

Each intensity level maps to its own watering interval (minutes), configurable in the automation UI.

## File Location

Blueprint file:

- blueprints/automation/hydroponic/hydroponic_tower_solar_watering.yaml

## Import Into Home Assistant

Use one of these methods:

1. Manual file method (recommended for local repos)
- Copy the blueprint YAML into your Home Assistant config folder under:
  - blueprints/automation/hydroponic/
- In Home Assistant, go to:
  - Settings -> Automations & Scenes -> Blueprints
- Create an automation from this blueprint.

2. Import by URL
- Host the YAML file at a reachable raw URL.
- In Home Assistant Blueprints, choose Import Blueprint and paste the URL.

## Required Inputs

When creating the automation from the blueprint, set:

- Weather entity
- Last watering helper (input_datetime)
- Night watering time
- Normal watering duration (seconds)
- Normal interval (minutes)
- Low sun interval multiplier
- High sun interval multiplier
- Night duration multiplier
- Safety gap multiplier
- Start watering action (pump on / irrigation on)
- Stop watering action (pump off / irrigation off)

Create the helper first in Home Assistant:

- Settings -> Devices & Services -> Helpers -> Create Helper -> Date and/or Time
- Choose Date and time, then select this helper in the blueprint input.

## Suggested Starting Values

- Normal duration: 300 seconds (5 minutes)
- Normal interval: 120 minutes
- Low sun multiplier: 1.5 (result: 180 minutes)
- High sun multiplier: 0.4 (result: 48 minutes)
- Night duration multiplier: 0.5 (result: 150 seconds)
- Safety gap multiplier: 0.17 (result: ~20 minutes)
- Night watering time: 02:30

Adjust these values based on plant type, reservoir volume, climate, and tower size.

## Notes

- Some YAML linters in editors may show unresolved !input tag warnings for Home Assistant blueprints. This is expected in generic YAML tooling.
- The logic runs every 5 minutes during daytime checks and at the configured night time trigger.

## License

This project is licensed under the MIT License. See the LICENSE file for details.
