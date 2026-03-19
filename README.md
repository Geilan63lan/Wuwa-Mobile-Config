# **Wuwa Mobile Config**

Performance and graphics configuration presets for Wuthering Waves (Mobile) designed to help optimize gameplay based on device capability. These configs aim to improve FPS stability, visual quality, or provide a balanced gaming experience depending on your hardware.

Built on top of AlteriaX's command reference and adapted directly from Kuro's official 3.2 base engine files.

---

## 📁 Overview

This repository contains two main configuration folders:

### All Devices
General presets designed to work across most supported Android devices (Mali, PowerVR, Xclipse, Tegra).

### Snapdragon
Presets specifically optimized for Qualcomm Snapdragon chipsets, including Adreno-specific Vulkan optimizations and SGSR2 upscaling support for better stability and performance consistency.

---

## ⚙️ Performance Presets & Recommended Chipsets

These chipset suggestions are based on devices known to run Wuthering Waves properly.
Actual performance may still vary depending on RAM, cooling, storage speed, and device optimization.

| Tier | Snapdragon Target | All Devices Target | Scale Factor |
|---|---|---|---|
| **Low End** | Adreno 5xx / 6xx Low | Mali T/G5x, PowerVR GE8xxx | 1.0 |
| **Balance Performance** | Adreno 7xx / 8xx | Mali G715/G78, Xclipse 9xx | 1.0 |
| **Balance Visual** | Adreno 7xx / 8xx | Mali G715/G78, Xclipse 9xx | 1.5 (SD) / 1.0 (All) |
| **High End** | Adreno 7xx / 8xx | Mali G925, Xclipse 9xx | 2.0 (SD) / 1.5 (All) |

---

### Low End
Best for devices that struggle with default graphics or experience FPS drops.

**Typical compatible chipsets:**
- Snapdragon 660 / 665 / 670 / 710
- Snapdragon 720G
- MediaTek Helio G85 / G88 / G95
- Dimensity 700 / 810

**What's applied:** Minimum shadow resolution, no SSR, no AO, no fog, no foliage. Thermal throttle protection enabled by default.

**Goal:** *Maximum smoothness over visuals.*

---

### Balanced Performance
Focuses on stable FPS while maintaining acceptable graphics quality.

**Typical compatible chipsets:**
- Snapdragon 730 / 732G / 765G / 778G
- Snapdragon 845 / 855
- Dimensity 900 / 920 / 1080

**What's applied:** Fog and light shafts at reduced cost. Volumetric cloud/fog off, contact shadows off. SGSR2 on Snapdragon, FSR-only on All Devices.

**Goal:** *Smooth gameplay with decent visuals.*

---

### Balanced Visual
Better graphics while maintaining stable performance.

**Typical compatible chipsets:**
- Snapdragon 870 / 888
- Snapdragon 7+ Gen 2
- Dimensity 1200 / 1300 / 8020

**What's applied:** Full atmosphere stack, full bloom convolution, full GTAO, full shadow quality. 1.5x supersampling on Snapdragon. TAA + FSR fully configured.

**Goal:** *Improved visuals without sacrificing stability.*

---

### High End
Maximum visuals for flagship-level devices.

**Typical compatible chipsets:**
- Snapdragon 8 Gen 1 / 8+ Gen 1
- Snapdragon 8 Gen 2 / 8 Gen 3
- Dimensity 9000 / 9200 / 9300

**What's applied:** Everything in Balanced Visual plus 2.0x supersampling on Snapdragon and extended world streaming range (`wp.Runtime.KuroRuntimeStreamingRangeOverallScale=3.0`).

**Goal:** *Highest visual quality with stable high FPS.*

---

## 🎮 Frame Generation

All configs include **AFME (Kuro's native mobile frame interpolation)** configured in both `DeviceProfiles.ini` CVars and `Engine.ini`.

> FSR Frame Generation is **not applicable on Android** — FSR on mobile is upscaling only.

- **Snapdragon tiers:** AFME set in both DeviceProfiles + Engine.ini
- **All Devices tiers:** AFME set in Engine.ini only (hardware support varies by device)

---

## 📌 Installation

1. Choose either the **All Devices** or **Snapdragon** folder
2. Select the preset suitable for your device
3. **Copy the config files into this directory:**

```
Internal Storage/Android/data/
com.kurogame.wutheringwaves.global/files/
UE4Game/Client/Client/Saved/Config/Android/
```

4. Overwrite existing files when prompted
5. Launch the game normally

> ⚠️ On newer Android versions you may need **Shizuku** or a similar tool to access the data folder.

---

## 📖 Code Explanations

https://alteriax.github.io/WuWa-Config-Info/

https://youtu.be/MvgWzF41Pnc

---

## ☕ Support

If you find these configs helpful, consider supporting via Ko-Fi!

https://ko-fi.com/geilan63

---

## ⚠️ Important Warning

> [!WARNING]
> These configs are provided as-is with **minimal** guarantees.
> Choosing the **wrong preset** may cause crashes, instability, overheating, or performance issues.
> **I am NOT responsible** for any problems caused by **incorrect usage**.
> Always back up your original config files before replacing anything.

---

## 📌 Notes

- All configs are based on Kuro's **official 3.2 base engine files**, not generated from scratch
- Snapdragon configs include Adreno-specific Vulkan optimizations — these are excluded from All Devices configs
- SGSR2 is Snapdragon-exclusive and is disabled in all All Devices configs
- Always verify your CVars in `Client.log` after applying

---

## 🙏 Credits

- **AlteriaX** — command reference and config philosophy
- **Arglax** — Mobile WuWa Config reference and GPU crash notes
- Kuro Game — base 3.2 engine files

---

## 💻 Similar Repository for WuWa PC

https://github.com/AlteriaX/WuWa-Configs.git
