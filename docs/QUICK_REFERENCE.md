# ZMK Sofle - Quick Reference

## One-Page Cheat Sheet

---

## 📁 Repository Structure

```
zmk-sofle-1/
├── config/
│   ├── eyelash_sofle.keymap ← YOUR LAYOUT (edit this!)
│   ├── eyelash_sofle.conf   ← Settings
│   └── west.yml             ← Dependencies
├── .github/workflows/
│   ├── build.yml            ← Builds firmware
│   └── draw.yml             ← Draws keymap
├── build.yaml               ← What to build
└── byou.json                ← Your QMK layout reference
```

---

## 🚀 Common Tasks

### Build Firmware

**Via GitHub Actions** (easiest):
1. Go to: `github.com/YOUR_USERNAME/zmk-sofle-1/actions`
2. Click "Build ZMK firmware"
3. Click "Run workflow" → "Run workflow"
4. Wait 5-10 minutes
5. Download artifacts

**Via Git Push** (auto-trigger):
```bash
cmd /c cd /d "G:\Sofle Keyboard\zmk-sofle-1"
cmd /c git add config/eyelash_sofle.keymap
cmd /c git commit -m "Update keymap"
cmd /c git push
```

---

### Flash Firmware

**⚠️ ALWAYS FLASH RIGHT HALF FIRST, THEN LEFT!**

1. **Enter bootloader**: Double-press reset button
2. **Drive appears**: "NICENANO" USB drive
3. **Copy firmware**: Drag `.uf2` file to drive
4. **Wait**: Drive disconnects automatically (2-5 sec)
5. **Repeat**: Flash other half

**Files to Flash**:
- Right: `eyelash_sofle_right-nice_view-zmk.uf2`
- Left: `eyelash_sofle_left-nice_view-zmk.uf2`

---

### Edit Keymap

```bash
# Open keymap
code "G:\Sofle Keyboard\zmk-sofle-1\config\eyelash_sofle.keymap"

# Edit layers 52-119

# Commit and push
cmd /c cd /d "G:\Sofle Keyboard\zmk-sofle-1"
cmd /c git add config/
cmd /c git commit -m "Changed layout"
cmd /c git push

# Build automatically starts
```

---

## 🎹 Current Layout

### Layer 0 (Base - QWERTY)

```
┌───┬───┬───┬───┬───┬───┐       ┌───┬───┬───┬───┬───┬───┐
│ESC│ 1 │ 2 │ 3 │ 4 │ 5 │  ↑    │ 6 │ 7 │ 8 │ 9 │ 0 │BSP│
├───┼───┼───┼───┼───┼───┤  ↓    ├───┼───┼───┼───┼───┼───┤
│TAB│ Q │ W │ E │ R │ T │       │ Y │ U │ I │ O │ P │ \ │
├───┼───┼───┼───┼───┼───┤  ←    ├───┼───┼───┼───┼───┼───┤
│CAP│ A │ S │ D │ F │ G │       │ H │ J │ K │ L │ ; │ ' │
├───┼───┼───┼───┼───┼───┤  →    ├───┼───┼───┼───┼───┼───┤
│SFT│ Z │ X │ C │ V │ B │       │ N │ M │ , │ . │ / │ENT│
└───┴───┼───┼───┼───┼───┤       ├───┼───┼───┼───┼───┴───┘
 🔇VOL  │CTL│GUI│ALT│L1 │  CLK  │SPC│ENT│L2 │SFT│DEL
        └───┴───┴───┴───┘       └───┴───┴───┴───┘
```

**Encoder**: Volume Up/Down  
**Hold**: Layer 1 (left thumb) / Layer 2 (right thumb)

---

### Layer 1 (Function / Mouse / RGB)

```
┌───┬───┬───┬───┬───┬───┐       ┌───┬───┬───┬───┬───┬───┐
│ ` │F1 │F2 │F3 │F4 │F5 │  M↑   │F6 │F7 │F8 │F9 │F10│   │
├───┼───┼───┼───┼───┼───┤  M↓   ├───┼───┼───┼───┼───┼───┤
│   │ ` │LCK│MCK│RCK│MB4│       │PgU│End│ ↑ │Hom│ - │ = │
├───┼───┼───┼───┼───┼───┤  M←   ├───┼───┼───┼───┼───┼───┤
│   │ ~ │   │   │   │MB5│       │PgD│ ← │ ↓ │ → │ [ │ ] │
├───┼───┼───┼───┼───┼───┤  M→   ├───┼───┼───┼───┼───┼───┤
│   │RGF│RGN│EFF│EFR│SPI│       │BR+│BR-│Ins│F11│F12│   │
└───┴───┼───┼───┼───┼───┤       ├───┼───┼───┼───┼───┴───┘
        │   │   │   │▓▓▓│  LCK  │   │   │   │   │
        └───┴───┴───┴───┘       └───┴───┴───┴───┘
```

**Encoder**: Scroll Up/Down  
**Mouse**: LCK=Left Click, MCK=Middle, RCK=Right  
**RGB**: RGF=Off, RGN=On, EFF=Effect, BR+/-=Brightness

---

### Layer 2 (System / Bluetooth)

```
┌───┬───┬───┬───┬───┬───┐       ┌───┬───┬───┬───┬───┬───┐
│ ~ │BT0│BT1│BT2│BT3│BT4│  M↑   │F6 │F7 │F8 │F9 │F10│   │
├───┼───┼───┼───┼───┼───┤  M↓   ├───┼───┼───┼───┼───┼───┤
│   │CLR│CLA│   │   │   │       │   │   │F11│F12│ _ │ + │
├───┼───┼───┼───┼───┼───┤  M←   ├───┼───┼───┼───┼───┼───┤
│   │USB│BLE│   │   │   │       │   │   │   │   │ { │ } │
├───┼───┼───┼───┼───┼───┤  M→   ├───┼───┼───┼───┼───┼───┤
│   │RST│   │BTL│   │   │       │   │   │RST│OFF│BTL│   │
└───┴───┼───┼───┼───┼───┤       ├───┼───┼───┼───┼───┴───┘
        │   │   │   │   │  LCK  │   │   │▓▓▓│   │
        └───┴───┴───┴───┘       └───┴───┴───┴───┘
```

**Encoder**: Scroll Up/Down  
**BT0-4**: Bluetooth profiles 0-4  
**CLR**: Clear current profile  
**CLA**: Clear all profiles  
**USB/BLE**: Force output mode  
**RST**: Soft reset  
**BTL**: Bootloader (for flashing)  
**OFF**: Soft-off (deep sleep)

---

### Layer 3 & 4 (Empty)

Currently unused - available for customization!

---

## 🔑 Key Code Quick Reference

### Basic Keys

| Type | ZMK Code | Description |
|------|----------|-------------|
| **Letters** | `&kp A` - `&kp Z` | Alphabet |
| **Numbers** | `&kp N1` - `&kp N0` | Top row numbers |
| **Functions** | `&kp F1` - `&kp F12` | Function keys |
| **Modifiers** | `&kp LSHIFT`, `LCTRL`, `LALT`, `LGUI` | Left modifiers |
| **Special** | `&kp ENTER`, `SPACE`, `TAB`, `BSPC`, `DEL`, `ESC` | Common keys |

### Symbols

| Symbol | Code | Symbol | Code |
|--------|------|--------|------|
| `-` | `MINUS` | `_` | `UNDER` |
| `=` | `EQUAL` | `+` | `PLUS` |
| `[` | `LBKT` | `{` | `LBRC` |
| `]` | `RBKT` | `}` | `RBRC` |
| `\` | `BSLH` | `|` | `PIPE` |
| `;` | `SEMI` | `:` | `COLON` |
| `'` | `APOS` | `"` | `DQT` |
| `,` | `COMMA` | `<` | `LT` |
| `.` | `DOT` | `>` | `GT` |
| `/` | `FSLH` | `?` | `QMARK` |
| `` ` `` | `GRAVE` | `~` | `TILDE` |

### Layers

| Code | Description |
|------|-------------|
| `&mo 1` | Hold for layer 1, release to return |
| `&to 1` | Toggle to layer 1 (stays) |
| `&lt 1 SPACE` | Tap: space, hold: layer 1 |
| `&trans` | Transparent (pass to lower layer) |
| `&none` | No action |

### Mouse

| Code | Action |
|------|--------|
| `&mkp LCLK` | Left click |
| `&mkp RCLK` | Right click |
| `&mkp MCLK` | Middle click |
| `&mmv MOVE_UP` | Move cursor up |
| `&mmv MOVE_DOWN` | Move cursor down |
| `&mmv MOVE_LEFT` | Move cursor left |
| `&mmv MOVE_RIGHT` | Move cursor right |
| `&msc SCRL_UP` | Scroll up |
| `&msc SCRL_DOWN` | Scroll down |

### Media

| Code | Action |
|------|--------|
| `&kp C_MUTE` | Mute |
| `&kp C_VOL_UP` | Volume up |
| `&kp C_VOL_DN` | Volume down |
| `&kp C_PLAY_PAUSE` | Play/Pause |
| `&kp C_NEXT` | Next track |
| `&kp C_PREV` | Previous track |

### Bluetooth

| Code | Action |
|------|--------|
| `&bt BT_SEL 0` | Select profile 0 (1-4 also) |
| `&bt BT_CLR` | Clear current profile |
| `&bt BT_CLR_ALL` | Clear all profiles |
| `&out OUT_BLE` | Force Bluetooth |
| `&out OUT_USB` | Force USB |

### RGB

| Code | Action |
|------|--------|
| `&rgb_ug RGB_ON` | Turn RGB on |
| `&rgb_ug RGB_OFF` | Turn RGB off |
| `&rgb_ug RGB_TOG` | Toggle RGB |
| `&rgb_ug RGB_BRI` | Brightness up |
| `&rgb_ug RGB_BRD` | Brightness down |
| `&rgb_ug RGB_EFF` | Next effect |
| `&rgb_ug RGB_EFR` | Previous effect |

### System

| Code | Action |
|------|--------|
| `&sys_reset` | Soft reset |
| `&bootloader` | Enter bootloader |
| `&soft_off` | Deep sleep |

---

## 🐛 Troubleshooting

### Build Fails

| Issue | Fix |
|-------|-----|
| **Syntax error** | Check for missing `;` or `,` |
| **Invalid key code** | Use correct ZMK codes (not QMK) |
| **Wrong key count** | Each layer needs exactly 65 bindings |

### Keyboard Issues

| Issue | Fix |
|-------|-----|
| **Keys not working** | Reflash both halves (RIGHT first!) |
| **Bluetooth won't pair** | Press `BT_CLR` on Layer 2, repair |
| **One half dead** | Check battery, reflash that half |
| **Random key presses** | Increase debounce in `.conf` file |
| **Won't enter bootloader** | Try different USB cable |

### Common Fixes

```bash
# Settings reset (fixes most issues)
# 1. Flash settings_reset-nice_nano_v2-zmk.uf2 to LEFT
# 2. Immediately reflash normal firmware
# 3. Repeat for RIGHT if needed

# Clear Bluetooth
# - On keyboard: Access Layer 2
# - Press BT_CLR_ALL key
# - On computer: Forget/unpair device
# - Re-pair from scratch
```

---

## ⚙️ Configuration Files

### eyelash_sofle.conf

Key settings you might change:

```c
# Sleep timeout (milliseconds)
CONFIG_ZMK_IDLE_SLEEP_TIMEOUT=3600000  # 1 hour

# RGB brightness (0-100)
CONFIG_ZMK_RGB_UNDERGLOW_BRT_MAX=90

# Debounce timing (milliseconds)
CONFIG_ZMK_KSCAN_DEBOUNCE_PRESS_MS=8
CONFIG_ZMK_KSCAN_DEBOUNCE_RELEASE_MS=8

# RGB auto-off
CONFIG_ZMK_RGB_UNDERGLOW_AUTO_OFF_IDLE=y  # Turn off when idle
CONFIG_ZMK_RGB_UNDERGLOW_ON_START=n        # Don't start with RGB on
```

### build.yaml

What gets built:

```yaml
- board: eyelash_sofle_right    # Right half
  shield: nice_view
  
- board: eyelash_sofle_left     # Left half
  shield: nice_view
  
- board: eyelash_sofle_left     # Studio left (live editing)
  shield: nice_view
  cmake-args: -DCONFIG_ZMK_STUDIO=y
```

---

## 📱 Special Features

### Soft Off (Deep Sleep)

**Activate**: Press Q + S + Z simultaneously, hold 2 seconds  
**Wake**: Press reset button once  
**Use**: Travel/storage to save battery

### ZMK Studio (Left Half Only)

**Enable**: Flash `eyelash_sofle_studio_left` firmware  
**Use**: Connect via USB, edit keymap live  
**Link**: https://zmk.studio (in browser)

### Bluetooth Profiles

**5 devices** supported:
- Profile 0-4: `BT_SEL 0` through `BT_SEL 4` on Layer 2
- **Switch**: Press corresponding `BT_SEL` key
- **Clear**: `BT_CLR` (current) or `BT_CLR_ALL` (all)

---

## 📚 File Locations

| File | Purpose |
|------|---------|
| `config/eyelash_sofle.keymap` | **EDIT THIS** - Your layout |
| `config/eyelash_sofle.conf` | Hardware settings |
| `build.yaml` | Build configuration |
| `byou.json` | QMK layout reference (not used by ZMK) |
| `.github/workflows/build.yml` | Build automation |
| `.github/workflows/draw.yml` | Keymap visualization |
| `keymap-drawer/eyelash_sofle.svg` | Visual keymap (auto-generated) |

---

## 🔗 Useful Links

| Resource | URL |
|----------|-----|
| **ZMK Docs** | https://zmk.dev/docs |
| **Key Codes** | https://zmk.dev/docs/codes |
| **Behaviors** | https://zmk.dev/docs/behaviors |
| **Keymap Editor** | https://nickcoutsos.github.io/keymap-editor/ |
| **ZMK Discord** | https://zmk.dev/community/discord/invite |
| **Board Repo** | https://github.com/a741725193/zmk-sofle |

---

## 💡 Pro Tips

1. **Test locally**: Use ZMK Studio for rapid testing (left half only)
2. **Backup**: Keep a working firmware copy before major changes
3. **Document**: Comment your keymap with `//` for future reference
4. **Visualize**: Check `keymap-drawer/eyelash_sofle.svg` after changes
5. **Start small**: Test one layer change at a time
6. **Use git**: Commit often with descriptive messages
7. **Layer logic**: 
   - Layer 0: Base layout
   - Layer 1: Functions, mouse, RGB
   - Layer 2: System, Bluetooth
   - Layer 3-4: Custom (empty now)

---

## 📋 Quick Flash Checklist

```
Before Flashing:
[ ] Firmware downloaded and extracted
[ ] USB cable ready
[ ] Both halves accessible

Flash Process:
[ ] Connect RIGHT half
[ ] Double-press reset
[ ] Drag right .uf2 to drive
[ ] Wait for disconnect
[ ] Wait 30 seconds
[ ] Connect LEFT half
[ ] Double-press reset
[ ] Drag left .uf2 to drive
[ ] Wait for disconnect
[ ] Test keyboard

Verify:
[ ] Both halves respond
[ ] Layers work
[ ] Bluetooth pairs
[ ] Encoder works
```

---

## 🆘 Emergency Commands

```bash
# Reset to last working version
cmd /c cd /d "G:\Sofle Keyboard\zmk-sofle-1"
cmd /c git log --oneline -5  # Find last good commit
cmd /c git checkout COMMIT_HASH config/eyelash_sofle.keymap
cmd /c git push

# Force rebuild
cmd /c git commit --allow-empty -m "Rebuild"
cmd /c git push

# Check build logs
# Go to: github.com/YOUR_USERNAME/zmk-sofle-1/actions
# Click failed build → Click "build" job → Read logs
```

---

**For detailed guides, see**:
- [PROJECT_OVERVIEW.md](./PROJECT_OVERVIEW.md) - Full documentation
- [BUILD_GUIDE.md](./BUILD_GUIDE.md) - Building and flashing
- [KEYMAP_GUIDE.md](./KEYMAP_GUIDE.md) - Layout customization

---

**Last Updated**: 2025-11-07  
**Version**: ZMK v0.3.0
