# Microsoft Family Safety integration

## Purpose

This repository stores Home Assistant configuration for recording Microsoft Family Safety data once it is exposed as Home Assistant entities.

The intended reporting scope is:

- screen time by child
- app or device usage where exposed by the integration
- pending requests where exposed by the integration
- at least the last 7 days of recorded history

## Important limitation

Microsoft does not provide an official public Family Safety API for screen-time or activity reporting.

Therefore, this repository should not contain:

- Microsoft account passwords
- browser cookies
- CSRF tokens
- reverse-engineered Microsoft endpoint credentials
- child-account secrets

## Recommended setup

1. Install a Microsoft Family Safety custom integration through HACS.
2. Authenticate manually in Home Assistant.
3. Confirm that sensors appear in **Developer Tools > States**.
4. Restart Home Assistant.
5. Confirm that `sensor.microsoft_family_safety_integration_status` changes to `detected`.
6. Keep recorder retention at minimum 10 days for weekly reporting.

## Expected sensor naming

The configuration records sensors matching patterns such as:

- `sensor.microsoft_family_*`
- `sensor.family_safety_*`
- `sensor.*_screen_time*`
- `sensor.*_device_usage*`
- `sensor.*_app_usage*`

If the installed custom integration uses different entity names, update `configuration.yaml`.

## Recommended architecture

```text
Microsoft Family Safety
        |
        | Custom Home Assistant integration
        v
Home Assistant sensors
        |
        | Recorder history, 10+ days
        v
Weekly report or dashboard export
```
