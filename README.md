# **Wuwa Mobile Config**

Performance and graphics configuration presets for Wuthering Waves (Mobile) designed to help optimize gameplay based on device capability. These configs aim to improve FPS stability, visual quality, or provide a balanced gaming experience depending on your hardware.

Built on top of AlteriaX's command reference and adapted directly from Kuro's official **3.3 base engine files**[cite: 1].

---

## 🛠️ Patch 3.3 Optimization Summary

The transition to **Version 3.3 (2nd Anniversary)** introduced significant engine-level overhauls to support massive storage reduction and the high-density anniversary map areas[cite: 1]. The following core coding updates have been applied across all presets:

*   **New Kuro Streaming**: Forced `r.Streaming.UsingNewKuroStreaming=1` to utilize the overhauled 3.3 asset streaming architecture[cite: 1, 15, 17, 19, 21].
*   **Low Memory Logic**: Implemented `m.LowMemoryDeviceThreshold=5800` to correctly trigger performance profiles on 6GB RAM devices[cite: 1, 14, 16, 18, 20].
*   **Anniversary Map Stability**: Optimized foliage and geometry via `r.LandscapeLOD0ScreenSizeScale` and `r.Kuro.Foliage.EnableFoliageCulling` to handle new high-density environments[cite: 1, 15, 17, 19, 21].
*   **Snapdragon Super Resolution**: Explicitly configured the `GSRTUModule` and `bEnableGSR=1` for Snapdragon tiers to improve clarity[cite: 1, 3, 7, 11].
*   **Priority Level Overrides**: Moved critical CVars like `r.ScreenPercentage` into the `VeryHigh` device profile base to bypass 3.3's project-level setting locks[cite: 1, 14, 16, 18, 20].
*   **Batching Improvements**: Activated `HISMBatcher` and `r.BBM.EnableBatcher` to improve rendering efficiency of world objects[cite: 1, 15, 17, 19, 21].

---

## 📁 Overview

This repository contains two main configuration folders:

### All Devices
General presets designed to work across most supported Android devices (Mali, PowerVR, Xclipse, Tegra)[cite: 12].

### Snapdragon
Presets specifically optimized for Qualcomm Snapdragon chipsets, including Adreno-specific optimizations and GSR upscaling support for better stability and performance consistency[cite: 4, 10].

---

## ⚙️ Performance Presets & Recommended Chipsets

These chipset suggestions are based on devices known to run Wuthering Waves properly[cite: 4, 10, 12, 20]. Actual performance may still vary depending on RAM, cooling, storage speed, and device optimization.

| Tier | Snapdragon Target | All Devices Target | Scale Factor |
|---|---|---|---|
| **Low End** | Adreno 5xx / 6xx Low | Mali T/G5x, PowerVR GE8xxx | 1.0 |
| **Balance Performance** | Adreno 7xx / 8xx | Mali G715/G78, Xclipse 9xx | 1.0 |
| **Balance Visual** | Adreno 7xx / 8xx | Mali G715/G78, Xclipse 9xx | 1.5 (SD) / 1.0 (All) |
| **High End** | Adreno 7xx / 8xx | Mali G925, Xclipse 9xx | 2.0 (SD) / 1.5 (All) |

---

### Low End
Best for devices that struggle with default graphics or experience FPS drops[cite: 15].

**Typical compatible chipsets:**
- Snapdragon 660 / 665 / 670 / 710[cite: 3]
- Snapdragon 720G[cite: 3]
- MediaTek Helio G85 / G88 / G95
- Dimensity 700 / 810[cite: 13]

**What's applied**: Minimum shadow resolution, no SSR, no AO, no fog, no foliage[cite: 15]. Thermal throttle protection enabled by default[cite: 15]. Aggressive `r.streaming.QualityExtraLODBiasSetting=975` is applied to save VRAM[cite: 1, 15].

**Goal**: *Maximum smoothness over visuals.*

---

### Balanced Performance
Focuses on stable FPS while maintaining acceptable graphics quality[cite: 7, 17].

**Typical compatible chipsets:**
- Snapdragon 730 / 732G / 765G / 778G[cite: 6]
- Snapdragon 845 / 855[cite: 6]
- Dimensity 900 / 920 / 1080[cite: 17]

**What's applied**: Fog and light shafts at reduced cost[cite: 7, 17]. Volumetric cloud/fog off, contact shadows off[cite: 17]. GSR on Snapdragon, FSR-only on All Devices[cite: 7, 17].

**Goal**: *Smooth gameplay with decent visuals.*

---

### Balanced Visual
Better graphics while maintaining stable performance[cite: 9, 19].

**Typical compatible chipsets:**
- Snapdragon 870 / 888[cite: 8]
- Snapdragon 7+ Gen 2[cite: 8]
- Dimensity 1200 / 1300 / 8020[cite: 19]

**What's applied**: Full atmosphere stack, full bloom convolution, full GTAO, full shadow quality[cite: 9, 19]. 1.5x supersampling on Snapdragon[cite: 8]. TAA + FSR fully configured[cite: 9, 19].

**Goal**: *Improved visuals without sacrificing stability.*

---

### High End
Maximum visuals for flagship-level devices[cite: 11, 21].

**Typical compatible chipsets:**
- Snapdragon 8 Gen 1 / 8+ Gen 1[cite: 10]
- Snapdragon 8 Gen 2 / 8 Gen 3[cite: 10]
- Dimensity 9000 / 9200 / 9300[cite: 21]

**What's applied**: Everything in Balanced Visual plus 2.0x supersampling and extended world streaming range (`wp.Runtime.KuroRuntimeStreamingRangeOverallScale=3.0`)[cite: 11, 21].

**Goal**: *Highest visual quality with stable high FPS.*

---

## 🎮 Frame Generation

All configs include **r.KuroFI.Enable** configured in `DeviceProfiles.ini` CVars[cite: 1, 14, 20].

> FSR Frame Generation is **not applicable on Android** — FSR on mobile is upscaling only.

- **On Vulkan devices**: → works[cite: 1]  
- **On OpenGL devices**: → shaders fail silently, no crash, just ignored[cite: 1]

---

## 📌 Installation

1. Choose either the **All Devices** or **Snapdragon** folder.
2. Select the preset suitable for your device.
3. **Copy the config files into this directory**:

```
Internal Storage/Android/data/
com.kurogame.wutheringwaves.global/files/
UE4Game/Client/Client/Saved/Config/Android/
```

4. Overwrite existing files when prompted.
5. Launch the game normally.

> ⚠️ On newer Android versions you may need **Shizuku** or a similar tool to access the data folder.

---

## 📖 Code Explanations

[https://alteriax.github.io/WuWa-Config-Info/](https://alteriax.github.io/WuWa-Config-Info/)

---

## 📖 Youtube Tutorial

[https://youtu.be/MvgWzF41Pnc](https://youtu.be/MvgWzF41Pnc)

---

## ☕ Support

If you find these configs helpful, consider supporting via Ko-Fi!

[https://ko-fi.com/geilan63](https://ko-fi.com/geilan63)

---

## ⚠️ Important Warning

> [!WARNING]
> These configs are provided as-is with **minimal** guarantees.
> Choosing the **wrong preset** may cause crashes, instability, overheating, or performance issues.
> **I am NOT responsible** for any problems caused by **incorrect usage**.
> Always back up your original config files before replacing anything.

---

## 📌 Notes

- All configs are based on Kuro's **official 3.3 base engine files**, not generated from scratch[cite: 1].
- Snapdragon configs include Adreno-specific optimizations — these are excluded from All Devices configs.
- GSR is Snapdragon-exclusive and is disabled in all All Devices configs[cite: 1].
- Always verify your CVars in `Client.log` after applying[cite: 1].

---

## 🙏 Credits

- **AlteriaX** — command reference and config philosophy.
- **Arglax** — Mobile WuWa Config reference and GPU crash notes.
- Kuro Game — base 3.3 engine files[cite: 1].

---

## 💻 Similar Repository for WuWa PC

[https://github.com/AlteriaX/WuWa-Configs.git](https://github.com/AlteriaX/WuWa-Configs.git)