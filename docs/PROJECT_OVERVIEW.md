# ZMK Sofle Keyboard - Project Overview

## Table of Contents
1. [Introduction](#introduction)
2. [Repository Structure](#repository-structure)
3. [Key Components](#key-components)
4. [How It Works](#how-it-works)
5. [Build Process](#build-process)
6. [Customization](#customization)

---

## Introduction

This repository contains the ZMK firmware configuration for the **Eyelash Sofle** keyboard - a custom split mechanical keyboard running ZMK (Zephyr Mechanical Keyboard) firmware. The Sofle is a 6x4+5 split keyboard with encoders, RGB underglow, OLED displays, and mouse support.

### Key Features
- **Split Keyboard**: Left and right halves connected via Bluetooth
- **ZMK Studio Support**: Left hand supports ZMK Studio for live keymap editing
- **Wireless**: Bluetooth connectivity with multi-device support (up to 5 profiles)
- **RGB Underglow**: WS2812 LED strip support with power management
- **OLED Displays**: Nice!View displays on both halves
- **Rotary Encoders**: EC11 encoder support with custom scroll behaviors
- **Mouse Emulation**: Built-in pointing device support
- **Power Management**: Advanced sleep modes and soft-off functionality

---

## Repository Structure

```
zmk-sofle-1/
├── .github/
│   └── workflows/
│       ├── build.yml         # GitHub Actions: Build firmware
│       └── draw.yml          # GitHub Actions: Generate keymap visualizations
├── boards/
│   └── arm/
│       └── eyelash_sofle/    # Custom board definition
├── config/
│   ├── eyelash_sofle.conf    # Keyboard configuration settings
│   ├── eyelash_sofle.keymap  # Keymap definition (YOUR LAYOUT)
│   ├── eyelash_sofle.json    # JSON keymap export
│   └── west.yml              # Zephyr west manifest (dependencies)
├── keymap-drawer/            # Generated keymap visualization files
├── build.yaml                # Build configuration (what to build)
├── byou.json                 # Your QMK-format layout reference
└── README.md                 # Project README
```

---

## Key Components

### 1. **build.yaml** - Build Configuration
Defines what firmware variants to build:

- **Right Half**: `eyelash_sofle_right` with nice_view display
- **Left Half (Standard)**: `eyelash_sofle_left` with nice_view display
- **Left Half (Studio)**: Left with ZMK Studio enabled for live editing
- **Settings Reset**: Utility firmware to reset keyboard settings

### 2. **config/eyelash_sofle.keymap** - Your Keyboard Layout
This is the **main file** you'll edit to customize your keyboard. It contains:

- **5 Layers**: Base layer + 4 additional layers
- **Key Bindings**: What each key does
- **Behaviors**: Custom actions (scroll encoder, combos, etc.)
- **Sensor Bindings**: Encoder behavior per layer

**Current Layers:**
- **Layer 0**: Base QWERTY layer with standard keys
- **Layer 1**: Function keys, mouse controls, RGB controls, navigation
- **Layer 2**: Bluetooth management, system controls, bootloader access
- **Layer 3-4**: Empty layers for future customization

### 3. **config/eyelash_sofle.conf** - Configuration Settings
Hardware and feature configuration:

- **Sleep Timeout**: 1 hour idle sleep
- **RGB Settings**: Underglow with auto-off, max brightness 90%
- **Mouse Support**: Pointing device enabled
- **Encoder Support**: EC11 rotary encoder enabled
- **Debounce**: 8ms press/release debounce
- **Soft Off**: Deep sleep combo (Q+S+Z held 2 seconds)

### 4. **config/west.yml** - Dependencies
Defines external dependencies:

- **ZMK Core**: v0.3.0 from zmkfirmware
- **Board Support**: Custom eyelash_sofle board from GitHub

### 5. **byou.json** - Your QMK Layout Reference
This is a **QMK Configurator export** documenting your non-standard layout. It's a reference file showing your desired key positions but **NOT USED** by ZMK directly. You'd need to manually translate this to the `.keymap` file.

---

## How It Works

### GitHub Actions Workflow

#### **Build Process** (`.github/workflows/build.yml`)

1. **Trigger**: 
   - Manual trigger via GitHub Actions UI ("Run workflow" button)
   - Automatic on push to repository (except keymap-drawer files)

2. **What Happens**:
   - GitHub Actions calls ZMK's official build workflow
   - Reads `build.yaml` to know what to build
   - Pulls ZMK firmware source (v0.3.0)
   - Pulls custom board definition from `a741725193/zmk-sofle`
   - Compiles firmware for each configuration in `build.yaml`
   - Generates `.uf2` firmware files
   - Publishes artifacts for download

3. **Output**:
   - `eyelash_sofle_left-nice_view-zmk.uf2` (Left half)
   - `eyelash_sofle_right-nice_view-zmk.uf2` (Right half)
   - `eyelash_sofle_studio_left-nice_view-zmk.uf2` (Left with ZMK Studio)
   - `settings_reset-nice_nano_v2-zmk.uf2` (Settings reset utility)

#### **Keymap Drawing** (`.github/workflows/draw.yml`)

1. **Trigger**:
   - Automatic when `config/` files change
   - Manual trigger

2. **What Happens**:
   - Parses your `.keymap` file
   - Generates SVG visualization using keymap-drawer
   - Commits the generated image back to the repository

3. **Output**:
   - `keymap-drawer/eyelash_sofle.svg` (Visual representation of your keymap)

---

### Firmware Architecture

```
┌─────────────────────────────────────────┐
│     Your Fork (zmk-sofle-1)             │
│  ┌─────────────────────────────────┐    │
│  │   config/eyelash_sofle.keymap   │◄───┼── YOU EDIT THIS
│  │   config/eyelash_sofle.conf     │◄───┼── YOU EDIT THIS
│  │   build.yaml                    │◄───┼── YOU EDIT THIS
│  └─────────────────────────────────┘    │
└─────────────────────────────────────────┘
                    │
                    │ GitHub Actions Build
                    ▼
┌─────────────────────────────────────────┐
│   ZMK Firmware (v0.3.0)                 │
│   github.com/zmkfirmware/zmk            │
└─────────────────────────────────────────┘
                    +
┌─────────────────────────────────────────┐
│   Custom Board Definition               │
│   github.com/a741725193/zmk-sofle       │
└─────────────────────────────────────────┘
                    │
                    │ Compilation
                    ▼
┌─────────────────────────────────────────┐
│   Firmware Files (.uf2)                 │
│   - Left Half                           │
│   - Right Half                          │
│   - Studio Left                         │
│   - Settings Reset                      │
└─────────────────────────────────────────┘
```

---

## Build Process

### Step-by-Step: Building Your Firmware

#### **Prerequisites**
- Forked this repository to your GitHub account ✓ (You've done this)
- GitHub account with Actions enabled

#### **Method 1: Automatic Build (Push Trigger)**

1. **Edit your keymap locally**:
   ```bash
   # Navigate to config directory
   cmd /c cd /d "G:\Sofle Keyboard\zmk-sofle-1\config"
   
   # Edit the keymap file
   # Make changes to eyelash_sofle.keymap
   ```

2. **Commit and push**:
   ```bash
   cmd /c cd /d "G:\Sofle Keyboard\zmk-sofle-1"
   cmd /c git add config/eyelash_sofle.keymap
   cmd /c git commit -m "Update keymap"
   cmd /c git push
   ```

3. **Build starts automatically**
   - GitHub Actions detects the push
   - Build workflow runs automatically
   - Check progress at: `https://github.com/YOUR_USERNAME/zmk-sofle-1/actions`

#### **Method 2: Manual Build (Workflow Dispatch)**

1. **Go to GitHub Actions**:
   - Navigate to: `https://github.com/YOUR_USERNAME/zmk-sofle-1/actions`

2. **Select "Build ZMK firmware"** from the left sidebar

3. **Click "Run workflow"** button (top right)

4. **Select branch** (usually `main`) and click green "Run workflow" button

5. **Wait for build** (takes 5-10 minutes)

#### **Downloading Firmware**

1. **Go to completed workflow run**:
   - Click on the successful workflow run in Actions tab

2. **Scroll to "Artifacts" section** at the bottom

3. **Download the firmware ZIP** file

4. **Extract** to get individual `.uf2` files

#### **Flashing Firmware**

1. **Enter bootloader mode**:
   - Double-press the reset button on your keyboard
   - OR use the bootloader key combo (Layer 2 + specific key)

2. **Keyboard appears as USB drive** (e.g., "NICENANO")

3. **Copy the appropriate .uf2 file** to the drive:
   - `eyelash_sofle_left-*.uf2` → Left half
   - `eyelash_sofle_right-*.uf2` → Right half

4. **Drive disconnects automatically** - firmware is now flashed!

5. **Repeat for the other half**

---

## Customization

### Editing Your Keymap

The main file you'll edit is `config/eyelash_sofle.keymap`.

#### **Basic Structure**

```c
keymap {
    compatible = "zmk,keymap";
    
    layer0 {
        bindings = <
            // Row 1: 13 keys
            &kp ESC  &kp N1  &kp N2  ...  &kp BACKSPACE
            // Row 2: 13 keys
            &kp TAB  &kp Q   &kp W   ...  &kp BSLH
            // Row 3: 13 keys
            ...
            // Row 4: 13 keys
            ...
            // Row 5: 10 keys (thumb cluster)
            ...
        >;
    };
}
```

#### **Key Code Reference**

- **Basic Keys**: `&kp A`, `&kp N1`, `&kp ESC`, `&kp ENTER`
- **Modifiers**: `&kp LSHIFT`, `&kp LCTRL`, `&kp LALT`, `&kp LGUI`
- **Layer Access**: `&mo 1` (momentary), `&lt 1 SPACE` (layer-tap)
- **Mouse**: `&mkp LCLK` (left click), `&mmv MOVE_UP` (move up)
- **Bluetooth**: `&bt BT_SEL 0` (select profile), `&bt BT_CLR` (clear)
- **RGB**: `&rgb_ug RGB_ON`, `&rgb_ug RGB_TOG`, `&rgb_ug RGB_BRI`
- **System**: `&sys_reset`, `&bootloader`, `&soft_off`

#### **Common Modifications**

1. **Change a single key**:
   ```c
   // Before: &kp Q
   // After:  &kp A
   ```

2. **Add a layer toggle**:
   ```c
   &mo 2  // Hold to activate layer 2
   ```

3. **Create key combo**:
   ```c
   combos {
       compatible = "zmk,combos";
       
       my_combo {
           bindings = <&kp ESC>;
           key-positions = <0 1>;  // Keys at position 0 and 1
       };
   };
   ```

#### **Using byou.json as Reference**

Your `byou.json` file shows a non-standard layout. To apply it:

1. **Open `byou.json`** to see your desired layout
2. **Find key positions** in the "layers" array
3. **Translate QMK codes to ZMK codes**:
   - QMK: `KC_ESC` → ZMK: `&kp ESC`
   - QMK: `KC_1` → ZMK: `&kp N1`
   - QMK: `KC_LSFT` → ZMK: `&kp LSHIFT`
4. **Update `eyelash_sofle.keymap`** with new bindings

---

## Advanced Features

### ZMK Studio Support

**Left half only** can use ZMK Studio for live editing:

1. Flash the `eyelash_sofle_studio_left` firmware
2. Connect via USB
3. Use ZMK Studio web app to edit keymap in real-time
4. No need to rebuild/reflash for testing changes

### Soft Off Feature

**Deep sleep combo**: Press Q + S + Z simultaneously for 2 seconds
- Keyboard enters ultra-low power mode
- Cannot wake with keypress
- **Wake method**: Press reset button once
- Perfect for travel/storage

### Mouse Emulation

Layer 1 includes mouse controls:
- Movement: Directional arrows in encoder column
- Clicks: `&mkp LCLK`, `&mkp RCLK`, `&mkp MCLK`
- Scroll: Encoder becomes scroll wheel on Layer 1 & 2

### RGB Underglow

Control via Layer 1:
- `RGB_ON` / `RGB_OFF`: Toggle underglow
- `RGB_BRI` / `RGB_BRD`: Brightness up/down
- `RGB_EFF` / `RGB_EFR`: Effect forward/reverse
- Auto-off when idle (configurable in `.conf`)

---

## Troubleshooting

### Build Fails on GitHub Actions

1. **Check workflow logs**: Click on failed run → Click on "build" job
2. **Common issues**:
   - Syntax error in `.keymap` file (missing semicolon, wrong binding format)
   - Invalid key code
   - Incorrect layer structure

### Keyboard Not Working After Flash

1. **Flash both halves**: Ensure both left AND right are flashed
2. **Try settings reset**: Flash `settings_reset` firmware, then reflash normal firmware
3. **Check battery**: Ensure batteries are charged
4. **Re-pair Bluetooth**: Clear Bluetooth bonds on Layer 2

### Keys Not Responding

1. **Check layer**: Might be stuck on wrong layer (press layer keys to cycle back)
2. **Check connections**: Ensure keyboard switches are properly soldered
3. **Reflash firmware**: Try clean reflash of firmware

---

## Quick Reference Card

### File You'll Actually Edit
- `config/eyelash_sofle.keymap` - Your keyboard layout
- `config/eyelash_sofle.conf` - Feature settings (rarely edited)
- `build.yaml` - What to build (rarely edited)

### Files You Reference
- `byou.json` - Your desired layout reference (QMK format)

### Files Generated Automatically
- `keymap-drawer/*.svg` - Keymap visualization
- Firmware `.uf2` files (downloaded from Actions)

### GitHub Actions Workflows
- **Build**: `.github/workflows/build.yml` - Compiles firmware
- **Draw**: `.github/workflows/draw.yml` - Generates keymap image

### Key Locations
- **Bootloader Access**: Layer 2 → Bottom row
- **Bluetooth Management**: Layer 2 → Top rows
- **Mouse Controls**: Layer 1 → Right side + encoder
- **RGB Controls**: Layer 1 → Bottom row left side

---

## Next Steps

1. **Read**: [BUILD_GUIDE.md](./BUILD_GUIDE.md) - Detailed build instructions
2. **Read**: [KEYMAP_GUIDE.md](./KEYMAP_GUIDE.md) - How to customize your layout
3. **Read**: [QUICK_REFERENCE.md](./QUICK_REFERENCE.md) - Common tasks cheat sheet

---

## Resources

- **ZMK Documentation**: https://zmk.dev/docs
- **ZMK Discord**: https://zmk.dev/community/discord/invite
- **Keymap Editor**: https://nickcoutsos.github.io/keymap-editor/
- **Key Code Reference**: https://zmk.dev/docs/codes
- **Original Board Repo**: https://github.com/a741725193/zmk-sofle

---

**Last Updated**: 2025-11-07
**ZMK Version**: v0.3.0
**Board**: Eyelash Sofle (a741725193)
