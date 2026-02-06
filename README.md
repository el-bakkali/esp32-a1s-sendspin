# ESP32-A1S Audio Kit - Sendspin Configuration

[![ESPHome](https://img.shields.io/badge/ESPHome-2026.1.x-blue.svg)](https://esphome.io/)
[![Music Assistant](https://img.shields.io/badge/Music%20Assistant-Sendspin-green.svg)](https://music-assistant.io/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A working ESPHome configuration for the **AI-Thinker ESP32-A1S Audio Kit** with **Sendspin** protocol support for synchronized multi-room audio playback via [Music Assistant](https://music-assistant.io/).

## Features

- ✅ **Sendspin Protocol** - Synchronized multi-room audio playback
- ✅ **ES8388 Audio Codec** - High-quality audio DAC/ADC
- ✅ **Music Assistant Integration** - Stream music from various sources
- ✅ **Track Metadata** - Display track title, artist, album info
- ✅ **Hardware Controls** - 6 physical buttons on the board
- ✅ **Jack Detection** - Automatic headphone jack status
- ✅ **Microphone Support** - Built-in microphone input
- ✅ **LED Control** - Onboard status LED

## Requirements

- **Hardware**: AI-Thinker ESP32-A1S Audio Kit (with ES8388 codec)
- **Software**: 
  - ESPHome 2026.1.x or later
  - Home Assistant
  - Music Assistant 2.7.0 beta 19 or later

## Quick Start

### 1. Clone this repository

```bash
git clone https://github.com/el-bakkali/esp32-a1s-sendspin.git
cd esp32-a1s-sendspin
```

### 2. Create your secrets file

Copy the example secrets file and fill in your details:

```bash
cp secrets.yaml.example secrets.yaml
```

Edit `secrets.yaml` with your credentials:

```yaml
wifi_ssid: "Your-WiFi-Name"
wifi_password: "Your-WiFi-Password"
api_encryption_key: "your-32-character-base64-key"
ota_password: "your-ota-password"
ap_password: "fallback-ap-password"
```

> **Tip**: Generate an API encryption key using: `openssl rand -base64 32`

### 3. Flash to your device

```bash
esphome run esp32-a1s.yaml
```

Or use the ESPHome Dashboard in Home Assistant.

### 4. Configure Music Assistant

1. Install Music Assistant in Home Assistant
2. Add your ESP32-A1S as a player
3. The device will appear as "Sendspin Media Player"
4. Start streaming!

## Hardware Pin Configuration

| Function | GPIO | Notes |
|----------|------|-------|
| I2C SDA | GPIO33 | ES8388 control |
| I2C SCL | GPIO32 | ES8388 control |
| I2S LRCLK | GPIO25 | Word select |
| I2S BCLK | GPIO27 | Bit clock |
| I2S MCLK | GPIO0 | Master clock |
| I2S DOUT | GPIO26 | Speaker output |
| I2S DIN | GPIO35 | Microphone input |
| AMP Enable | GPIO21 | Amplifier switch |
| LED | GPIO22 | Red status LED |
| Jack Detect | GPIO39 | Headphone detection |
| Key 1 | GPIO36 | Button |
| Key 2 | GPIO13 | Button |
| Key 3 | GPIO19 | Button |
| Key 4 | GPIO23 | Button |
| Key 5 | GPIO18 | Button |
| Key 6 | GPIO5 | Button |

## DIP Switch Configuration

For the ESP32 Audio Kit V2.2, set the DIP switches as follows:

| Switch | Position | Purpose |
|--------|----------|---------|
| 1 | ON | |
| 2 | ON | |
| 3 | ON | |
| 4 | OFF | |
| 5 | OFF | |

> **Note:** Incorrect DIP switch settings can prevent audio output or interfere with flashing/serial communication.

## Troubleshooting

### No Audio Output

1. **Check DAC Output setting** - DAC Output is automatically set to `BOTH` on boot. If changed, verify it's set back to `BOTH` in Home Assistant
2. **Verify AMP Switch** - Make sure "AMP Switch" is ON
3. **Check volume** - Ensure media player volume is not at minimum
4. **Clear ESPHome cache** - Delete `.esphome/external_components/` folder and recompile

### Compilation Errors

If you encounter `include_builtin_idf_component` errors:
- This config uses a specific audio component commit that works with ESPHome 2026.1.x
- Once ESPHome 2026.2.0 is released, the external components can be simplified

### Connection Issues

- Ensure your WiFi credentials are correct in `secrets.yaml`
- Check that Music Assistant 2.7.0 beta 19 or later is installed
- Verify the device appears in Home Assistant

## External Components

This configuration uses several external components from ESPHome pull requests:

| Component | PR | Description |
|-----------|-----|-------------|
| audio | [commit 9148832](https://github.com/esphome/esphome/commit/9148832ea4e54907bad71a24d4ced1ce6c862433) | Audio processing |
| mixer | [#12253](https://github.com/esphome/esphome/pull/12253) | Audio mixer |
| resampler | [#12254](https://github.com/esphome/esphome/pull/12254) | Sample rate conversion |
| media_player | [#12258](https://github.com/esphome/esphome/pull/12258) | Media player platform |
| sendspin | [#12284](https://github.com/esphome/esphome/pull/12284) | Sendspin protocol |
| speaker_source | [#12429](https://github.com/esphome/esphome/pull/12429) | Speaker source media player |

> **Note**: These are work-in-progress PRs. Configuration may need updates as they are merged into ESPHome.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- [ESPHome](https://esphome.io/) team for the amazing platform
- [Music Assistant](https://music-assistant.io/) team for Sendspin protocol
- [@kahrendt](https://github.com/kahrendt) for the Sendspin ESPHome implementation
- The ESPHome community for testing and feedback

## Related Links

- [ESPHome ES8388 Documentation](https://esphome.io/components/audio_dac/es8388/)
- [Sendspin PR #12284](https://github.com/esphome/esphome/pull/12284)
- [Music Assistant](https://music-assistant.io/)
