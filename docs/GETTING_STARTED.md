# Getting Started with Your ZMK Sofle Keyboard

## 🎯 Your Complete Step-by-Step Workflow

This guide walks you through everything you need to know, in order.

---

## Phase 1: Understanding (10 minutes)

### What You Have

You have a **forked repository** for a ZMK-powered Sofle split keyboard. Here's what that means:

- **Split Keyboard**: Two halves (left and right) that communicate via Bluetooth
- **ZMK Firmware**: Modern, wireless keyboard firmware
- **GitHub-Based**: You edit files, push to GitHub, it builds firmware automatically
- **Highly Customizable**: Full control over layout, layers, features

### Key Concept: The Workflow

```
1. Edit keymap file locally
   ↓
2. Commit and push to GitHub
   ↓
3. GitHub Actions builds firmware automatically
   ↓
4. Download .uf2 files
   ↓
5. Flash to keyboard
   ↓
6. Test and repeat!
```

**You never install build tools locally** - GitHub does all the compilation!

---

## Phase 2: First Build (30 minutes)

### Step 1: Verify Repository Setup

Your repository is at:
```
G:\Sofle Keyboard\zmk-sofle-1\
```

Check that you have:
- [x] Forked the original repository ✓
- [x] Cloned to your local machine ✓
- [ ] GitHub Actions enabled (we'll check this next)

### Step 2: Check GitHub Actions

1. **Go to your repository** on GitHub:
   ```
   https://github.com/YOUR_USERNAME/zmk-sofle-1
   ```

2. **Click the "Actions" tab** at the top

3. **If you see workflows listed**: ✅ You're good!

4. **If you see a message about enabling Actions**:
   - Click "I understand my workflows, go ahead and enable them"
   - Actions are now enabled

### Step 3: Trigger Your First Build

**Option A: Manual Trigger** (Recommended for first time)

1. On the **Actions** tab, click **"Build ZMK firmware"** in the left sidebar
2. Click the **"Run workflow"** dropdown button (top right)
3. Keep the branch as `main`
4. Click the green **"Run workflow"** button
5. **Wait 5-10 minutes** - grab a coffee! ☕

**Option B: Push Trigger**

```bash
cmd /c cd /d "G:\Sofle Keyboard\zmk-sofle-1"
cmd /c git commit --allow-empty -m "Trigger build"
cmd /c git push
```

### Step 4: Monitor the Build

1. Click on the running workflow (it'll show "Build ZMK firmware" with a yellow dot)
2. Click on the **"build"** job to see live logs
3. Watch it compile - you'll see:
   - Checking out code
   - Setting up ZMK
   - Building each firmware variant
   - Uploading artifacts

### Step 5: Download Firmware

Once the build succeeds (green checkmark ✅):

1. Scroll to the bottom of the workflow page
2. Find **"Artifacts"** section
3. Click **firmware.zip** to download
4. Extract the ZIP file

You'll get:
- `eyelash_sofle_left-nice_view-zmk.uf2` (Standard left)
- `eyelash_sofle_right-nice_view-zmk.uf2` (Right)
- `eyelash_sofle_studio_left-nice_view-zmk.uf2` (Studio left)
- `settings_reset-nice_nano_v2-zmk.uf2` (Utility)

**Save these files somewhere safe!** 💾

---

## Phase 3: First Flash (15 minutes)

### Preparation

You'll need:
- [ ] USB cable
- [ ] Both keyboard halves
- [ ] Downloaded firmware files
- [ ] 5 minutes per half

### ⚠️ CRITICAL: Flash Order

**ALWAYS flash RIGHT half first, then LEFT!**

This ensures proper Bluetooth pairing.

### Flashing RIGHT Half

1. **Connect RIGHT half** to your computer via USB

2. **Enter bootloader mode**:
   - Locate the **reset button** on the keyboard PCB
   - **Double-press** it quickly (within 1 second)
   - You should see a **USB drive** appear (e.g., "NICENANO")

3. **If drive doesn't appear**:
   - Try double-pressing faster
   - Try a different USB cable (some are charge-only)
   - Try a different USB port

4. **Flash the firmware**:
   - Open the USB drive in File Explorer
   - **Drag** `eyelash_sofle_right-nice_view-zmk.uf2` onto the drive
   - Drive will **disconnect automatically** after 2-5 seconds

5. **Success!** ✅ Right half is now flashed

6. **Wait 30 seconds** before proceeding

### Flashing LEFT Half

1. **Disconnect RIGHT half**

2. **Connect LEFT half** to your computer via USB

3. **Enter bootloader mode**:
   - Double-press the reset button

4. **Flash the firmware**:
   - Drag `eyelash_sofle_left-nice_view-zmk.uf2` onto the drive
   - Wait for automatic disconnect

5. **Success!** ✅ Left half is now flashed

---

## Phase 4: First Test (10 minutes)

### Power On

1. **Disconnect USB** from both halves
2. **Turn on power switches** (if your keyboard has them)
3. **Wait 10 seconds** for Bluetooth handshake
4. **Check OLED displays** - should show battery/connection info

### Test Keys

1. **Press a few keys** on each half
   - They might not do anything yet (not paired to computer)
   - Just checking that halves communicate

2. **Test layers**:
   - Hold bottom-left thumb key (Layer 1)
   - Hold bottom-right thumb key (Layer 2)
   - Keys should work on both halves

### Bluetooth Pairing

1. **On keyboard**:
   - Hold the right thumb key (Layer 2)
   - Press the top-left key on left half (BT_SEL 0)
   - This selects Bluetooth profile 0

2. **On your computer**:
   - Open Bluetooth settings
   - Look for a device like "Sofle" or "zmk-sofle"
   - Click "Pair" or "Connect"

3. **Test typing**:
   - Open Notepad or any text editor
   - Type some keys
   - **If it works**: 🎉 SUCCESS! You're done!
   - **If not**: See troubleshooting below

### Test Special Features

- **Encoder**: Turn it - should control volume
- **Layer 1**: Hold left thumb, test function keys
- **Layer 2**: Hold right thumb, test Bluetooth controls
- **RGB** (if enabled): Access Layer 1, press RGB control keys

---

## Phase 5: First Customization (30 minutes)

### Understanding Your Keymap

The file you'll edit is:
```
config/eyelash_sofle.keymap
```

Open it in your favorite text editor (VS Code recommended).

### Your First Edit

Let's change one key to verify the workflow:

1. **Open the keymap file**:
   ```bash
   cmd /c code "G:\Sofle Keyboard\zmk-sofle-1\config\eyelash_sofle.keymap"
   ```

2. **Find Layer 0** (around line 56):
   ```c
   layer0 {
       bindings = <
           &kp ESC  &kp N1  &kp N2  ...
   ```

3. **Change ESC to GRAVE** (the ` key):
   ```c
   // Before:
   &kp ESC
   
   // After:
   &kp GRAVE
   ```

4. **Save the file**

5. **Commit and push**:
   ```bash
   cmd /c cd /d "G:\Sofle Keyboard\zmk-sofle-1"
   cmd /c git add config/eyelash_sofle.keymap
   cmd /c git commit -m "Test: change ESC to GRAVE"
   cmd /c git push
   ```

6. **Wait for build** (5-10 minutes)
   - Check GitHub Actions tab
   - Wait for green checkmark

7. **Download new firmware**

8. **Flash to keyboard** (both halves)

9. **Test**: Top-left key should now be ` instead of ESC

**It worked? Congratulations!** 🎊 You've completed the full cycle!

---

## Phase 6: Advanced Usage (Ongoing)

Now you're ready to:

### Customize Your Layout

Read **[KEYMAP_GUIDE.md](./KEYMAP_GUIDE.md)** to learn:
- How to remap any key
- Add custom layers
- Create combos (multiple keys pressed together)
- Add macros (sequences of keys)
- Convert from your `byou.json` layout

### Optimize Settings

Edit **`config/eyelash_sofle.conf`** to adjust:
- Sleep timeout
- RGB brightness
- Debounce timing
- Power management

### Use ZMK Studio (Optional)

For live editing without rebuilding:

1. Flash `eyelash_sofle_studio_left-nice_view-zmk.uf2` to LEFT half
2. Connect LEFT half via USB
3. Go to https://zmk.studio
4. Edit keymap in real-time!

**Note**: Only works on left half.

---

## Troubleshooting

### Build Fails

**Error: "Syntax error"**
- Check for missing semicolons `;` in keymap
- Ensure all `<` and `>` are paired
- Verify key codes are valid

**How to fix**:
1. Click on failed build in Actions
2. Read error message (tells you the line number)
3. Fix the error in your keymap
4. Commit and push again

### Flash Fails

**Drive doesn't appear**
- Double-press faster
- Try different USB cable
- Try different USB port

**Flashed but keys don't work**
- Reflash both halves (RIGHT first!)
- Try settings reset (flash `settings_reset` firmware)
- Check battery connections

### Bluetooth Issues

**Won't pair**
- Press `BT_CLR` on Layer 2 (top-left, third row)
- Forget device in computer's Bluetooth settings
- Try pairing again

**One half works, other doesn't**
- Reflash in correct order (RIGHT first!)
- Wait 30 seconds between flashes
- Check both batteries are charged

---

## Quick Reference Commands

### Navigate to Repository
```bash
cmd /c cd /d "G:\Sofle Keyboard\zmk-sofle-1"
```

### Check Status
```bash
cmd /c git status
```

### Add Changes
```bash
cmd /c git add config/eyelash_sofle.keymap
```

### Commit
```bash
cmd /c git commit -m "Describe your changes here"
```

### Push (Triggers Build)
```bash
cmd /c git push
```

### View Logs
```bash
cmd /c git log --oneline -5
```

---

## Next Steps

You've completed the getting started guide! Now:

1. **Bookmark** [QUICK_REFERENCE.md](./QUICK_REFERENCE.md) for quick lookups
2. **Read** [KEYMAP_GUIDE.md](./KEYMAP_GUIDE.md) to customize your layout
3. **Experiment** with different layouts and features
4. **Join** the ZMK Discord: https://zmk.dev/community/discord/invite

---

## Summary Checklist

- [ ] Repository forked and cloned
- [ ] GitHub Actions enabled
- [ ] First firmware built successfully
- [ ] RIGHT half flashed
- [ ] LEFT half flashed
- [ ] Keyboard powers on
- [ ] Bluetooth paired to computer
- [ ] Keys work correctly
- [ ] Layers switch properly
- [ ] First keymap edit completed
- [ ] Custom firmware built and flashed
- [ ] Documentation bookmarked

**All checked?** You're now a ZMK keyboard master! 🏆

---

**Need more details?** Read the comprehensive guides:
- [PROJECT_OVERVIEW.md](./PROJECT_OVERVIEW.md)
- [BUILD_GUIDE.md](./BUILD_GUIDE.md)
- [KEYMAP_GUIDE.md](./KEYMAP_GUIDE.md)
- [QUICK_REFERENCE.md](./QUICK_REFERENCE.md)

Happy typing! ⌨️✨
