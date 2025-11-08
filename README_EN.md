# Sofle

- [Chinese](README.md)
- [English](README_EN.md)

## Update List

- 2024/12/21
  1. Added support for zmk-studio (just refresh the left hand to use).
- 2024/10/24
  1. Modified power supply mode to reduce power consumption.
  2. Fixed the automatic shut-off feature for RGB power supply.
- 2025/8/22
  1. update the soft off.When you press the keys Q, S and Z simultaneously and hold them for 2 seconds, the keyboard will enter a deep sleep state and cannot be awakened by pressing the keys. This function can be used when carrying it outside. The activation method is to press the reset switch once.
  2. This month, I also updated the ultra-thin versions of the corne and sofle cases. The frame and base plate have been thickened, and the opening of the reset switch has been adjusted, so that the reset switch can be easily pressed. At present, we are still conceptualizing how to design the shell with an inclined bracket.If you have carefully examined a PCB, you will notice that there are reserved interfaces for expansion IO. I wonder if anyone has been able to utilize them,I will try it！
  3. The GIF animations on the right-hand keyboard screen have been removed, which will significantly reduce the power consumption of the right-hand keyboard.

> If your  sofle was updated before 2025/8/22, please update to the latest firmware.
>

## Contact Me

For 3D printed model files or any issues and malfunctions with the keyboard, please contact [380465425@qq.com](mailto:380465425@qq.com)

## 📚 Comprehensive Documentation

**Complete step-by-step guides available!**

For detailed instructions, see the [docs/](./docs/) folder:

- **[docs/PROJECT_OVERVIEW.md](./docs/PROJECT_OVERVIEW.md)** - Complete project documentation
  - Repository structure explained
  - How ZMK firmware works
  - GitHub Actions workflow details
  
- **[docs/BUILD_GUIDE.md](./docs/BUILD_GUIDE.md)** - Build and flash instructions
  - Step-by-step firmware building
  - Flashing to your keyboard
  - Troubleshooting guide
  
- **[docs/KEYMAP_GUIDE.md](./docs/KEYMAP_GUIDE.md)** - Keymap customization guide
  - Understanding keymap syntax
  - Complete key code reference
  - Adding layers, combos, macros
  - Converting from QMK (byou.json)
  
- **[docs/QUICK_REFERENCE.md](./docs/QUICK_REFERENCE.md)** - Quick reference cheat sheet
  - One-page layout overview
  - Common tasks
  - Troubleshooting shortcuts

**Getting Started**: Start with [docs/README.md](./docs/README.md)!

---

## Sofle Keymap

![Sofle键位图](keymap-drawer/eyelash_sofle.svg)
