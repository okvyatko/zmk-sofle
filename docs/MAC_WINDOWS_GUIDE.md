# Mac & Windows Dual-OS Keyboard Guide

## Overview

Your keyboard now supports both Windows and Mac with dedicated layouts and features for each OS. This guide explains all the new functionality.

---

## Key Changes Summary

### Layer 0 (Windows Base)
- **Top-right key**: Changed from `BACKSPACE` to `DELETE`
- **First thumb key**: Added `BACKSPACE` for easy access
- Layout optimized for Windows/PC usage

### Layer 1 (Windows Function Layer)
- **Joystick/Nav cluster**: Now snaps windows
  - Up: Maximize window (Win+Up)
  - Down: Restore/Minimize (Win+Down)
  - Left: Snap window left (Win+Left)
  - Right: Snap window right (Win+Right)
- **Left home row**: Common macros
  - B→A: Select All (Ctrl+A)
  - Y→A: Copy (Ctrl+C)
  - O→A: Paste (Ctrl+V)
  - U→A: Cut (Ctrl+X)
  - '→A: Undo (Ctrl+Z)
- **Bottom-right corner**: `to 3` - Switch to Mac mode

### Layer 3 (Mac Base)
- Same letter layout as Layer 0
- **Key differences**:
  - Right-hand modifiers: `CMD` instead of `RGUI`
  - Optimized for macOS shortcuts
- Access Layer 4 (Mac function layer) via left thumb FN key

### Layer 4 (Mac Function Layer)
- **Joystick/Nav cluster**: Mac window snapping (Rectangle/Magnet style)
  - Up: Maximize window (Ctrl+Opt+Up)
  - Down: Restore (Ctrl+Opt+Down)
  - Left: Snap window left (Ctrl+Opt+Left)
  - Right: Snap window right (Ctrl+Opt+Right)
- **Left home row**: Mac macros
  - B→A: Select All (Cmd+A)
  - Y→A: Copy (Cmd+C)
  - O→A: Paste (Cmd+V)
  - U→A: Cut (Cmd+X)
  - '→A: Undo (Cmd+Z)
- **Bottom-right corner**: `to 0` - Switch back to Windows mode

---

## How to Use

### Switching Between Windows and Mac Modes

#### To Mac Mode:
1. Hold left thumb FN key (activates Layer 1)
2. Press the bottom-right key (was `&trans`, now `to 3`)
3. You're now on Layer 3 (Mac base layer)

#### Back to Windows Mode:
1. Hold left thumb FN key (activates Layer 4 from Layer 3)
2. Press the bottom-right key (`to 0`)
3. You're back on Layer 0 (Windows base layer)

### Window Snapping

#### Windows (Layer 1):
1. Hold left thumb FN key
2. Use nav cluster:
   - Up arrow: Maximize
   - Down arrow: Restore/Minimize
   - Left arrow: Snap left half
   - Right arrow: Snap right half

#### Mac (Layer 4):
**Prerequisites**: Install [Rectangle](https://rectangleapp.com/) or [Magnet](https://magnet.crowdcafe.com/) for window management

1. Hold left thumb FN key (from Layer 3)
2. Use nav cluster:
   - Up arrow: Maximize (Ctrl+Opt+Up)
   - Down arrow: Restore (Ctrl+Opt+Down)
   - Left arrow: Snap left (Ctrl+Opt+Left)
   - Right arrow: Snap right (Ctrl+Opt+Right)

**Note**: Configure Rectangle/Magnet to use `Ctrl+Option+Arrow` shortcuts to match the keyboard layout.

### Common Macros

Both Windows (Layer 1) and Mac (Layer 4) have the same macro key positions on the left home row:

```
Position on Layer 1/4:
┌─────────────────────────────────┐
│ Grave│ F1 │ F2 │ F3 │ F4 │ F5  │
├──────┼────┼────┼────┼────┼─────┤
│ Trans│SEL │COPY│PSTE│CUT │UNDO │  ← These keys!
└──────┴────┴────┴────┴────┴─────┘
```

**Windows shortcuts** (Layer 1):
- **Select All**: Ctrl+A
- **Copy**: Ctrl+C
- **Paste**: Ctrl+V
- **Cut**: Ctrl+X
- **Undo**: Ctrl+Z

**Mac shortcuts** (Layer 4):
- **Select All**: Cmd+A
- **Copy**: Cmd+C
- **Paste**: Cmd+V
- **Cut**: Cmd+X
- **Undo**: Cmd+Z

---

## Layout Recommendations

### Current Layout Analysis

**What works well**:
- Custom letter arrangement (BYOU layout)
- Nav cluster for arrows
- Layer access is intuitive

**Considerations**:

#### Second Space Key
You currently have `SPACE` on both the left and right thumb clusters. Options:
1. **Keep both**: Good for typing comfort, can press with either hand
2. **Replace right space**: Could become `BACKSPACE` or `ENTER` for symmetry
3. **Current recommendation**: Keep both - having space accessible from either hand reduces hand movement

#### Backspace vs Delete Placement
- **Top-right**: Now `DELETE` (as requested)
- **First thumb**: Now `BACKSPACE` (easy to reach)
- This gives you quick access to both without needing function layers

#### Missing Keys You Might Need

**On Mac**:
- **Spotlight Search** (Cmd+Space): Consider adding to Layer 4
- **Mission Control** (Ctrl+Up): Already covered by nav cluster
- **Screenshot** (Cmd+Shift+4): Could add as macro

**On Windows**:
- **Task View** (Win+Tab): Could add to Layer 1
- **Virtual Desktop switching** (Win+Ctrl+Left/Right): Could add

---

## Advanced Customization

### Adding More Macros

The keyboard supports additional macros. Here are some useful ones to consider:

#### Windows:
```c
// Task View
win_task_view: win_task_view {
    compatible = "zmk,behavior-macro";
    #binding-cells = <0>;
    bindings = <&kp LG(TAB)>;
};

// Virtual Desktop Left
win_desk_left: win_desk_left {
    compatible = "zmk,behavior-macro";
    #binding-cells = <0>;
    bindings = <&kp LG(LC(LEFT))>;
};

// Virtual Desktop Right
win_desk_right: win_desk_right {
    compatible = "zmk,behavior-macro";
    #binding-cells = <0>;
    bindings = <&kp LG(LC(RIGHT))>;
};
```

#### Mac:
```c
// Spotlight
mac_spotlight: mac_spotlight {
    compatible = "zmk,behavior-macro";
    #binding-cells = <0>;
    bindings = <&kp LG(SPACE)>;
};

// Screenshot area
mac_screenshot: mac_screenshot {
    compatible = "zmk,behavior-macro";
    #binding-cells = <0>;
    bindings = <&kp LG(LS(N4))>;
};

// Mission Control
mac_mission: mac_mission {
    compatible = "zmk,behavior-macro";
    #binding-cells = <0>;
    bindings = <&kp LC(UP)>;
};
```

### Profile-Based Switching (Future)

While ZMK doesn't have automatic OS detection, you could:
1. **Use Bluetooth profiles**: Dedicate profiles 0-2 for PC, 3-4 for Mac
2. **Visual indicators**: Use RGB underglow colors to show which mode you're in
3. **Sticky mode**: Once you switch to Mac mode (Layer 3), it stays until you explicitly switch back

---

## Troubleshooting

### Window Snapping Not Working

**Windows**: Should work out of the box with Win+Arrow shortcuts

**Mac**: 
1. Install Rectangle or Magnet
2. Configure shortcuts to match:
   - Left Half: Ctrl+Option+Left
   - Right Half: Ctrl+Option+Right
   - Maximize: Ctrl+Option+Up
   - Restore: Ctrl+Option+Down

### Macros Not Working
- Ensure firmware is flashed to both halves
- Check that you're on the correct layer (1 for Windows, 4 for Mac)
- Verify the application you're using supports the shortcuts

### Can't Switch Back to Windows Mode
- From Mac mode (Layer 3), hold left FN → press bottom-right key
- If stuck, Layer 2 is still accessible and has system reset options

---

## Quick Reference

### Layer Map

```
Layer 0: Windows Base (default)
  ├─ Layer 1: Windows Function + Macros (FN key)
  └─ Layer 2: System/Bluetooth (right FN key)

Layer 3: Mac Base (toggle from Layer 1)
  ├─ Layer 4: Mac Function + Macros (FN key)
  └─ Layer 2: System/Bluetooth (right FN key)
```

### Key Combos

| Action | From Layer | Keys |
|--------|-----------|------|
| Switch to Mac | 1 (Windows FN) | FN + F12 (bottom-right) |
| Switch to Windows | 4 (Mac FN) | FN + F12 (bottom-right) |
| Window snap left | 1 or 4 | FN + Left arrow |
| Window snap right | 1 or 4 | FN + Right arrow |
| Select all + paste | 1 or 4 | FN + A, release FN, FN + Paste |

---

## Next Steps

1. **Build the firmware** via GitHub Actions
2. **Flash both halves** (right first, then left)
3. **Test on Windows**: Try window snapping and macros
4. **Install Rectangle on Mac** if you use macOS
5. **Test mode switching**: Switch between Windows and Mac modes
6. **Customize further**: Add your own macros or adjust key positions

---

## Technical Notes

### Macro Implementation
All macros are defined in the `behaviors` section using `zmk,behavior-macro`. They execute key combinations atomically, ensuring reliable shortcuts.

### Layer Toggling
- `&mo X`: Momentary layer (active while held)
- `&to X`: Toggle to layer (stays until switched)

Layer 0 and Layer 3 are "base" layers you toggle between. Layers 1, 2, and 4 are accessed momentarily with FN keys.

### Modifier Keys
- Windows uses `LGUI`/`RGUI` (Windows key)
- Mac uses `LCMD`/`RCMD` (Command key)
- ZMK translates these appropriately per OS

---

**Last Updated**: 2025-11-09  
**ZMK Version**: v0.3.0
