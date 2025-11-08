# ZMK Sofle - Keymap Customization Guide

## Table of Contents
1. [Introduction](#introduction)
2. [Understanding the Keymap File](#understanding-the-keymap-file)
3. [Keymap Structure](#keymap-structure)
4. [Key Codes Reference](#key-codes-reference)
5. [Common Modifications](#common-modifications)
6. [Advanced Features](#advanced-features)
7. [Converting from byou.json](#converting-from-byoujson)
8. [Examples](#examples)

---

## Introduction

Your keyboard layout is defined in:
```
config/eyelash_sofle.keymap
```

This file uses **ZMK's keymap syntax** (based on device tree format). It defines:
- **5 layers** (base + 4 additional)
- **Key bindings** for each position
- **Behaviors** (combos, hold-taps, etc.)
- **Encoder actions** per layer

---

## Understanding the Keymap File

### File Overview

```c
config/eyelash_sofle.keymap
├── Preprocessor defines (mouse/scroll speed)
├── Includes (ZMK libraries)
├── Input listeners (mouse/scroll scalers)
├── Behavior configurations
├── Combos (key combinations)
└── Keymap (YOUR LAYOUT)
    ├── Layer 0 (Base)
    ├── Layer 1 (Function/Mouse)
    ├── Layer 2 (System/Bluetooth)
    ├── Layer 3 (Empty)
    └── Layer 4 (Empty)
```

### Key Sections

#### **1. Configuration** (Lines 1-3)
```c
#define ZMK_POINTING_DEFAULT_MOVE_VAL 1200  // Mouse movement speed
#define ZMK_POINTING_DEFAULT_SCRL_VAL 25    // Scroll speed
```

#### **2. Includes** (Lines 4-11)
Standard ZMK libraries - don't modify unless you know what you're doing.

#### **3. Soft Off Settings** (Line 29)
```c
&soft_off { hold-time-ms = <2000>; };  // Deep sleep after 2 seconds
```

#### **4. Combos** (Lines 43-50)
Key combinations that trigger special actions:
```c
softoff {
    bindings = <&soft_off>;
    key-positions = <14 28 40>;  // Q + S + Z = deep sleep
};
```

#### **5. Keymap** (Lines 52-119)
**THIS IS WHERE YOU MAKE CHANGES!**

---

## Keymap Structure

### Layer Anatomy

Each layer has **65 key positions**:

```c
layer0 {
    bindings = <
        // Row 1: Left side (6) + Encoder (1) + Right side (6) = 13 keys
        &kp ESC  &kp N1  &kp N2  &kp N3  &kp N4  &kp N5    &kp UP    &kp N6  &kp N7  &kp N8  &kp N9  &kp N0  &kp BSPC
        
        // Row 2: 13 keys
        &kp TAB  &kp Q   &kp W   &kp E   &kp R   &kp T     &kp DOWN  &kp Y   &kp U   &kp I   &kp O   &kp P   &kp BSLH
        
        // Row 3: 13 keys
        &kp CAPS &kp A   &kp S   &kp D   &kp F   &kp G     &kp LEFT  &kp H   &kp J   &kp K   &kp L   &kp SEMI &kp APOS
        
        // Row 4: 13 keys
        &kp LSHFT &kp Z  &kp X   &kp C   &kp V   &kp B     &kp RIGHT &kp N   &kp M   &kp COMMA &kp DOT &kp FSLH &kp ENTER
        
        // Row 5: Thumb cluster (10 keys)
        &kp C_MUTE &kp LCTRL &kp LGUI &kp LALT &mo 1 &kp SPACE    &kp ENTER &kp SPACE &kp ENTER &mo 2 &kp RSHIFT &kp DEL
    >;
    
    sensor-bindings = <&inc_dec_kp C_VOLUME_UP C_VOL_DN>;
    display-name = "LAYER0";
};
```

### Key Position Map

```
Physical Layout (60 key Sofle):

LEFT HALF:                   ENCODER            RIGHT HALF:
┌───┬───┬───┬───┬───┬───┐   ┌───┐   ┌───┬───┬───┬───┬───┬───┐
│ 0 │ 1 │ 2 │ 3 │ 4 │ 5 │   │ 6 │   │ 7 │ 8 │ 9 │10 │11 │12 │  Row 1
├───┼───┼───┼───┼───┼───┤   └───┘   ├───┼───┼───┼───┼───┼───┤
│13 │14 │15 │16 │17 │18 │           │19 │20 │21 │22 │23 │24 │  Row 2
├───┼───┼───┼───┼───┼───┤   ┌───┐   ├───┼───┼───┼───┼───┼───┤
│25 │26 │27 │28 │29 │30 │   │31 │   │32 │33 │34 │35 │36 │37 │  Row 3
├───┼───┼───┼───┼───┼───┤   └───┘   ├───┼───┼───┼───┼───┼───┤
│38 │39 │40 │41 │42 │43 │           │44 │45 │46 │47 │48 │49 │  Row 4
└───┴───┼───┼───┼───┼───┤   ┌───┐   ├───┼───┼───┼───┼───┴───┘
        │50 │51 │52 │53 │   │54 │   │55 │56 │57 │58 │            Row 5
        ├───┼───┴───┴───┤   └───┘   ├───┴───┴───┼───┤            (Thumb)
        │59 │    60     │           │    61     │62 │
        └───┴───────────┘           └───────────┴───┘
```

Position numbers correspond to the order in your keymap bindings.

---

## Key Codes Reference

### Basic Behavior Syntax

```c
&behavior_name PARAMETER
```

Examples:
- `&kp ESC` - Keypress: ESC key
- `&mo 1` - Momentary layer: Hold for layer 1
- `&trans` - Transparent: Pass through to lower layer
- `&none` - No operation

### Alphabetic Keys

```c
&kp A    &kp B    &kp C    &kp D    &kp E    &kp F    &kp G
&kp H    &kp I    &kp J    &kp K    &kp L    &kp M    &kp N
&kp O    &kp P    &kp Q    &kp R    &kp S    &kp T    &kp U
&kp V    &kp W    &kp X    &kp Y    &kp Z
```

### Number Keys

```c
&kp N1   &kp N2   &kp N3   &kp N4   &kp N5
&kp N6   &kp N7   &kp N8   &kp N9   &kp N0
```

**Note**: Use `N1` not `1` (ZMK syntax)

### Function Keys

```c
&kp F1   &kp F2   &kp F3   &kp F4   &kp F5   &kp F6
&kp F7   &kp F8   &kp F9   &kp F10  &kp F11  &kp F12
```

### Modifiers

```c
&kp LSHIFT   &kp RSHIFT   // Shift
&kp LCTRL    &kp RCTRL    // Control
&kp LALT     &kp RALT     // Alt
&kp LGUI     &kp RGUI     // Windows/Command key
```

### Special Keys

```c
&kp ENTER    &kp SPACE    &kp TAB      &kp BSPC     &kp DEL
&kp ESC      &kp CAPS     &kp INS      &kp HOME     &kp END
&kp PG_UP    &kp PG_DN    &kp PSCRN    &kp PAUSE_BREAK
```

### Symbols

```c
&kp MINUS    // -
&kp EQUAL    // =
&kp LBKT     // [
&kp RBKT     // ]
&kp BSLH     // \
&kp SEMI     // ;
&kp APOS     // '
&kp GRAVE    // `
&kp COMMA    // ,
&kp DOT      // .
&kp FSLH     // /
```

### Shifted Symbols

```c
&kp EXCL     // !
&kp AT       // @
&kp HASH     // #
&kp DLLR     // $
&kp PRCNT    // %
&kp CARET    // ^
&kp AMPS     // &
&kp ASTRK    // *
&kp LPAR     // (
&kp RPAR     // )
&kp UNDER    // _
&kp PLUS     // +
&kp LBRC     // {
&kp RBRC     // }
&kp PIPE     // |
&kp COLON    // :
&kp DQT      // "
&kp TILDE    // ~
&kp LT       // <
&kp GT       // >
&kp QMARK    // ?
```

### Arrow Keys

```c
&kp UP       &kp DOWN     &kp LEFT     &kp RIGHT
&kp UP_ARROW &kp DOWN_ARROW &kp LEFT_ARROW &kp RIGHT_ARROW  // Alternative
```

### Media Keys

```c
&kp C_MUTE       // Mute
&kp C_VOL_UP     // Volume Up
&kp C_VOL_DN     // Volume Down
&kp C_PLAY_PAUSE // Play/Pause (alternative: C_PP)
&kp C_NEXT       // Next Track (alternative: C_NEXT_TRACK)
&kp C_PREV       // Previous Track (alternative: C_PREV_TRACK)
&kp C_BRI_UP     // Brightness Up
&kp C_BRI_DN     // Brightness Down
```

### Navigation

```c
&kp HOME     &kp END      &kp PG_UP    &kp PG_DN
&kp INS      &kp DEL      &kp BSPC     &kp ENTER
```

---

## Layer Behaviors

### Momentary Layer

```c
&mo 1        // Hold: activate layer 1, release: back to base
&mo 2        // Hold: activate layer 2
```

### Toggle Layer

```c
&to 1        // Switch to layer 1 (stays there)
&to 0        // Back to base layer
```

### Layer-Tap

```c
&lt 1 SPACE  // Tap: space, hold: layer 1
&lt 2 ENTER  // Tap: enter, hold: layer 2
```

### Transparent & None

```c
&trans       // Pass through to layer below
&none        // Do nothing (no key action)
```

---

## Mouse Controls

### Mouse Movement

```c
&mmv MOVE_UP      // Move cursor up
&mmv MOVE_DOWN    // Move cursor down
&mmv MOVE_LEFT    // Move cursor left
&mmv MOVE_RIGHT   // Move cursor right
```

### Mouse Buttons

```c
&mkp LCLK         // Left click
&mkp RCLK         // Right click
&mkp MCLK         // Middle click
&mkp MB4          // Mouse button 4 (back)
&mkp MB5          // Mouse button 5 (forward)
```

### Mouse Scroll

```c
&msc SCRL_UP      // Scroll up
&msc SCRL_DOWN    // Scroll down
&msc SCRL_LEFT    // Scroll left
&msc SCRL_RIGHT   // Scroll right
```

---

## Bluetooth Controls

### Profile Selection

```c
&bt BT_SEL 0      // Select profile 0
&bt BT_SEL 1      // Select profile 1
&bt BT_SEL 2      // Select profile 2
&bt BT_SEL 3      // Select profile 3
&bt BT_SEL 4      // Select profile 4
```

### Clear Bonds

```c
&bt BT_CLR        // Clear current profile
&bt BT_CLR_ALL    // Clear all profiles
```

### Output Selection

```c
&out OUT_BLE      // Force Bluetooth output
&out OUT_USB      // Force USB output
&out OUT_TOG      // Toggle between BLE and USB
```

---

## RGB Controls

```c
&rgb_ug RGB_ON       // Turn RGB on
&rgb_ug RGB_OFF      // Turn RGB off
&rgb_ug RGB_TOG      // Toggle RGB
&rgb_ug RGB_BRI      // Increase brightness
&rgb_ug RGB_BRD      // Decrease brightness
&rgb_ug RGB_EFF      // Next effect
&rgb_ug RGB_EFR      // Previous effect
&rgb_ug RGB_HUI      // Increase hue
&rgb_ug RGB_HUD      // Decrease hue
&rgb_ug RGB_SAI      // Increase saturation
&rgb_ug RGB_SAD      // Decrease saturation
&rgb_ug RGB_SPI      // Increase speed
&rgb_ug RGB_SPD      // Decrease speed
```

---

## System Controls

```c
&sys_reset        // Soft reset keyboard
&bootloader       // Enter bootloader (for flashing)
&soft_off         // Enter deep sleep mode
```

---

## Common Modifications

### Example 1: Change Base Layer Key

**Change Q key to A:**

```c
// Before (Line 58 in layer0):
&kp Q

// After:
&kp A
```

### Example 2: Add Function Key

**Make right Shift into F13:**

```c
// Before (Line 61):
&kp RSHIFT

// After:
&kp F13
```

### Example 3: Create Layer Toggle

**Make Caps Lock a layer toggle:**

```c
// Before (Line 59):
&kp CAPS

// After (hold Caps for layer 1, tap for Caps):
&lt 1 CAPS
```

### Example 4: Add Media Keys

**Replace number keys with media controls:**

```c
// Before:
&kp N1  &kp N2  &kp N3  &kp N4  &kp N5

// After:
&kp C_PREV  &kp C_PLAY_PAUSE  &kp C_NEXT  &kp C_MUTE  &kp C_VOL_UP
```

### Example 5: Swap Modifiers

**Swap Ctrl and Alt:**

```c
// Before:
&kp LCTRL  &kp LGUI  &kp LALT

// After:
&kp LALT   &kp LGUI  &kp LCTRL
```

---

## Advanced Features

### Hold-Tap Behaviors

**Custom behavior: tap for key, hold for modifier**

```c
// In behaviors section (line 40):
behaviors {
    hm: homerow_mods {
        compatible = "zmk,behavior-hold-tap";
        #binding-cells = <2>;
        tapping-term-ms = <200>;
        quick-tap-ms = <0>;
        flavor = "tap-preferred";
        bindings = <&kp>, <&kp>;
    };
};

// Usage in keymap:
&hm LSHIFT A   // Tap: A, hold: Shift
```

### Combos

**Press multiple keys simultaneously for action**

```c
// In combos section:
combos {
    compatible = "zmk,combos";
    
    // ESC combo (J + K together)
    combo_esc {
        bindings = <&kp ESC>;
        key-positions = <33 34>;  // J and K positions
        timeout-ms = <50>;
    };
    
    // Delete combo (O + P together)
    combo_del {
        bindings = <&kp DEL>;
        key-positions = <22 23>;  // O and P positions
    };
};
```

### Macros

**Record sequence of keypresses**

```c
// Define macro
macros {
    email: email {
        compatible = "zmk,behavior-macro";
        #binding-cells = <0>;
        bindings = <&kp Y &kp O &kp U &kp AT &kp E &kp X &kp A &kp M &kp P &kp L &kp E &kp DOT &kp C &kp O &kp M>;
    };
};

// Use in keymap:
&email   // Types: you@example.com
```

### Encoder Configuration

**Change encoder behavior per layer:**

```c
layer1 {
    // ... bindings ...
    
    sensor-bindings = <&inc_dec_kp PG_UP PG_DN>;  // Page up/down
};

layer2 {
    sensor-bindings = <&scroll_encoder>;  // Scroll wheel
};
```

---

## Converting from byou.json

Your `byou.json` file is in **QMK format**. Here's how to convert it to ZMK:

### Step 1: Understand QMK vs ZMK Differences

| QMK Code | ZMK Code | Description |
|----------|----------|-------------|
| `KC_ESC` | `ESC` | Escape key |
| `KC_1` | `N1` | Number 1 |
| `KC_TAB` | `TAB` | Tab key |
| `KC_LSFT` | `LSHIFT` | Left Shift |
| `KC_LCTL` | `LCTRL` | Left Control |
| `KC_LGUI` | `LGUI` | Left GUI/Win |
| `KC_BSPC` | `BSPC` | Backspace |
| `KC_DEL` | `DEL` | Delete |
| `KC_ENT` | `ENTER` | Enter |
| `KC_NO` | `&none` | No action |
| `KC_TRNS` | `&trans` | Transparent |
| `MO(1)` | `&mo 1` | Momentary layer |
| `TL_LOWR` | `&mo 1` | Lower layer |
| `TL_UPPR` | `&mo 2` | Upper layer |
| `KC_VOLD` | `C_VOL_DN` | Volume down |
| `KC_VOLU` | `C_VOL_UP` | Volume up |
| `KC_MUTE` | `C_MUTE` | Mute |

### Step 2: Map QMK Layer to ZMK

**QMK Layer 0 (from byou.json lines 9-70):**

```json
"KC_ESC", "KC_1", "KC_2", "KC_3", ...
```

**Converts to ZMK:**

```c
layer0 {
    bindings = <
        &kp ESC  &kp N1  &kp N2  &kp N3  ...
    >;
};
```

### Step 3: Convert Full Layout

Example conversion from byou.json Layer 1 (lines 72-132):

**QMK JSON:**
```json
["KC_GRV", "KC_1", "KC_2", "KC_3", "KC_4", "KC_5", ...]
```

**ZMK Keymap:**
```c
layer1 {
    bindings = <
        &kp GRAVE  &kp N1  &kp N2  &kp N3  &kp N4  &kp N5  ...
    >;
};
```

### Step 4: Handle Special Cases

**QMK Tap Dance / Layer-Tap:**
```json
"ANY(TL_LOWR)"  // QMK custom
```

**ZMK Equivalent:**
```c
&mo 1           // Simple momentary layer
&lt 1 SPACE     // Layer-tap (if tap functionality needed)
```

---

## Examples

### Example Layout: Colemak DH

```c
layer0 {
    bindings = <
&kp ESC    &kp N1  &kp N2  &kp N3  &kp N4  &kp N5    &kp UP    &kp N6  &kp N7  &kp N8  &kp N9    &kp N0    &kp BSPC
&kp TAB    &kp Q   &kp W   &kp F   &kp P   &kp B     &kp DOWN  &kp J   &kp L   &kp U   &kp Y     &kp SEMI  &kp BSLH
&kp CAPS   &kp A   &kp R   &kp S   &kp T   &kp G     &kp LEFT  &kp M   &kp N   &kp E   &kp I     &kp O     &kp APOS
&kp LSHFT  &kp Z   &kp X   &kp C   &kp D   &kp V     &kp RIGHT &kp K   &kp H   &kp COMMA &kp DOT &kp FSLH  &kp ENTER
&kp C_MUTE &kp LCTRL &kp LGUI &kp LALT &mo 1 &kp SPACE    &kp ENTER &kp SPACE &kp ENTER &mo 2 &kp RSHIFT &kp DEL
    >;
    
    sensor-bindings = <&inc_dec_kp C_VOL_UP C_VOL_DN>;
    display-name = "Colemak";
};
```

### Example Layer: Developer Layer

```c
layer_dev {
    bindings = <
&kp GRAVE  &kp F1    &kp F2    &kp F3    &kp F4    &kp F5      &trans  &kp F6    &kp F7    &kp F8     &kp F9     &kp F10   &kp F11
&trans     &kp EXCL  &kp AT    &kp HASH  &kp DLLR  &kp PRCNT   &trans  &kp CARET &kp AMPS  &kp ASTRK  &kp LPAR   &kp RPAR  &kp F12
&trans     &kp N1    &kp N2    &kp N3    &kp N4    &kp N5      &trans  &kp N6    &kp N7    &kp N8     &kp N9     &kp N0    &trans
&trans     &kp MINUS &kp EQUAL &kp LBKT  &kp RBKT  &kp BSLH    &trans  &kp GRAVE &kp UNDER &kp PLUS   &kp LBRC   &kp RBRC  &kp PIPE
&trans     &trans    &trans    &trans    &trans    &trans      &trans  &trans    &trans    &trans     &trans     &trans
    >;
    
    display-name = "Dev";
};
```

### Example Layer: Gaming Layer

```c
layer_game {
    bindings = <
&kp ESC    &kp N1   &kp N2   &kp N3   &kp N4   &kp N5     &trans  &kp N6   &kp N7   &kp N8   &kp N9   &kp N0   &kp BSPC
&kp TAB    &kp Q    &kp W    &kp E    &kp R    &kp T      &trans  &kp Y    &kp U    &kp I    &kp O    &kp P    &kp ENTER
&kp LSHIFT &kp A    &kp S    &kp D    &kp F    &kp G      &trans  &kp H    &kp J    &kp K    &kp L    &kp SEMI &kp APOS
&kp LCTRL  &kp Z    &kp X    &kp C    &kp V    &kp B      &trans  &kp N    &kp M    &kp COMMA &kp DOT &kp FSLH &kp RSHIFT
&kp LALT   &kp N1   &kp N2   &kp N3   &kp SPACE &kp SPACE &trans  &kp SPACE &mo 2   &trans   &trans   &trans
    >;
    
    display-name = "Game";
};
```

---

## Validation & Testing

### Before Committing

1. **Check syntax**: Ensure all lines end with `;`
2. **Count keys**: Each layer should have 65 bindings
3. **Match brackets**: `<` and `>` must be paired
4. **Valid codes**: Use correct ZMK key codes

### Test Process

1. **Edit** `config/eyelash_sofle.keymap`
2. **Commit and push** to GitHub
3. **Monitor build** in GitHub Actions
4. **Download firmware** if build succeeds
5. **Flash** to keyboard
6. **Test layout** thoroughly

### Common Errors

**Build Error: "Expected ')'"**
```
Missing semicolon at end of line
```
**Fix**: Add `;` at line end

**Build Error: "Undeclared identifier"**
```
Invalid key code like &kp INVALID_KEY
```
**Fix**: Use valid ZMK key code

**Keyboard doesn't respond correctly**
```
Wrong number of keys in layer
```
**Fix**: Ensure exactly 65 bindings per layer

---

## Quick Reference

### Editing Workflow

```bash
# 1. Open keymap file
code "G:\Sofle Keyboard\zmk-sofle-1\config\eyelash_sofle.keymap"

# 2. Make changes

# 3. Commit and push
cmd /c cd /d "G:\Sofle Keyboard\zmk-sofle-1"
cmd /c git add config/eyelash_sofle.keymap
cmd /c git commit -m "Update keymap: describe changes"
cmd /c git push

# 4. Wait for build
# 5. Download and flash firmware
```

### Key Code Quick Lookup

- **Letters**: `&kp A` to `&kp Z`
- **Numbers**: `&kp N1` to `&kp N0`
- **Functions**: `&kp F1` to `&kp F12`
- **Modifiers**: `&kp LSHIFT`, `&kp LCTRL`, `&kp LALT`, `&kp LGUI`
- **Layer**: `&mo 1` (hold), `&to 1` (toggle), `&lt 1 SPACE` (layer-tap)
- **Special**: `&trans` (pass-through), `&none` (no action)

---

## Resources

- **ZMK Key Codes**: https://zmk.dev/docs/codes
- **ZMK Behaviors**: https://zmk.dev/docs/behaviors/key-press
- **Keymap Editor** (GUI): https://nickcoutsos.github.io/keymap-editor/
- **ZMK Discord**: https://zmk.dev/community/discord/invite

---

**Next Steps**:
- Experiment with layers 3 and 4 (currently empty)
- Add custom combos for frequent actions
- Create macros for repetitive text
- Check out [QUICK_REFERENCE.md](./QUICK_REFERENCE.md) for shortcuts

---

**Last Updated**: 2025-11-07
**ZMK Version**: v0.3.0
