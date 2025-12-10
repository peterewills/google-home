# Google Home Automation Documentation URLs

All URLs validated from official Google Home Developer documentation sidebar navigation.

Base URL: `https://developers.home.google.com`

## Main Documentation

| URL | Description |
|-----|-------------|
| `/codelabs/create-a-scripted-automation` | Tutorial: Create a scripted automation |
| `/automations/example-scripts` | Example scripted automations |
| `/automations/validation-errors` | Validation errors and warnings |
| `/automations/execution-logs` | Execution logs |

## Schema Reference

| URL | Description |
|-----|-------------|
| `/automations/schema` | Automation script overview |
| `/automations/schema/metadata` | metadata struct |
| `/automations/schema/automations` | automations struct (core) |
| `/automations/schema/basics` | Language basics (YAML syntax) |
| `/automations/starters-conditions-and-actions` | Supported starters, conditions, and actions |
| `/automations/supported-devices` | Supported devices |

## Standard Structs

| URL | Description |
|-----|-------------|
| `/automations/schema/reference/standard/script` | Script struct (top-level) |
| `/automations/schema/reference/standard/metadata` | Metadata struct |
| `/automations/schema/reference/standard/i18n_text` | I18nText struct (internationalization) |
| `/automations/schema/reference/standard/automation` | Automation struct |
| `/automations/schema/reference/standard/starter` | Starter struct |
| `/automations/schema/reference/standard/time_schedule_event` | TimeScheduleEvent struct |
| `/automations/schema/reference/standard/condition` | Condition struct |
| `/automations/schema/reference/standard/and_condition` | AndCondition struct |
| `/automations/schema/reference/standard/or_condition` | OrCondition struct |
| `/automations/schema/reference/standard/not_condition` | NotCondition struct |
| `/automations/schema/reference/standard/time_between_state` | TimeBetweenState struct |
| `/automations/schema/reference/standard/action` | Action struct |
| `/automations/schema/reference/standard/delay_action` | DelayAction struct |

## Entity Structs - Google Assistant

| URL | Description |
|-----|-------------|
| `/automations/schema/reference/entity/assistant/ok_google_event` | OkGoogleEvent (voice command starter) |
| `/automations/schema/reference/entity/assistant/ok_google_command` | OkGoogleCommand (voice command action) |
| `/automations/schema/reference/entity/assistant/broadcast_command` | BroadcastCommand (broadcast action) |

## Entity Structs - Home

| URL | Description |
|-----|-------------|
| `/automations/schema/reference/entity/sht_structure/home_presence_state` | HomePresenceState (HOME/AWAY) |
| `/automations/schema/reference/entity/sht_structure/notification_command` | NotificationCommand |

## Entity Structs - Device States

| URL | Description |
|-----|-------------|
| `/automations/schema/reference/entity/sht_device/app_selector_state` | AppSelectorState |
| `/automations/schema/reference/entity/sht_device/arm_disarm_state` | ArmDisarmState |
| `/automations/schema/reference/entity/sht_device/brightness_state` | BrightnessState |
| `/automations/schema/reference/entity/sht_device/channel_state` | ChannelState |
| `/automations/schema/reference/entity/sht_device/color_setting_state` | ColorSettingState |
| `/automations/schema/reference/entity/sht_device/cook_state` | CookState |
| `/automations/schema/reference/entity/sht_device/dock_state` | DockState |
| `/automations/schema/reference/entity/sht_device/energy_storage_state` | EnergyStorageState |
| `/automations/schema/reference/entity/sht_device/fan_speed_state` | FanSpeedState |
| `/automations/schema/reference/entity/sht_device/fill_state` | FillState |
| `/automations/schema/reference/entity/sht_device/humidity_setting_state` | HumiditySettingState |
| `/automations/schema/reference/entity/sht_device/input_selector_state` | InputSelectorState |
| `/automations/schema/reference/entity/sht_device/light_effects_state` | LightEffectsState |
| `/automations/schema/reference/entity/sht_device/lock_unlock_state` | LockUnlockState |
| `/automations/schema/reference/entity/sht_device/media_state_state` | MediaStateState |
| `/automations/schema/reference/entity/sht_device/motion_detection_state` | MotionDetectionState |
| `/automations/schema/reference/entity/sht_device/occupancy_sensing_state` | OccupancySensingState |
| `/automations/schema/reference/entity/sht_device/online_state` | OnlineState |
| `/automations/schema/reference/entity/sht_device/on_off_state` | OnOffState |
| `/automations/schema/reference/entity/sht_device/open_close_state` | OpenCloseState |
| `/automations/schema/reference/entity/sht_device/record_state` | RecordState |
| `/automations/schema/reference/entity/sht_device/rotation_state` | RotationState |
| `/automations/schema/reference/entity/sht_device/run_cycle_state` | RunCycleState |
| `/automations/schema/reference/entity/sht_device/sensor_state_state` | SensorStateState |
| `/automations/schema/reference/entity/sht_device/start_stop_state` | StartStopState |
| `/automations/schema/reference/entity/sht_device/temperature_control_state` | TemperatureControlState |
| `/automations/schema/reference/entity/sht_device/temperature_setting_state` | TemperatureSettingState |
| `/automations/schema/reference/entity/sht_device/timer_state` | TimerState |
| `/automations/schema/reference/entity/sht_device/volume_state` | VolumeState |

## Entity Structs - Device Events

| URL | Description |
|-----|-------------|
| `/automations/schema/reference/entity/sht_device/animal_other_detection_event` | AnimalOtherDetectionEvent |
| `/automations/schema/reference/entity/sht_device/doorbell_press_event` | DoorbellPressEvent |
| `/automations/schema/reference/entity/sht_device/face_familiar_detection_event` | FaceFamiliarDetectionEvent |
| `/automations/schema/reference/entity/sht_device/face_unfamiliar_detection_event` | FaceUnfamiliarDetectionEvent |
| `/automations/schema/reference/entity/sht_device/motion_detection_event` | MotionDetectionEvent |
| `/automations/schema/reference/entity/sht_device/moving_vehicle_detection_event` | MovingVehicleDetectionEvent |
| `/automations/schema/reference/entity/sht_device/package_delivered_event` | PackageDeliveredEvent |
| `/automations/schema/reference/entity/sht_device/person_detection_event` | PersonDetectionEvent |
| `/automations/schema/reference/entity/sht_device/person_talking_event` | PersonTalkingEvent |
| `/automations/schema/reference/entity/sht_device/sound_event` | SoundEvent |

## Entity Structs - Device Commands

| URL | Description |
|-----|-------------|
| `/automations/schema/reference/entity/sht_device/arm_disarm_command` | ArmDisarmCommand |
| `/automations/schema/reference/entity/sht_device/brightness_absolute_command` | BrightnessAbsoluteCommand |
| `/automations/schema/reference/entity/sht_device/brightness_relative_command` | BrightnessRelativeCommand |
| `/automations/schema/reference/entity/sht_device/color_absolute_command` | ColorAbsoluteCommand |
| `/automations/schema/reference/entity/sht_device/dock_command` | DockCommand |
| `/automations/schema/reference/entity/sht_device/on_off_command` | OnOffCommand |
| `/automations/schema/reference/entity/sht_device/open_close_command` | OpenCloseCommand |
| `/automations/schema/reference/entity/sht_device/start_stop_command` | StartStopCommand |
| `/automations/schema/reference/entity/sht_device/pause_unpause_command` | PauseUnpauseCommand |
| `/automations/schema/reference/entity/sht_device/lock_unlock_command` | LockUnlockCommand |
| `/automations/schema/reference/entity/sht_device/set_input_command` | SetInputCommand |
| `/automations/schema/reference/entity/sht_device/next_input_command` | NextInputCommand |
| `/automations/schema/reference/entity/sht_device/previous_input_command` | PreviousInputCommand |
| `/automations/schema/reference/entity/sht_device/light_effect_sleep_command` | LightEffectSleepCommand |
| `/automations/schema/reference/entity/sht_device/light_effect_wake_command` | LightEffectWakeCommand |
| `/automations/schema/reference/entity/sht_device/light_effect_pulse_command` | LightEffectPulseCommand |
| `/automations/schema/reference/entity/sht_device/light_effect_color_loop_command` | LightEffectColorLoopCommand |
| `/automations/schema/reference/entity/sht_device/stop_light_effect_command` | StopLightEffectCommand |
| `/automations/schema/reference/entity/sht_device/thermostat_temperature_setpoint_command` | ThermostatTemperatureSetpointCommand |
| `/automations/schema/reference/entity/sht_device/thermostat_temperature_set_range_command` | ThermostatTemperatureSetRangeCommand |
| `/automations/schema/reference/entity/sht_device/thermostat_set_mode_command` | ThermostatSetModeCommand |
| `/automations/schema/reference/entity/sht_device/mute_command` | MuteCommand |
| `/automations/schema/reference/entity/sht_device/set_volume_command` | SetVolumeCommand |
| `/automations/schema/reference/entity/sht_device/app_install_command` | AppInstallCommand |
| `/automations/schema/reference/entity/sht_device/app_search_command` | AppSearchCommand |
| `/automations/schema/reference/entity/sht_device/app_select_command` | AppSelectCommand |
| `/automations/schema/reference/entity/sht_device/select_channel_command` | SelectChannelCommand |
| `/automations/schema/reference/entity/sht_device/relative_channel_command` | RelativeChannelCommand |
| `/automations/schema/reference/entity/sht_device/return_channel_command` | ReturnChannelCommand |
| `/automations/schema/reference/entity/sht_device/cook_command` | CookCommand |
| `/automations/schema/reference/entity/sht_device/dispense_command` | DispenseCommand |
| `/automations/schema/reference/entity/sht_device/charge_command` | ChargeCommand |
| `/automations/schema/reference/entity/sht_device/set_fan_speed_command` | SetFanSpeedCommand |
| `/automations/schema/reference/entity/sht_device/set_fan_speed_relative_command` | SetFanSpeedRelativeCommand |
| `/automations/schema/reference/entity/sht_device/reverse_fan_command` | ReverseFanCommand |
| `/automations/schema/reference/entity/sht_device/fill_command` | FillCommand |
| `/automations/schema/reference/entity/sht_device/set_humidity_command` | SetHumidityCommand |
| `/automations/schema/reference/entity/sht_device/humidity_relative_command` | HumidityRelativeCommand |
| `/automations/schema/reference/entity/sht_device/find_my_device_command` | FindMyDeviceCommand |
| `/automations/schema/reference/entity/sht_device/reboot_command` | RebootCommand |
| `/automations/schema/reference/entity/sht_device/rotate_absolute_command` | RotateAbsoluteCommand |
| `/automations/schema/reference/entity/sht_device/activate_scene_command` | ActivateSceneCommand |
| `/automations/schema/reference/entity/sht_device/timer_start_command` | TimerStartCommand |
| `/automations/schema/reference/entity/sht_device/timer_adjust_command` | TimerAdjustCommand |
| `/automations/schema/reference/entity/sht_device/timer_pause_command` | TimerPauseCommand |
| `/automations/schema/reference/entity/sht_device/timer_resume_command` | TimerResumeCommand |
| `/automations/schema/reference/entity/sht_device/timer_cancel_command` | TimerCancelCommand |
| `/automations/schema/reference/entity/sht_device/media_stop_command` | MediaStopCommand |
| `/automations/schema/reference/entity/sht_device/media_next_command` | MediaNextCommand |
| `/automations/schema/reference/entity/sht_device/media_previous_command` | MediaPreviousCommand |
| `/automations/schema/reference/entity/sht_device/media_pause_command` | MediaPauseCommand |
| `/automations/schema/reference/entity/sht_device/media_resume_command` | MediaResumeCommand |
| `/automations/schema/reference/entity/sht_device/media_shuffle_command` | MediaShuffleCommand |
| `/automations/schema/reference/entity/sht_device/enable_disable_guest_network_command` | EnableDisableGuestNetworkCommand |
| `/automations/schema/reference/entity/sht_device/enable_disable_network_profile_command` | EnableDisableNetworkProfileCommand |

## External Resources

| URL | Description |
|-----|-------------|
| `https://home.google.com/automations` | Google Home web interface (script editor) |
| `https://support.google.com/googlenest/?p=script-editor` | Quick start guide |
