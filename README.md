# Wuwa Mobile Config

Performance and graphics configuration presets for **Wuthering Waves Mobile (Version 3.4)** designed to help optimize gameplay based on device capability.

These configs aim to improve FPS stability, visual quality, or provide a balanced gaming experience depending on your hardware.

Built using Kuro Game's official **3.4 engine configuration structure**, AlteriaX's command references, and extensive testing across multiple Android GPU architectures.

---

# 🛠️ Patch 3.4 Optimization Summary

Version **3.4** continues Kuro's streaming and memory management improvements introduced in previous versions while expanding support for newer mobile hardware.

The following optimizations are applied throughout the config collection:

* **Updated Kuro Streaming System**

  * Uses Kuro's latest streaming architecture where applicable.
  * Optimized texture streaming pools based on device tier.

* **Improved Memory Management**

  * Streaming and garbage collection values adjusted for better stability.
  * Reduced texture pop-in on higher-end presets.
  * Lower RAM pressure on low-end presets.

* **Device Tier Separation**

  * Presets are categorized by actual hardware capability rather than a one-size-fits-all approach.
  * Separate Snapdragon and All Devices profiles.

* **GPU-Specific Optimization**

  * Snapdragon presets include Adreno-focused tuning.
  * All Devices presets are designed for Mali, PowerVR, Xclipse, and other Android GPUs.

* **Streaming & World Loading Improvements**

  * Optimized World Partition loading ranges.
  * Reduced stutters during traversal and fast movement.

---

# 📁 Overview

This repository contains two main configuration folders.

## All Devices

General presets designed to work across most Android devices including:

* Mali
* PowerVR
* Xclipse
* Tegra
* Adreno

## Snapdragon

Presets specifically optimized for Qualcomm Snapdragon chipsets.

These presets include additional Adreno-focused optimizations and tuning designed for Snapdragon devices.

---

# ⚙️ Performance Presets & Recommended Chipsets

| Tier                    | Snapdragon Target         | All Devices Target         | Scale Factor         |
| ----------------------- | ------------------------- | -------------------------- | -------------------- |
| **Low End**             | Adreno 5xx / 6xx Low      | Mali T/G5x, PowerVR GE8xxx | 1.0                  |
| **Balance Performance** | Adreno 6xx / 7xx Midrange | Mali G57/G68/G78           | 1.0                  |
| **Balance Visual**      | Adreno 730 / 740          | Mali G715/G78, Xclipse 9xx | 1.5 (SD) / 1.0 (All) |
| **High End**            | Adreno 750 / 830          | Mali G925, Xclipse 9xx     | 2.0 (SD) / 1.5 (All) |

---

# Low End

Best for devices that struggle with default graphics or experience FPS drops.

### Typical Compatible Chipsets

* Snapdragon 660
* Snapdragon 665
* Snapdragon 680
* Helio G85
* Helio G88
* Helio G99
* Dimensity 700
* Dimensity 810

### What's Applied

* Reduced texture quality
* Reduced shadow quality
* Reduced view distance
* Reduced foliage density
* Reduced visual effects
* Optimized streaming pools

### Goal

*Maximum smoothness over visuals.*

---

# Balanced Performance

Focuses on stable FPS while maintaining acceptable graphics quality.

### Typical Compatible Chipsets

* Snapdragon 720G
* Snapdragon 730G
* Snapdragon 778G
* Snapdragon 845
* Snapdragon 855
* Dimensity 900
* Dimensity 920
* Dimensity 1080

### What's Applied

* Balanced texture quality
* Medium shadows
* Moderate foliage density
* Improved streaming quality
* Optimized world loading

### Goal

*Smooth gameplay with decent visuals.*

---

# Balanced Visual

Improved graphics while maintaining stable performance.

### Typical Compatible Chipsets

* Snapdragon 870
* Snapdragon 888
* Snapdragon 7+ Gen 2
* Dimensity 1200
* Dimensity 1300
* Dimensity 8020

### What's Applied

* Higher shadow quality
* Increased texture quality
* Improved post-processing
* Better foliage rendering
* Increased view distance

### Goal

*Improved visuals without sacrificing stability.*

---

# High End

Maximum visuals for flagship-level devices.

### Typical Compatible Chipsets

* Snapdragon 8 Gen 1
* Snapdragon 8+ Gen 1
* Snapdragon 8 Gen 2
* Snapdragon 8 Gen 3
* Snapdragon 8 Elite
* Dimensity 9000
* Dimensity 9200
* Dimensity 9300
* Dimensity 9400

### What's Applied

* Maximum texture quality
* Extended view distance
* Increased shadow quality
* Enhanced effects
* Increased world streaming range

### Goal

*Highest visual quality with stable high FPS.*

---

# 🎮 Frame Generation

Some presets include KuroFI-related settings where supported by the game.

> Actual frame generation availability depends on the game version, device, graphics API, and Kuro's implementation.

Not all Android devices will benefit from these settings.

---

# 📌 Installation

1. Choose either the **All Devices** or **Snapdragon** folder.
2. Select the preset suitable for your device.
3. Copy the configuration files into:

```text
Internal Storage/Android/data/
com.kurogame.wutheringwaves.global/files/
UE4Game/Client/Client/Saved/Config/Android/
```

4. Overwrite existing files when prompted.
5. Launch the game normally.

> On newer Android versions you may need Shizuku, ZArchiver, MT Manager, or another Android data folder access solution.

---

# 📖 Command Reference

https://alteriax.github.io/WuWa-Config-Info/

---

# 📖 Video Tutorial

https://youtu.be/MvgWzF41Pnc

---

# ☕ Support

If you find these configs helpful, consider supporting the project:

https://ko-fi.com/geilan63

---

# ⚠️ Important Warning

> [!WARNING]
>
> These configs are provided as-is.
>
> Choosing the wrong preset may cause:
>
> * Reduced performance
> * Overheating
> * Increased battery drain
> * Visual issues
> * Game instability
>
> Always back up your original configuration files before replacing anything.

---

# 📌 Notes

* Configs are designed specifically for Wuthering Waves 3.4.
* Snapdragon presets include Adreno-specific tuning.
* All Devices presets are designed to work across multiple Android GPU architectures.
* Future game updates may change or remove supported commands.
* Always verify functionality after major game updates.

---

# 🙏 Credits

* **AlteriaX** — Command reference, documentation, and research.
* **Arglax** — Mobile configuration references and testing methodology.
* **Kuro Game** — Wuthering Waves.

---

# 💻 Similar Repository for WuWa PC

https://github.com/AlteriaX/WuWa-Configs
