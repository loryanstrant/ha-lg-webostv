# LG webOS TV Classic

[![hacs_badge](https://img.shields.io/badge/HACS-Custom-41BDF5.svg)](https://github.com/hacs/integration)

An alternative implementation of the LG webOS TV integration for Home Assistant with classic availability behavior.

## Why this integration?

The official Home Assistant webOS TV integration changed its availability behavior in [PR #155164](https://github.com/home-assistant/core/pull/155164). This change made the TV entity show as `unavailable` instead of `off` when there's no connection to the TV (which happens when the TV is in standby, since LG TVs close their network connection when turned off).

This custom component restores the **classic behavior** where:
- The TV entity always shows as `off` when disconnected (not `unavailable`)
- This allows automations and scripts that depend on the `off` state to continue working as expected
- No logging spam about unavailability changes

## Installation

### HACS (Recommended)

1. Open HACS in your Home Assistant instance
2. Click on "Integrations"
3. Click the three dots in the top right corner
4. Select "Custom repositories"
5. Add `https://github.com/loryanstrant/ha-lg-webostv` as the repository URL
6. Select "Integration" as the category
7. Click "Add"
8. Search for "LG webOS TV Classic" and install it
9. Restart Home Assistant

### Manual Installation

1. Copy the `custom_components/webostv_classic` folder to your Home Assistant `config/custom_components` directory
2. Restart Home Assistant

## Configuration

After installation, add the integration through the Home Assistant UI:

1. Go to **Settings** → **Devices & Services**
2. Click **+ Add Integration**
3. Search for "LG webOS TV Classic"
4. Follow the setup wizard to pair with your TV

## Features

This integration provides all the features of the official webOS TV integration:

- Media player controls (play, pause, stop, volume, etc.)
- Source selection (inputs, apps)
- Send button presses
- Send custom commands
- Sound output selection
- Notifications
- Device automation triggers (turn on)

## Important Notes

- This integration uses a different domain (`webostv_classic`) than the official integration (`webostv`)
- You can run both integrations simultaneously if needed
- Entity IDs will be different from the official integration (e.g., `media_player.lg_webos_tv_classic_xxxxx`)

## Differences from Official Integration

| Feature | Official webOS TV | webOS TV Classic |
|---------|-------------------|------------------|
| Availability when TV is off | `unavailable` (if no turn_on automation) | Always `off` |
| Logging | Logs availability changes | Silent on connection failures |

## License

This project is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) file for details.

## Credits

This integration is based on the official Home Assistant [webOS TV integration](https://github.com/home-assistant/core/tree/dev/homeassistant/components/webostv), with modifications to restore the classic availability behavior.
