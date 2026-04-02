# TomTuT Dishwasher Card

A Home Assistant Lovelace custom card for AEG/Electrolux dishwashers with status-dependent images and animated overlays.

Designed to work with the [TomTuT Electrolux/AEG Dishwasher](https://github.com/TomTuT1242/tomtut-electrolux-dishwasher) integration.

## Features

- Three status images: closed, running (with animated blue glow), finished
- Status badge with color coding (green=running, orange=paused, blue=done, gray=idle, red=alarm)
- Program display (ECO, AUTO, Quick, etc.)
- Timer with estimated finish time
- Cycle phase in control bar (Prewash, Main Wash, Drying, etc.)
- Warning badges for salt and rinse aid
- Optional power consumption display (e.g. via Shelly Plug)
- Context-dependent control buttons (Start, Pause, Resume, Stop)
- Dark theme, responsive
- All labels in German

## Installation

### HACS (Recommended)

1. Open HACS in Home Assistant
2. Go to Frontend
3. Click the three dots menu > Custom repositories
4. Add `https://github.com/TomTuT1242/tomtut-dishwasher-card` as **Dashboard**
5. Install "TomTuT Dishwasher Card"
6. Copy the `images/` folder to your `config/www/tomtut-dishwasher/` directory
7. Restart Home Assistant

### Manual

1. Copy `tomtut-dishwasher-card.js` to `config/www/`
2. Copy `images/*.png` to `config/www/tomtut-dishwasher/`
3. Add `/local/tomtut-dishwasher-card.js` as a Lovelace resource (JavaScript Module)

## Configuration

```yaml
type: custom:tomtut-dishwasher-card
# Required: sensors from the Electrolux Dishwasher integration
entity_state: sensor.geschirrspulmaschine_status
entity_phase: sensor.geschirrspulmaschine_phase
entity_program: sensor.geschirrspulmaschine_programm
entity_time: sensor.geschirrspulmaschine_restzeit
entity_door: binary_sensor.geschirrspulmaschine_tur
entity_running: binary_sensor.geschirrspulmaschine_lauft
entity_salt: binary_sensor.geschirrspulmaschine_salz_fehlt
entity_rinse_aid: binary_sensor.geschirrspulmaschine_klarspuler_niedrig

# Optional: power consumption sensor (e.g. Shelly Plug)
entity_power: sensor.shelly_plug_dishwasher_power

# Optional: button entities for controls
button_on: button.geschirrspulmaschine_einschalten
button_off: button.geschirrspulmaschine_ausschalten
button_start: button.geschirrspulmaschine_start
button_pause: button.geschirrspulmaschine_pause
button_resume: button.geschirrspulmaschine_fortsetzen
button_stopreset: button.geschirrspulmaschine_stop_reset
```

## Status Images

The card switches between three images based on the dishwasher state:

| State | Image |
|-------|-------|
| OFF, IDLE, READY_TO_START, DELAYED_START | `closed.png` |
| RUNNING, PAUSED | `running.png` (with animated blue glow) |
| END_OF_CYCLE | `done.png` |

Images are served from `/local/tomtut-dishwasher/`. You can replace them with your own photos.

## Control Bar

The control bar below the image shows context-dependent elements:

- **Left:** Cycle phase + warning badges (salt, rinse aid) + power consumption
- **Right:** Action buttons that change based on state:
  - OFF → "Ein"
  - READY_TO_START → "Start" + "Aus"
  - RUNNING → "Pause" + "Stop"
  - PAUSED → "Weiter" + "Stop"
  - END_OF_CYCLE → "Reset"

## License

MIT License - see [LICENSE](LICENSE)
