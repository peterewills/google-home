# g-home

A personal repository for writing, validating, and storing Google Home automation scripts in YAML format.

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
         4am          sunrise+1hr        sunset-1hr         10pm           4am
          |               |                  |                |             |
 ─────────┼───────────────┼──────────────────┼────────────────┼─────────────┼─────
          │   MORNING     │     DAYTIME      │    EVENING     │  NIGHTTIME  │
          │               │                  │                │             │
```

### Time-Based Environments

| Environment | Condition Window | Trigger Time |
|-------------|------------------|--------------|
| Morning | 3:59 am → sunrise+1hour | Voice only |
| Daytime | sunrise+59min → sunset-1hour | sunrise+1hour |
| Evening | sunset-61min → 10:00 pm | sunset-1hour |
| Nighttime | 9:59 pm → 4:00 am | 10:00 pm |

### Automatic Triggers

Each environment activates in three ways:

1. **Scheduled time**: Triggers at the start of its time window (except Morning)
2. **Arriving home**: Triggers when presence changes to HOME within the time window
3. **Voice command**: Manual activation via Google Assistant

### Leaving Home

When presence changes to AWAY (any time), the **Leaving** automation:
- Turns off all lights and space heater
- Sets thermostat to away temperature (62°F)

### Scripts

| Script | Description |
|--------|-------------|
| `morning.yaml` | Early morning lighting and climate |
| `daytime.yaml` | Daytime settings with work lighting |
| `evening.yaml` | Ambient evening lighting |
| `nighttime.yaml` | Dim night lighting, lower thermostat |
| `leaving.yaml` | Away mode when leaving home |

## Google Home Automation API Status (2025)

As of early 2025, Google offers Home APIs in public developer beta that include an Automation API. However, this API is **not suitable for managing YAML-based scripts**:

| Aspect | Web Script Editor | Home APIs |
|--------|-------------------|-----------|
| Format | YAML | Kotlin DSL |
| Platform | Web browser | Android app (iOS coming) |
| Target users | End users | App developers |
| Programmatic access | No | Yes |
| User limit | None | 100 during beta |

**Bottom line**: There is no API to programmatically upload or validate the YAML scripts used by the web editor. The Home APIs use a completely different format (Kotlin DSL) and are designed for developers building consumer apps, not for personal automation management.

### Resources

- [Home APIs Overview](https://developers.home.google.com/apis)
- [Automation API on Android](https://developers.home.google.com/apis/android/automation)
- [Web Script Editor](https://home.google.com/automations)
- [Script Editor Documentation](https://developers.home.google.com/automations/schema)
