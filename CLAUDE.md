# Google Home Automation Scripts

This project is for writing, validating, and storing YAML scripts that create Google Home automations.

## Project Structure

- `docs/` - Reference documentation
  - `automation-reference.md` - Core reference for script syntax (starters, conditions, actions, examples)
  - `device-list.md` - The user's actual device names (check before writing any script)
  - `google-home-automation-urls.md` - URLs for official Google documentation
  - `google-home-agent.md` - Agent instructions for automation scripting
  - `script-template.yaml` - Blank template for new scripts
- `scripts/` - Saved automation scripts (YAML files)

## Workflow

1. **Read the reference docs first** - Start with `docs/automation-reference.md` for syntax and `docs/device-list.md` for device names
2. **Verify device names** - Device names must match EXACTLY as listed in `device-list.md` (spelling, capitalization, room suffix)
3. **Write the script** - Use proper YAML formatting with 2-space indentation
4. **If unsure about a capability** - Look up the URL in `google-home-automation-urls.md` and fetch the documentation from `https://developers.home.google.com`

## Script Structure

```yaml
metadata:
  name: Script Name
  description: What this script does

automations:
  - starters:
      - type: <starter_type>
    condition:  # optional
      type: <condition_type>
    actions:
      - type: <action_type>
```

## Key References

- **Common starters**: `time.schedule`, `assistant.event.OkGoogle`, `device.state.OnOff`, `home.state.HomePresence`
- **Common actions**: `device.command.OnOff`, `device.command.BrightnessAbsolute`, `device.command.ColorAbsolute`, `time.delay`
- **Common conditions**: `time.between`, `device.state.*`, `and`/`or`/`not`
- **Data formats**: Time (`6:00 pm`, `SUNSET`), Duration (`5min`), Temperature (`72F`), Weekdays (`MON`, `TUE`, etc.)

## Important Notes

- If a device name doesn't exist in `device-list.md`, ask for the correct name before proceeding
- Scripts can be validated in the Google Home web editor at https://home.google.com/automations
- Multiple automations can exist in one script file
