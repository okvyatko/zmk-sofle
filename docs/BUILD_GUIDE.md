# ZMK Sofle - Build & Flash Guide

## Table of Contents
1. [Prerequisites](#prerequisites)
2. [Building Firmware](#building-firmware)
3. [Understanding Build Outputs](#understanding-build-outputs)
4. [Flashing Firmware](#flashing-firmware)
5. [Testing & Verification](#testing--verification)
6. [Troubleshooting](#troubleshooting)

---

## Prerequisites

### What You Need

✅ **Completed**:
- [x] Forked this repository to your GitHub account
- [x] ZMK firmware configuration in place

⚙️ **Required**:
- [ ] GitHub account with Actions enabled
- [ ] USB cable to connect keyboard to computer
- [ ] Both keyboard halves (left and right)
- [ ] Batteries installed (if wireless)

💡 **Optional**:
- Git installed on your computer (for local editing)
- Text editor (VS Code, Notepad++, etc.)

---

## Building Firmware

### Option 1: GitHub Actions (Recommended)

This is the **easiest method** - no local tools required!

#### Step 1: Navigate to GitHub Actions

```
https://github.com/YOUR_USERNAME/zmk-sofle-1/actions
```

Replace `YOUR_USERNAME` with your GitHub username.

#### Step 2: Select Build Workflow

- In the left sidebar, click **"Build ZMK firmware"**

#### Step 3: Trigger Build

**Option A: Manual Trigger**
1. Click the **"Run workflow"** button (top right, dropdown)
2. Ensure the correct branch is selected (usually `main`)
3. Click the green **"Run workflow"** button

**Option B: Automatic Trigger (Push)**
- Simply push changes to your repository:
  ```bash
  cmd /c cd /d "G:\Sofle Keyboard\zmk-sofle-1"
  cmd /c git add .
  cmd /c git commit -m "Update keymap"
  cmd /c git push
  ```
- Build starts automatically within seconds

#### Step 4: Monitor Build Progress

1. Click on the running workflow in the list
2. Click on the **"build"** job to see live logs
3. Build typically takes **5-10 minutes**

**Build Status Indicators**:
- 🟡 Yellow circle = Running
- ✅ Green checkmark = Success
- ❌ Red X = Failed (check logs for errors)

#### Step 5: Download Firmware

Once the build succeeds:

1. Scroll to the bottom of the workflow run page
2. Find the **"Artifacts"** section
3. Click the **firmware** link to download a ZIP file
4. Extract the ZIP file

You'll find these files:
- `eyelash_sofle_left-nice_view-zmk.uf2`
- `eyelash_sofle_right-nice_view-zmk.uf2`
- `eyelash_sofle_studio_left-nice_view-zmk.uf2` (optional)
- `settings_reset-nice_nano_v2-zmk.uf2` (utility)

---

### Option 2: Local Build (Advanced)

**⚠️ Not Recommended for Beginners** - Use GitHub Actions instead unless you need offline builds.

<details>
<summary>Click to expand local build instructions</summary>

#### Prerequisites
- Windows WSL2 or Linux
- Python 3
- West build tool
- ARM GCC toolchain
- Multiple GB of disk space

#### Steps

1. **Install dependencies**:
   ```bash
   # Install west
   pip3 install west
   
   # Install ARM GCC toolchain
   # (Instructions vary by OS - see ZMK docs)
   ```

2. **Initialize workspace**:
   ```bash
   west init -l config/
   west update
   ```

3. **Build firmware**:
   ```bash
   # Build left half
   west build -p -b eyelash_sofle_left -- -DSHIELD=nice_view
   
   # Build right half
   west build -p -b eyelash_sofle_right -- -DSHIELD=nice_view
   ```

4. **Find compiled firmware**:
   ```
   build/zephyr/zmk.uf2
   ```

**Note**: Local builds require significant setup. GitHub Actions is much simpler.

</details>

---

## Understanding Build Outputs

### What Gets Built (build.yaml)

```yaml
include:
  # RIGHT HALF (Standard)
  - board: eyelash_sofle_right
    shield: nice_view
  
  # LEFT HALF (Standard)
  - board: eyelash_sofle_left
    shield: nice_view
  
  # LEFT HALF (ZMK Studio - Live Editing)
  - board: eyelash_sofle_left
    shield: nice_view
    snippet: studio-rpc-usb-uart
    cmake-args: -DCONFIG_ZMK_STUDIO=y
    artifact-name: eyelash_sofle_studio_left
  
  # UTILITY: Settings Reset
  - board: nice_nano_v2
    shield: settings_reset
```

### Firmware Files Explained

| File | Purpose | When to Use |
|------|---------|-------------|
| `eyelash_sofle_left-nice_view-zmk.uf2` | **Standard left half** | Regular use |
| `eyelash_sofle_right-nice_view-zmk.uf2` | **Standard right half** | Regular use (flash first!) |
| `eyelash_sofle_studio_left-nice_view-zmk.uf2` | **Studio-enabled left** | For live keymap editing |
| `settings_reset-nice_nano_v2-zmk.uf2` | **Reset utility** | When keyboard behaves strangely |

### Build Artifacts Structure

After extraction:
```
firmware/
├── eyelash_sofle_left-nice_view-zmk.uf2
├── eyelash_sofle_right-nice_view-zmk.uf2
├── eyelash_sofle_studio_left-nice_view-zmk.uf2
└── settings_reset-nice_nano_v2-zmk.uf2
```

---

## Flashing Firmware

### ⚠️ Important: Flash Order

**ALWAYS flash the RIGHT half first, then the LEFT half!**

This ensures proper Bluetooth pairing.

### Step-by-Step Flashing Process

#### **1. Enter Bootloader Mode**

Choose one method:

**Method A: Reset Button (Recommended)**
1. Locate the **reset button** on your keyboard PCB
2. **Double-press** the button quickly (within 1 second)
3. Keyboard should appear as a USB drive

**Method B: Bootloader Key Combo**
1. Access **Layer 2** (hold layer key)
2. Press the **bootloader** key (check your keymap)
3. Keyboard enters bootloader mode

**Method C: Physical Reset**
1. Short the **RST** and **GND** pins twice quickly
2. Only if you have exposed pins

#### **2. Verify Bootloader Mode**

When successful, you'll see:
- 💾 **New USB drive** appears (named "NICENANO" or similar)
- 🔵 LED on keyboard may blink or change color
- **File explorer** shows the drive with some files

#### **3. Flash RIGHT Half First**

1. **Connect RIGHT keyboard half** to computer via USB
2. **Enter bootloader** using one of the methods above
3. **Drag and drop** `eyelash_sofle_right-nice_view-zmk.uf2` onto the drive
   - OR **copy/paste** the file to the drive
4. **Wait 2-5 seconds** - drive will disconnect automatically
5. ✅ **RIGHT half is now flashed!**

**⏱️ Wait 30 seconds** before proceeding.

#### **4. Flash LEFT Half Second**

1. **Disconnect RIGHT half**
2. **Connect LEFT keyboard half** to computer via USB
3. **Enter bootloader** mode
4. **Drag and drop** `eyelash_sofle_left-nice_view-zmk.uf2` onto the drive
5. **Wait 2-5 seconds** - drive will disconnect automatically
6. ✅ **LEFT half is now flashed!**

#### **5. Optional: Flash Studio Left**

For ZMK Studio support (live editing):

1. **Connect LEFT half** only
2. **Enter bootloader** mode
3. **Drag and drop** `eyelash_sofle_studio_left-nice_view-zmk.uf2`
4. Done! You can now use ZMK Studio

**Note**: Studio version replaces standard left firmware.

---

## Testing & Verification

### Initial Power-On

After flashing both halves:

1. **Disconnect USB** from both halves
2. **Turn on both halves** (power switches)
3. **Wait 10 seconds** for Bluetooth pairing
4. **Test a few keys** - they should work!

### Bluetooth Pairing

#### **To Computer (First Time)**

1. **On keyboard**: Press Layer 2 keys to access Bluetooth layer
2. **Select profile**: Press BT_SEL 0 key (profile 0)
3. **On computer**: 
   - Open Bluetooth settings
   - Look for "Sofle" or similar device name
   - Click "Connect" or "Pair"
4. **Test typing** - should work wirelessly now!

#### **Additional Profiles**

You can pair up to **5 devices**:

- Profile 0: `BT_SEL 0` (Layer 2)
- Profile 1: `BT_SEL 1` (Layer 2)
- Profile 2: `BT_SEL 2` (Layer 2)
- Profile 3: `BT_SEL 3` (Layer 2)
- Profile 4: `BT_SEL 4` (Layer 2)

**Switch between devices**: Just press the corresponding `BT_SEL` key.

### Testing Checklist

- [ ] Both halves power on
- [ ] Keys respond on both halves
- [ ] Layers switch correctly
- [ ] Encoder turns and registers inputs
- [ ] OLED displays show information
- [ ] RGB underglow works (if enabled)
- [ ] Bluetooth connects to computer
- [ ] Special keys work (media, function keys, etc.)

### Keymap Visualization

After changes, check the generated visualization:
```
keymap-drawer/eyelash_sofle.svg
```

Open this in a browser to see your layout visually.

---

## Troubleshooting

### Build Issues

#### **Build Fails with Syntax Error**

**Problem**: Error in `.keymap` file
```
ERROR: Syntax error at line 57
```

**Solution**:
1. Open `config/eyelash_sofle.keymap`
2. Check line mentioned in error
3. Common issues:
   - Missing semicolon `;`
   - Missing comma `,`
   - Incorrect key code (e.g., `&kp INVALID`)
   - Mismatched brackets `< >`

#### **Build Fails: Invalid Key Code**

**Problem**: Using non-existent key code

**Solution**:
- Check [ZMK key codes documentation](https://zmk.dev/docs/codes)
- Common mistakes:
  - `KC_ESC` (QMK) → Use `ESC` (ZMK)
  - `LSFT` → Use `LSHIFT`

#### **GitHub Actions Disabled**

**Problem**: Workflows don't appear

**Solution**:
1. Go to repository Settings
2. Click "Actions" → "General"
3. Enable "Allow all actions"
4. Save

---

### Flashing Issues

#### **Keyboard Doesn't Enter Bootloader**

**Problem**: No USB drive appears

**Solutions**:
1. **Try different USB cable** - some cables are charge-only
2. **Double-press faster** - reset timing is critical
3. **Try different USB port**
4. **Check battery** - ensure it's connected and charged
5. **Manual reset**: Short RST to GND twice

#### **Drive Appears but Flash Fails**

**Problem**: File copies but keyboard doesn't work

**Solutions**:
1. **Verify file**: Ensure you copied the correct `.uf2` file
2. **Don't rename**: Keep original filename
3. **Complete copy**: Wait for copy to finish before unplugging
4. **Try settings reset**: Flash `settings_reset` firmware, then reflash

#### **Only One Half Works**

**Problem**: One side works, other doesn't

**Solutions**:
1. **Reflash non-working side**
2. **Flash RIGHT first, then LEFT** (correct order)
3. **Wait between flashes** (30 seconds)
4. **Check connections**: Ensure USB connection is solid

---

### Keyboard Behavior Issues

#### **Keys Not Responding**

**Problem**: Some or all keys don't work

**Solutions**:
1. **Check layer**: You might be on wrong layer
   - Press layer keys to cycle through
   - Reset to base layer
2. **Reflash firmware**: Flash both halves again
3. **Settings reset**: Use settings reset utility
4. **Hardware check**: Verify switches are properly soldered

#### **Bluetooth Won't Pair**

**Problem**: Computer doesn't see keyboard

**Solutions**:
1. **Clear Bluetooth bonds**:
   - Press `BT_CLR` key on Layer 2
   - Try pairing again
2. **Clear all bonds**:
   - Press `BT_CLR_ALL` key on Layer 2
   - Unpair from computer Bluetooth settings
   - Repair from scratch
3. **Check profile**: Ensure you're on correct profile (BT_SEL 0-4)
4. **Reflash**: Sometimes a reflash fixes BT issues

#### **Halves Not Communicating**

**Problem**: Only one half works at a time

**Solutions**:
1. **Reflash in correct order**: RIGHT first, then LEFT
2. **Wait longer**: Give 30 seconds after each flash
3. **Power cycle**: Turn both halves off, then on again
4. **Settings reset**: Flash reset utility on both halves

#### **Random Key Presses / Chattering**

**Problem**: Keys register multiple times

**Solutions**:
1. **Adjust debounce** in `eyelash_sofle.conf`:
   ```
   CONFIG_ZMK_KSCAN_DEBOUNCE_PRESS_MS=10
   CONFIG_ZMK_KSCAN_DEBOUNCE_RELEASE_MS=10
   ```
2. **Check switches**: Might be faulty switch
3. **Clean contacts**: Debris can cause issues

---

## Advanced: Settings Reset

### When to Use Settings Reset

Use when:
- Keyboard behaves erratically
- Bluetooth pairing issues persist
- After major firmware changes
- "Factory reset" needed

### How to Reset Settings

1. **Flash reset utility**:
   - Enter bootloader on LEFT half
   - Flash `settings_reset-nice_nano_v2-zmk.uf2`
   - Wait for completion

2. **Immediately reflash normal firmware**:
   - Enter bootloader again
   - Flash standard firmware
   - Done!

3. **Repeat for RIGHT half** if needed

**⚠️ Warning**: This clears ALL saved settings:
- Bluetooth pairings
- Layer states
- Any saved configurations

---

## Command Reference

### Using cmd /c (Windows)

When running commands on Windows, use `cmd /c` prefix:

```bash
# Navigate to repository
cmd /c cd /d "G:\Sofle Keyboard\zmk-sofle-1"

# Check git status
cmd /c git status

# Add files
cmd /c git add config/eyelash_sofle.keymap

# Commit changes
cmd /c git commit -m "Update keymap: change layer 1 layout"

# Push to GitHub (triggers build)
cmd /c git push
```

### Git Workflow

```bash
# 1. Make changes to keymap
# Edit: config/eyelash_sofle.keymap

# 2. Stage changes
cmd /c cd /d "G:\Sofle Keyboard\zmk-sofle-1"
cmd /c git add config/

# 3. Commit with descriptive message
cmd /c git commit -m "Add mouse layer with custom bindings"

# 4. Push to trigger build
cmd /c git push origin main

# 5. Wait for GitHub Actions to complete
# 6. Download firmware from Actions artifacts
# 7. Flash to keyboard
```

---

## Quick Flash Checklist

```
Pre-Flight:
[ ] Firmware files downloaded and extracted
[ ] USB cable connected and tested
[ ] Both keyboard halves accessible

Flash Procedure:
[ ] 1. Connect RIGHT half via USB
[ ] 2. Double-press reset button on RIGHT
[ ] 3. Drag right firmware to USB drive
[ ] 4. Wait for drive to disconnect
[ ] 5. Wait 30 seconds
[ ] 6. Connect LEFT half via USB  
[ ] 7. Double-press reset button on LEFT
[ ] 8. Drag left firmware to USB drive
[ ] 9. Wait for drive to disconnect
[ ] 10. Test keyboard!

Post-Flash:
[ ] Both halves power on
[ ] Keys respond correctly
[ ] Layers switch properly
[ ] Bluetooth pairs successfully
```

---

## Next Steps

- **Customize Layout**: Read [KEYMAP_GUIDE.md](./KEYMAP_GUIDE.md)
- **Quick Reference**: See [QUICK_REFERENCE.md](./QUICK_REFERENCE.md)
- **Report Issues**: Check GitHub issues or ZMK Discord

---

## Resources

- **ZMK Flashing Guide**: https://zmk.dev/docs/user-setup#flashing-uf2-files
- **Troubleshooting**: https://zmk.dev/docs/troubleshooting
- **ZMK Discord**: https://zmk.dev/community/discord/invite

---

**Last Updated**: 2025-11-07
**Tested on**: Eyelash Sofle, ZMK v0.3.0
