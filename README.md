# Hydroponic Tower Automation Blueprint

This repository contains an importable Home Assistant automation blueprint for a hydroponic tower.

## What It Does

The blueprint automates irrigation with a day/night strategy:

- Night: exactly one watering at a fixed time.
- Day: repeated watering based on weather-derived sun intensity.
- Safety gap: enforces a minimum time between waterings.

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
- Night watering time
- Day watering duration (seconds)
- Night watering duration (seconds)
- Interval at low sun (minutes)
- Interval at medium sun (minutes)
- Interval at high sun (minutes)
- Safety gap between waterings (minutes)
- Start watering action (pump on / irrigation on)
- Stop watering action (pump off / irrigation off)

## Suggested Starting Values

- Day duration: 45 seconds
- Night duration: 30 seconds
- Low sun interval: 180 minutes
- Medium sun interval: 90 minutes
- High sun interval: 45 minutes
- Safety gap: 20 minutes
- Night watering time: 02:30

Adjust these values based on plant type, reservoir volume, climate, and tower size.

## Notes

- Some YAML linters in editors may show unresolved !input tag warnings for Home Assistant blueprints. This is expected in generic YAML tooling.
- The logic runs every 5 minutes during daytime checks and at the configured night time trigger.

## License

Add your preferred license information here.
