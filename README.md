# Caldera Split Keyboard - nice!nano v2 with RGB LEDs

Custom wireless split keyboard with professional RGB LED animations.

## Features

- 🎹 Split keyboard (70 keys - 35 per half)
- 📡 Wireless Bluetooth
- 🔋 3.7V LiPo battery powered
- 🎨 Professional RGB LED animations (wave, spectrum, breathe, swirl)
- 💡 Full brightness and color control

## LED Setup

### Quick Facts

- ✅ Your 3.7V battery works perfectly with WS2812B LEDs
- ✅ Professional animations built into ZMK firmware
- ✅ Simple 3-wire connection per keyboard half
- ✅ Multiple animation modes with easy controls

### Documentation

**Complete wiring and setup guide:**
- **[PROFESSIONAL_LED_SETUP.md](PROFESSIONAL_LED_SETUP.md)** - How to wire LEDs for professional animations
- **[PROFESSIONAL_WIRING.txt](PROFESSIONAL_WIRING.txt)** - Detailed wiring diagrams

### LED Controls

Hold **LOWER** layer key + these keys:

| Key | Function |
|-----|----------|
| U | Toggle LEDs on/off |
| I | Next effect (Solid → Breathe → Spectrum → Swirl) |
| O/J | Change color |
| [/L | Brightness up/down |
| P/K | Saturation up/down |

### Recommended Setup

**Start with 10 LEDs per half (underglow):**
- Battery life: 30-40 hours @ 30% brightness
- Cost: ~$10
- Time: 1-2 hours to install
- All effects work great

## Wiring Summary

Each keyboard half needs 3 wires to nice!nano:

```
LED System  →  nice!nano v2
VCC Bus     →  VCC (pin 10)
GND Bus     →  GND (pin 11)
Data Chain  →  P0.06 (pin 9)
```

See [PROFESSIONAL_WIRING.txt](PROFESSIONAL_WIRING.txt) for complete diagrams.

## Firmware

### Configuration Files

- `config/boards/shields/caldera/caldera_left.overlay` - Left side with LED config
- `config/boards/shields/caldera/caldera_right.overlay` - Right side with LED config
- `config/boards/shields/caldera/caldera_left.conf` - RGB features enabled
- `config/boards/shields/caldera/caldera_right.conf` - RGB features enabled
- `config/caldera.keymap` - Keymap with RGB controls

### Update LED Count

Edit both overlay files and change:
```c
chain-length = <10>;  // Change to your actual LED count
```

### Building

1. Update `chain-length` in both overlay files
2. Commit and push to GitHub
3. GitHub Actions builds firmware automatically
4. Download `.uf2` files from Actions tab

### Flashing

1. Plug nice!nano into USB
2. Double-tap reset button
3. Copy `.uf2` file to USB drive that appears
4. Drive disconnects when done
5. Repeat for other half

## Battery Life

With 3.7V, 350mAh battery:

| LEDs per half | Brightness | Battery Life |
|---------------|------------|--------------|
| 10 | 30% | 30-40 hours |
| 15 | 30% | 20-25 hours |
| 35 (per-key) | 20% | 8-12 hours |

## Shopping List

For 10 LED underglow setup:
- WS2812B LED strips or individual LEDs: $5-10
- 26-30 AWG wire (red, black, white): $3-5
- **Total: ~$10-15**

## Resources

- **ZMK Firmware:** https://zmk.dev/
- **ZMK Discord:** https://zmk.dev/community/discord/invite
- **nice!nano Docs:** https://nicekeyboards.com/docs/nice-nano/

## License

This configuration follows the ZMK firmware project license.

---

**Get started:** Read [PROFESSIONAL_LED_SETUP.md](PROFESSIONAL_LED_SETUP.md) for complete wiring instructions and animation setup!