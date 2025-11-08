# ZMK Sofle Keyboard - Documentation

Welcome to the comprehensive documentation for your ZMK Sofle keyboard firmware!

## 📚 Documentation Structure

### 🚀 Getting Started

**NEW USER? START HERE!**

0. **[GETTING_STARTED.md](./GETTING_STARTED.md)** - Complete step-by-step walkthrough
   - Your first build
   - Your first flash
   - Your first customization
   - Everything in order!

Then continue with:

1. **[PROJECT_OVERVIEW.md](./PROJECT_OVERVIEW.md)** - Complete project documentation
   - Repository structure
   - How the firmware works
   - GitHub Actions workflow
   - Key components explained

### 🔨 Building & Flashing

2. **[BUILD_GUIDE.md](./BUILD_GUIDE.md)** - Step-by-step build and flash instructions
   - Using GitHub Actions to build firmware
   - Downloading firmware files
   - Flashing to your keyboard
   - Troubleshooting build issues
   - Settings reset procedures

### ⌨️ Customization

3. **[KEYMAP_GUIDE.md](./KEYMAP_GUIDE.md)** - Complete keymap customization guide
   - Understanding the keymap file structure
   - ZMK key code reference
   - Adding layers
   - Creating combos and macros
   - Converting from QMK (byou.json)
   - Advanced features

### ⚡ Quick Reference

4. **[QUICK_REFERENCE.md](./QUICK_REFERENCE.md)** - One-page cheat sheet
   - Current layout overview
   - Common tasks
   - Key code quick lookup
   - Troubleshooting shortcuts
   - Emergency commands

---

## 🎯 Quick Navigation

### I want to...

**Build firmware:**
→ Read [BUILD_GUIDE.md](./BUILD_GUIDE.md) → Section "Building Firmware"

**Flash firmware:**
→ Read [BUILD_GUIDE.md](./BUILD_GUIDE.md) → Section "Flashing Firmware"

**Change my layout:**
→ Read [KEYMAP_GUIDE.md](./KEYMAP_GUIDE.md) → Section "Common Modifications"

**Understand how it works:**
→ Read [PROJECT_OVERVIEW.md](./PROJECT_OVERVIEW.md) → Section "How It Works"

**Fix a problem:**
→ Check [QUICK_REFERENCE.md](./QUICK_REFERENCE.md) → Section "Troubleshooting"

**See my current layout:**
→ Check [QUICK_REFERENCE.md](./QUICK_REFERENCE.md) → Section "Current Layout"

---

## 📖 Reading Order

### For Complete Beginners

1. Start with **[PROJECT_OVERVIEW.md](./PROJECT_OVERVIEW.md)** (15 min read)
   - Understand what you're working with
   - Learn the repository structure
   - See how GitHub Actions builds firmware

2. Continue with **[BUILD_GUIDE.md](./BUILD_GUIDE.md)** (20 min read)
   - Learn how to build firmware
   - Flash it to your keyboard
   - Test that everything works

3. Read **[KEYMAP_GUIDE.md](./KEYMAP_GUIDE.md)** (30 min read)
   - Understand the keymap syntax
   - Learn key codes
   - Start customizing your layout

4. Bookmark **[QUICK_REFERENCE.md](./QUICK_REFERENCE.md)**
   - Keep it handy for quick lookups
   - Reference while editing

### For Experienced Users

If you've worked with ZMK before:

1. **[QUICK_REFERENCE.md](./QUICK_REFERENCE.md)** - See current layout and quick commands
2. **[KEYMAP_GUIDE.md](./KEYMAP_GUIDE.md)** - Dive into customization
3. **[PROJECT_OVERVIEW.md](./PROJECT_OVERVIEW.md)** - Reference as needed

---

## 🔑 Key Files in This Repository

| File | What It Does | When to Edit |
|------|--------------|--------------|
| `config/eyelash_sofle.keymap` | **YOUR KEYBOARD LAYOUT** | Edit to customize keys |
| `config/eyelash_sofle.conf` | Hardware/feature settings | Rarely (e.g., change debounce) |
| `build.yaml` | What firmware to build | Rarely (e.g., add/remove builds) |
| `byou.json` | QMK layout reference | Reference only (not used by ZMK) |
| `.github/workflows/build.yml` | Build automation | Don't edit unless you know what you're doing |

---

## 🎓 Learning Path

### Week 1: Understanding
- [ ] Read PROJECT_OVERVIEW.md
- [ ] Understand repository structure
- [ ] Know what files do what
- [ ] Understand the build process

### Week 2: Building
- [ ] Build firmware using GitHub Actions
- [ ] Download and flash firmware
- [ ] Test all layers
- [ ] Verify encoder and special features work

### Week 3: Customizing
- [ ] Make small keymap changes
- [ ] Build and test
- [ ] Add a custom layer
- [ ] Create a combo or macro

### Week 4: Mastery
- [ ] Implement your full custom layout
- [ ] Add advanced features
- [ ] Optimize for your workflow
- [ ] Share your setup!

---

## 💡 Pro Tips

1. **Start Small**: Don't change everything at once. Test incrementally.
2. **Commit Often**: Use git to track changes. Easy to revert mistakes.
3. **Comment Code**: Add `//` comments in your keymap for future reference.
4. **Use ZMK Studio**: Flash studio firmware on left half for live testing.
5. **Keep Backups**: Save working firmware files before major changes.
6. **Check Visualizations**: Look at generated SVG files to verify layout.
7. **Join Community**: ZMK Discord is incredibly helpful!

---

## 🔍 Documentation Standards

All documentation in this folder follows these principles:

- **Beginner-Friendly**: Assumes minimal technical knowledge
- **Step-by-Step**: Clear instructions with examples
- **Windows-Focused**: Uses `cmd /c` for commands (your system)
- **Comprehensive**: Covers common tasks and edge cases
- **Cross-Referenced**: Links between docs for easy navigation
- **Up-to-Date**: Last updated 2025-11-07 for ZMK v0.3.0

---

## 🆘 Getting Help

### First Steps
1. Check **[QUICK_REFERENCE.md](./QUICK_REFERENCE.md)** troubleshooting section
2. Read relevant section in main guides
3. Check build logs in GitHub Actions

### Still Stuck?
- **ZMK Discord**: https://zmk.dev/community/discord/invite
- **ZMK Docs**: https://zmk.dev/docs
- **GitHub Issues**: Check this repo's issues tab

### Reporting Issues
When asking for help, provide:
- What you're trying to do
- What you expected to happen
- What actually happened
- Build logs (if build failed)
- Your keymap file (if keys don't work)

---

## 📋 Common Tasks Quick Links

| Task | Link | Time |
|------|------|------|
| **First-time setup** | [BUILD_GUIDE.md](./BUILD_GUIDE.md) | 30 min |
| **Build firmware** | [BUILD_GUIDE.md#building-firmware](./BUILD_GUIDE.md#building-firmware) | 10 min |
| **Flash keyboard** | [BUILD_GUIDE.md#flashing-firmware](./BUILD_GUIDE.md#flashing-firmware) | 5 min |
| **Change one key** | [KEYMAP_GUIDE.md#example-1-change-base-layer-key](./KEYMAP_GUIDE.md#example-1-change-base-layer-key) | 5 min |
| **Add new layer** | [KEYMAP_GUIDE.md#layer-anatomy](./KEYMAP_GUIDE.md#layer-anatomy) | 15 min |
| **Create combo** | [KEYMAP_GUIDE.md#combos](./KEYMAP_GUIDE.md#combos) | 10 min |
| **Bluetooth pair** | [BUILD_GUIDE.md#bluetooth-pairing](./BUILD_GUIDE.md#bluetooth-pairing) | 2 min |
| **Reset settings** | [BUILD_GUIDE.md#settings-reset](./BUILD_GUIDE.md#settings-reset) | 5 min |

---

## 🎯 Your Next Steps

1. **If you haven't built yet**: Read [BUILD_GUIDE.md](./BUILD_GUIDE.md)
2. **If you want to customize**: Read [KEYMAP_GUIDE.md](./KEYMAP_GUIDE.md)
3. **For quick reference**: Bookmark [QUICK_REFERENCE.md](./QUICK_REFERENCE.md)

---

## 📁 Additional Resources

In the repository:
- `keymap-drawer/eyelash_sofle.svg` - Visual representation of your layout
- `config/west.yml` - Dependencies and versions
- `boards/arm/eyelash_sofle/` - Custom board definition

External:
- **ZMK Website**: https://zmk.dev
- **ZMK GitHub**: https://github.com/zmkfirmware/zmk
- **Board Repository**: https://github.com/a741725193/zmk-sofle
- **Keymap Editor**: https://nickcoutsos.github.io/keymap-editor/

---

## 📝 Documentation Changelog

**2025-11-07**:
- Initial comprehensive documentation created
- PROJECT_OVERVIEW.md - Complete repository guide
- BUILD_GUIDE.md - Build and flash instructions
- KEYMAP_GUIDE.md - Customization guide
- QUICK_REFERENCE.md - Cheat sheet

---

## 🙏 Credits

- **ZMK Firmware**: https://zmk.dev
- **Board Designer**: a741725193 (https://github.com/a741725193)
- **Sofle Keyboard**: Original design by Josef Adamčík
- **Documentation**: Created for this fork

---

**Happy Typing! ⌨️✨**

For questions about these docs, open an issue in this repository.
