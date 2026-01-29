# google-home

A personal repository for writing, validating, and storing Google Home automation
scripts in YAML format.

Note that some functionality is limited since I am operating on the iOS app and not on
Android.

**Script Editor**: https://home.google.com/automations

## Purpose

Google Home allows creating automations via a web-based script editor at https://home.google.com/automations. This project provides:

- **Reference documentation** for the YAML automation syntax
- **Device inventory** tracking my actual device names
- **Script storage** for version-controlled automation scripts

## Usage

1. Write automation scripts using the YAML format documented in `docs/automation-reference.md`
2. Verify device names match exactly as listed in `docs/device-list.md`
3. Copy the script into the [Google Home web editor](https://home.google.com/automations)
4. Use the Validate button to check for errors
5. Save the automation

### Updating Scripts

To update an existing automation:

1. Open the [automations UI](https://home.google.com/automations)
2. Select the script to edit (or create a new one)
3. **Delete the entire existing contents** of the script
4. Paste in the new YAML
5. Check for validation errors—these must be resolved before saving
6. Review any warnings—these are common and generally acceptable to ignore
7. Save the automation
8. Refresh the Google Home iOS app
9. Test the automation from the iOS app

## Project Structure

```
g-home/
├── docs/
│   ├── automation-reference.md    # Syntax reference (starters, conditions, actions)
│   ├── device-list.md             # My device names by room
│   ├── google-home-automation-urls.md  # Official documentation URLs
│   ├── google-home-agent.md       # Claude agent instructions
│   └── script-template.yaml       # Blank template
├── scripts/                       # Saved automation scripts
├── CLAUDE.md                      # Project instructions for Claude
└── README.md
```

## Automation Strategy

The home is configured with four time-based environments that automatically transition throughout the day:

```
                     sunrise         sunset-1hr           8pm
                         |                  |                |
 ────────────────────────┼──────────────────┼────────────────┼────────────────────
       LATE-NIGHT        │     DAYTIME      │    EVENING     │    LATE-NIGHT
    (8pm → sunrise)      │                  │                │   (8pm → sunrise)
```

### Time-Based Environments

| Environment | Condition Window | Trigger |
|-------------|------------------|---------|
| Late-night | 8:00 pm → sunrise | Arriving home, voice |
| Daytime | sunrise → sunset-1hour | sunrise+1hour, arriving home, voice |
| Evening | sunset-1hour → 8:00 pm | sunset-1hour, arriving home, voice |
| Sleeping | (none) | Voice only |

### Automatic Triggers

Each environment activates via:

1. **Scheduled time**: Daytime and Evening trigger at the start of their time windows
2. **Arriving home**: Late-night, Daytime, and Evening trigger when presence changes to HOME within their time window
3. **Voice command**: All environments can be manually activated via Google Assistant

### Leaving Home

When presence changes to AWAY (any time), the **Leaving** automation:
- Turns off all lights
- Sets thermostat to away temperature (62°F)

### Scripts

| Script | Description |
|--------|-------------|
| `late-night.yaml` | Late night lighting and climate (8pm-sunrise) |
| `daytime.yaml` | Daytime settings with work lighting |
| `evening.yaml` | Ambient evening lighting |
| `sleeping.yaml` | Dim sleeping lighting, lower thermostat (voice only) |
| `leaving.yaml` | Away mode when leaving home |

### Device States by Environment

| Device | Late-night | Daytime | Evening | Sleeping |
|--------|------------|---------|---------|----------|
| **Living Room** |
| Gallery Lights | off | on | on | off |
| Relax Sign | off | on | on | off |
| Dining Table Light | 25% | 100% | 25% | off |
| Living Room Paper Lamp | on | on | on | off |
| Johns Hopkins Lamp | on | off | on | on |
| **Bedroom** |
| Bedroom Paper Lamp | off | off | on | off |
| **Front Room** |
| Front Room (thermostat) | 66°F | 70°F | 70°F | 62°F |
| Zendo Lamp | on | off | on | off |
| Reading Lamp | off | 100% | 100% | off |
| **Front door** |
| Front Porch Lights | on | off | on | off |
| **Kitchen** |
| Kitchen Lamp | 25% | off | 25% | 5% |

## Google Home Automation API Status (2025)

As of early 2025, Google offers Home APIs in public developer beta that include an
Automation API. However, this API is **not suitable for managing YAML-based scripts**.
**Bottom line**: There is no API to programmatically upload or validate the YAML scripts
used by the web editor. The Home APIs use a completely different format (Kotlin DSL) and
are designed for developers building consumer apps, not for personal automation
management.

### Resources

- [Home APIs Overview](https://developers.home.google.com/apis)
- [Automation API on Android](https://developers.home.google.com/apis/android/automation)
- [Web Script Editor](https://home.google.com/automations)
- [Script Editor Documentation](https://developers.home.google.com/automations/schema)
