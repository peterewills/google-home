# Google Home Automation Script Reference

## Overview

Google Home automations are written in YAML and consist of two main sections:
1. **metadata** - Name and description
2. **automations** - One or more automation rules

Each automation rule has:
- **starters** (required) - Events that trigger the automation
- **condition** (optional) - Constraints that must be true for actions to run
- **actions** (required) - Operations to perform

```yaml
metadata:
  name: My Automation
  description: What this automation does

automations:
  - starters:
      - type: <starter_type>
        # starter parameters
    condition:  # optional
      type: <condition_type>
      # condition parameters
    actions:
      - type: <action_type>
        # action parameters
```

## YAML Basics

- **Key-value pairs**: `key: value`
- **Indentation**: Use consistent spaces (not tabs) to denote hierarchy
- **Arrays**: Items prefixed with `-`
- **Comments**: Text after `#` is ignored
- **Strings with special characters**: Quote strings starting with `[`, `{`, `"`, `'`, `#`, or containing `: `

## Device References

Devices are referenced by name using the format: `Device Name - Room Name`

```yaml
devices: Desk Lamp - Office
# or for multiple devices:
devices:
  - Desk Lamp - Office
  - Floor Lamp - Living Room
```

## Data Types

| Type | Format | Examples |
|------|--------|----------|
| Time | `HH:MM am/pm` or `HH:MM` | `6:00 pm`, `18:00`, `SUNRISE`, `SUNSET` |
| Duration | `<number><unit>` | `5sec`, `10min`, `1hour` |
| Temperature | `<number><unit>` | `72F`, `22C` |
| Weekday | String | `MON`, `TUE`, `WED`, `THU`, `FRI`, `SAT`, `SUN` |
| Boolean | `true` or `false` | |
| Number | Integer or decimal | `50`, `72.5` |

---

## Starters

### Time Schedule
Trigger at a specific time.

```yaml
starters:
  - type: time.schedule
    at: 6:00 pm
```

With specific weekdays:
```yaml
starters:
  - type: time.schedule
    at: 7:00 am
    weekdays:
      - MON
      - TUE
      - WED
      - THU
      - FRI
```

Using sunrise/sunset:
```yaml
starters:
  - type: time.schedule
    at: SUNSET
```

### Device State Change
Trigger when a device state changes.

```yaml
starters:
  - type: device.state.OnOff
    device: Smart Switch - Living Room
    state: on
    is: true
```

### Home Presence
Trigger when home occupancy changes.

```yaml
starters:
  - type: home.state.HomePresence
    state: homePresenceMode
    is: HOME  # or AWAY
```

### Voice Command
Trigger with a custom voice command.

```yaml
starters:
  - type: assistant.event.OkGoogle
    eventData: query
    is: Movie time
```
(User says "Hey Google, Movie time")

### Device Events
Trigger on specific device events.

```yaml
# Doorbell press
starters:
  - type: device.event.DoorbellPress
    device: Front Door Doorbell - Front Door

# Motion detection
starters:
  - type: device.event.MotionDetection
    device: Camera - Hallway
```

### Suppressing Repeated Triggers
Prevent an automation from firing repeatedly:

```yaml
starters:
  - type: device.event.MotionDetection
    device: Camera - Hallway
    suppressFor: 20min
```

### Duration Requirement
Require a state to persist before triggering:

```yaml
starters:
  - type: device.state.MotionDetection
    device: Sensor - Living Room
    state: motionDetectionEventInProgress
    is: false
    for: 5min  # only trigger after 5 min of no motion
```

---

## Conditions

### Time Between
Only run during certain hours.

```yaml
condition:
  type: time.between
  after: 6:00 pm
  before: 11:00 pm
```

Using sunrise/sunset:
```yaml
condition:
  type: time.between
  after: SUNSET
  before: SUNRISE
```

With weekdays:
```yaml
condition:
  type: time.between
  after: 9:00 am
  before: 5:00 pm
  weekdays:
    - MON
    - TUE
    - WED
    - THU
    - FRI
```

### Device State
Only run if a device is in a certain state.

```yaml
condition:
  type: device.state.OnOff
  device: TV - Living Room
  state: on
  is: true
```

### Logical Operators

**AND** - All conditions must be true:
```yaml
condition:
  type: and
  conditions:
    - type: device.state.OnOff
      device: TV - Living Room
      state: on
      is: true
    - type: time.between
      after: 6:00 pm
```

**OR** - Any condition can be true:
```yaml
condition:
  type: or
  conditions:
    - type: home.state.HomePresence
      state: homePresenceMode
      is: HOME
    - type: device.state.OnOff
      device: Guest Mode Switch - Office
      state: on
      is: true
```

**NOT** - Invert a condition:
```yaml
condition:
  type: not
  condition:
    type: time.between
    after: 11:00 pm
    before: 6:00 am
```

---

## Actions

### On/Off Control
Turn devices on or off.

```yaml
actions:
  - type: device.command.OnOff
    devices: Desk Lamp - Office
    on: true  # or false
```

Multiple devices:
```yaml
actions:
  - type: device.command.OnOff
    devices:
      - Desk Lamp - Office
      - Floor Lamp - Living Room
    on: true
```

### Brightness
Set absolute brightness (0-100).

```yaml
actions:
  - type: device.command.BrightnessAbsolute
    devices: Desk Lamp - Office
    brightness: 50
```

Note: Setting brightness > 0 turns on an off device. Setting to 0 turns it off.

### Color
Set light color by name:
```yaml
actions:
  - type: device.command.ColorAbsolute
    devices: Smart Bulb - Bedroom
    color:
      name: blue
```

By color temperature (Kelvin):
```yaml
actions:
  - type: device.command.ColorAbsolute
    devices: Smart Bulb - Bedroom
    color:
      temperature: 3000
```

### Thermostat
Set target temperature:
```yaml
actions:
  - type: device.command.ThermostatTemperatureSetpoint
    devices: Thermostat - Hallway
    thermostatTemperatureSetpoint: 72F
```

Set temperature range (for heat-cool mode):
```yaml
actions:
  - type: device.command.ThermostatTemperatureSetRange
    devices: Thermostat - Hallway
    thermostatTemperatureSetpointHigh: 76F
    thermostatTemperatureSetpointLow: 68F
```

Set thermostat mode:
```yaml
actions:
  - type: device.command.ThermostatSetMode
    devices: Thermostat - Hallway
    thermostatMode: cool  # heat, cool, off, heatcool, auto, etc.
```

### Lock/Unlock
```yaml
actions:
  - type: device.command.LockUnlock
    devices: Front Door Lock - Entry
    lock: true  # or false to unlock
```

### Open/Close (Blinds, Garage, etc.)
```yaml
actions:
  - type: device.command.OpenClose
    devices: Blinds - Living Room
    openPercent: 100  # 0 = closed, 100 = fully open
```

### Start/Stop (Vacuum, Washer, etc.)
```yaml
actions:
  - type: device.command.StartStop
    devices: Robot Vacuum - Living Room
    start: true  # or false to stop
```

### Volume
```yaml
actions:
  - type: device.command.SetVolume
    devices: Speaker - Living Room
    volumeLevel: 30
```

### Fan Speed
```yaml
actions:
  - type: device.command.SetFanSpeed
    devices: Ceiling Fan - Bedroom
    fanSpeed: speed_high  # values depend on device
```

### Delay Between Actions
```yaml
actions:
  - type: device.command.OnOff
    devices: Light - Bedroom
    on: true
  - type: time.delay
    for: 5min
  - type: device.command.OnOff
    devices: Light - Bedroom
    on: false
```

### Broadcast Message
```yaml
actions:
  - type: assistant.command.Broadcast
    message: Dinner is ready
```

To specific speakers:
```yaml
actions:
  - type: assistant.command.Broadcast
    devices:
      - Nest Hub - Kitchen
      - Nest Mini - Living Room
    message: Dinner is ready
```

### Send Notification
```yaml
actions:
  - type: home.command.Notification
    title: Motion Detected
    body: Motion was detected at the front door
    members:
      - user@gmail.com
```

Omit `members` to notify everyone in the home.

### Light Effects
Gradual wake-up:
```yaml
actions:
  - type: device.command.LightEffectWake
    devices: Bedroom Light - Bedroom
    duration: 10min
```

Gradual sleep:
```yaml
actions:
  - type: device.command.LightEffectSleep
    devices: Bedroom Light - Bedroom
    duration: 10min
```

Pulse effect:
```yaml
actions:
  - type: device.command.LightEffectPulse
    devices: Light - Living Room
    duration: 5min
```

---

## Complete Examples

### 1. Morning Routine
Turn on lights at sunrise on weekdays.

```yaml
metadata:
  name: Weekday Morning Lights
  description: Turn on lights at sunrise on weekdays

automations:
  - starters:
      - type: time.schedule
        at: SUNRISE
        weekdays:
          - MON
          - TUE
          - WED
          - THU
          - FRI
    actions:
      - type: device.command.BrightnessAbsolute
        devices:
          - Bedroom Light - Bedroom
          - Bathroom Light - Bathroom
        brightness: 80
```

### 2. Evening Lights
Dim lights at sunset, turn off at bedtime.

```yaml
metadata:
  name: Evening Lighting
  description: Manage evening lights

automations:
  - starters:
      - type: time.schedule
        at: SUNSET
    actions:
      - type: device.command.BrightnessAbsolute
        devices: Living Room Light - Living Room
        brightness: 70

  - starters:
      - type: time.schedule
        at: 10:30 pm
    actions:
      - type: device.command.BrightnessAbsolute
        devices: Living Room Light - Living Room
        brightness: 30

  - starters:
      - type: time.schedule
        at: 11:00 pm
    actions:
      - type: device.command.OnOff
        devices: Living Room Light - Living Room
        on: false
```

### 3. Smart Plug Control
Turn on coffee maker in the morning, off after 2 hours.

```yaml
metadata:
  name: Morning Coffee
  description: Turn on coffee maker and auto-off after 2 hours

automations:
  - starters:
      - type: time.schedule
        at: 6:30 am
        weekdays:
          - MON
          - TUE
          - WED
          - THU
          - FRI
    actions:
      - type: device.command.OnOff
        devices: Coffee Maker Plug - Kitchen
        on: true
      - type: time.delay
        for: 2hour
      - type: device.command.OnOff
        devices: Coffee Maker Plug - Kitchen
        on: false
```

### 4. Thermostat Schedule
Adjust temperature based on time of day.

```yaml
metadata:
  name: Thermostat Schedule
  description: Adjust temperature throughout the day

automations:
  # Morning - warm up
  - starters:
      - type: time.schedule
        at: 6:00 am
    actions:
      - type: device.command.ThermostatTemperatureSetpoint
        devices: Nest Thermostat - Hallway
        thermostatTemperatureSetpoint: 72F

  # Away during work
  - starters:
      - type: time.schedule
        at: 8:30 am
        weekdays:
          - MON
          - TUE
          - WED
          - THU
          - FRI
    actions:
      - type: device.command.ThermostatTemperatureSetpoint
        devices: Nest Thermostat - Hallway
        thermostatTemperatureSetpoint: 65F

  # Evening - comfortable
  - starters:
      - type: time.schedule
        at: 5:30 pm
    actions:
      - type: device.command.ThermostatTemperatureSetpoint
        devices: Nest Thermostat - Hallway
        thermostatTemperatureSetpoint: 71F

  # Night - cooler for sleeping
  - starters:
      - type: time.schedule
        at: 10:00 pm
    actions:
      - type: device.command.ThermostatTemperatureSetpoint
        devices: Nest Thermostat - Hallway
        thermostatTemperatureSetpoint: 68F
```

### 5. Motion-Activated Lights
Turn on lights when motion detected, off after 5 minutes of no motion.

```yaml
metadata:
  name: Motion Lights
  description: Motion-activated lighting

automations:
  - starters:
      - type: device.state.MotionDetection
        device: Motion Sensor - Hallway
        state: motionDetectionEventInProgress
        is: true
    condition:
      type: time.between
      after: SUNSET
      before: SUNRISE
    actions:
      - type: device.command.OnOff
        devices: Hallway Light - Hallway
        on: true

  - starters:
      - type: device.state.MotionDetection
        device: Motion Sensor - Hallway
        state: motionDetectionEventInProgress
        is: false
        for: 5min
    actions:
      - type: device.command.OnOff
        devices: Hallway Light - Hallway
        on: false
```

### 6. Away Mode
Turn off devices and adjust thermostat when everyone leaves.

```yaml
metadata:
  name: Away Mode
  description: Adjust home when everyone leaves

automations:
  - starters:
      - type: home.state.HomePresence
        state: homePresenceMode
        is: AWAY
    actions:
      - type: device.command.OnOff
        devices:
          - Living Room Light - Living Room
          - Kitchen Light - Kitchen
          - Bedroom Light - Bedroom
        on: false
      - type: device.command.ThermostatTemperatureSetpoint
        devices: Nest Thermostat - Hallway
        thermostatTemperatureSetpoint: 62F
```

### 7. Movie Night Voice Command
Custom voice command to set up movie watching.

```yaml
metadata:
  name: Movie Night
  description: Set up the living room for movies

automations:
  - starters:
      - type: assistant.event.OkGoogle
        eventData: query
        is: Movie night
    actions:
      - type: device.command.BrightnessAbsolute
        devices: Living Room Light - Living Room
        brightness: 10
      - type: device.command.OpenClose
        devices: Living Room Blinds - Living Room
        openPercent: 0
      - type: device.command.OnOff
        devices: TV - Living Room
        on: true
```

### 8. Doorbell Alert
Flash lights when doorbell is pressed.

```yaml
metadata:
  name: Doorbell Alert
  description: Flash lights when someone rings the doorbell

automations:
  - starters:
      - type: device.event.DoorbellPress
        device: Video Doorbell - Front Door
    actions:
      - type: device.command.LightEffectPulse
        devices:
          - Living Room Light - Living Room
          - Kitchen Light - Kitchen
        duration: 30sec
```

---

## Important Notes

1. **Safety**: Automations are for convenience only, not safety-critical applications. Do not rely on them for security or situations where failure could cause harm.

2. **Visibility**: All household members can see when automations run.

3. **Device Names**: Device names must match exactly as shown in the Google Home app, including the room name.

4. **Testing**: Use the Validate button in the script editor before saving. Test automations manually before relying on scheduled execution.

5. **Device Quality**: Devices with poor report state reliability (<90%) may be blocked from use as starters. Devices with poor command execution (<95%) may be blocked from use in actions.
