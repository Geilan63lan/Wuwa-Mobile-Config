# WuWa Mobile Config — Personal 3.7 Build

Performance and graphics configuration presets for **Wuthering Waves Mobile (Version 3.7)**, compiled and cleaned up across eight tiers: four **All Devices** presets and four **Snapdragon**-specific presets.

This is a personally maintained compilation built by pulling current files from Arglax's [Mobile-WuWa-Config](https://github.com/Arglax/Mobile-WuWa-Config) repo (All Devices side, restructured for 3.6) and a Snapdragon-specific source in the same style as AlteriaX/Geilan63lan's Adreno-focused configs, then auditing every file for bugs, dead CVars, and version consistency. It is **not** an official redistribution of either project — see Credits below.

---

## 📁 Folder Structure

```
All Devices/
├── Low End/
├── Balanced Performance/
├── Balanced Visual/
└── High End/

Snapdragon/
├── Low End/
├── Balanced Performance/
├── Balanced Visual/
└── High End/
```

Each folder contains an `Engine.ini` and a `DeviceProfiles.ini`.

**All Devices** — general presets for Mali, PowerVR, Xclipse, Unisoc, and other non-Snapdragon Android GPUs.
**Snapdragon** — presets with Adreno-specific device family mapping and tuning. Generally scored higher than their All Devices counterpart at the same nominal tier, since Adreno drivers tend to sustain performance better than budget Mali/PowerVR silicon.

---

## 📌 Installation

1. Choose either the **All Devices** or **Snapdragon** folder based on your chipset.
2. Pick the tier that matches your device (see below).
3. Copy `Engine.ini` and `DeviceProfiles.ini` into:

```text
Internal Storage/Android/data/
com.kurogame.wutheringwaves.global/files/
UE4Game/Client/Client/Saved/Config/Android/
```

4. Overwrite existing files when prompted.
5. Launch the game normally.

> On newer Android versions you may need Shizuku, ZArchiver, MT Manager, or another Android data folder access solution to reach that path.

---

## ⚙️ Tier Guide

| Tier | Goal | Typical Chipsets (rough guide) |
|---|---|---|
| **Low End** | Maximum smoothness over visuals | Snapdragon 660–680, Helio G85/G88/G99, Dimensity 700/810, older Mali/PowerVR |
| **Balanced Performance** | Stable FPS with acceptable visuals | Snapdragon 720G–855, Dimensity 900–1080, mid-range Mali G57/G68 |
| **Balanced Visual** | Better visuals without sacrificing stability | Snapdragon 870–7+ Gen 2, Dimensity 1200–8020, Mali G715/G78 |
| **High End** | Maximum visual quality, flagship hardware | Snapdragon 8 Gen 1–8 Elite, Dimensity 9000–9400, Mali G925 |

Some tiers use a single file with a **profile-name toggle** rather than fully separate configs — check the top of `DeviceProfiles.ini` and `Engine.ini` for a commented-out alternate profile line (e.g. swapping `Android_High` for `Android_Adreno840`) if you own a flagship Adreno chip but want a lighter preset while still unlocking chip-exclusive features like Frame Gen.

---

## 🎮 Frame Generation

Several tiers (Balanced Performance and up) include `r.KuroFI.*` settings. Actual availability depends on your device, graphics API, and Kuro's implementation — not every device will benefit. Both **Low End** tiers disable Frame Interpolation entirely; it's pure overhead with no upside on weak hardware.

---

## 🛠️ What Changed in This Compilation

### 1. Version headers updated 3.5 → 3.6
Several source files still carried 3.5-era headers despite 3.6 content/structure changes upstream (notably Arglax's move to a `dp.Override` profile-forcing system on some tiers, replacing the old `DeviceScore`/`BaseProfileName` GPU auto-detection). Headers were corrected across all eight tiers.

### 2. Casing normalized (`Cvars=` → `CVars=`)
The engine's ini key is case-sensitive as `CVars`. Several source files inconsistently mixed `Cvars=` and `CVars=` within the same file (usually the first few lines). Normalized throughout — affected nearly every tier's `DeviceProfiles.ini`.

### 3. Forbidden CVar removed: `r.ScreenPercentage`
This CVar is on Kuro's `ConfigMonitor` blacklist — setting it does nothing; the engine strips it at runtime. It appeared (and was doing nothing) in:
- All Devices Balanced Visual & High End
- Snapdragon Balanced Visual & High End

Commented out with an explanatory note rather than silently deleted, so the intent is preserved in case a future patch un-blacklists it.

### 4. Duplicate-key bug fixed: `r.ScreenSizeCullRatioFactor`
Both the All Devices and Snapdragon **Balanced Performance** `Engine.ini` files set this CVar twice in the same section (`2.5` near the top, a stray `5` further down) — same section, same key, so only the last value actually applied, silently overriding the intended `2.5` with the Low-End tier's more aggressive culling value. The stray duplicate was removed.

### 5. Structural change for 3.6 (Stable Configs tiers)
Arglax's repo restructured the device-matching system on the `Stable Configs` tiers: instead of the engine auto-detecting a GPU and scoring it against a `DeviceScore`, `dp.Override` in `Engine.ini` now force-assigns every device directly to a named profile. The old GPU-family mapping blocks (dozens of `[Android_Mali_*]`/`[Android_Adreno*]` sections) are no longer needed on those tiers. Reflected accordingly in the All Devices Low/Mid/High-End files.

### 6. Reconstructed files (flagged, not verified)
Two files in this set could not be pulled from a live, verified source and were built by extrapolating from adjacent tiers instead:
- **All Devices High End `Engine.ini`** — built from the Low/Balanced Performance/Balanced Visual progression pattern before the correct source file was located.
- **Snapdragon Low End `Engine.ini`** — built by applying the same 3.5→3.6 structural changes seen on the All Devices Low End file to the user's existing Snapdragon-tuned v3.5 file.

Both are marked in-file. Treat these two specifically as best-effort drafts — check `Client.log` after installing to confirm the CVars are actually being read.

### 7. Balanced Visual (Snapdragon) manually tuned toward visuals
Per request, nudged texture quality, post-process quality, mip bias, ambient occlusion quality, foliage/grass density, and mesh LOD distance upward, while deliberately leaving shadow quality, effects quality, and anti-aliasing untouched — keeping it inside "balanced" rather than drifting into High-End territory. This is a manual adjustment, not sourced from any repo.

### 8. 3.7 settings retune (generator-based)
All eight tiers were re-derived with Arglax's [DeviceProfiles.ini and Engine.ini generators](https://arglax.github.io/Mobile-WuWa-Config/tools/devprof-generator.html), using one representative device per tier, and the chosen values were tracked in a per-tier settings sheet.

| Folder | Tier | Device selected | GPU reference | Engine.ini mode |
|---|---|---|---|---|
| Snapdragon | High End | OnePlus 12 (`Android_Adreno_750`) | Adreno 750 (SD 8 Gen 3) | High Quality |
| Snapdragon | Balanced Visual | Poco F5 | Adreno 735 (SD 7s Gen 3) | Balanced |
| Snapdragon | Balanced Performance | Poco X5 Pro 5G | Adreno 660 (SD 888) | Performance |
| Snapdragon | Low End | Oppo A96 4G | Adreno 660 (SD 888) | Ultra Performance |
| All Devices | High End | Vivo X200 Pro | Mali G715 MC11 (Dimensity 9300) | High Quality |
| All Devices | Balanced Visual | Poco X7 Pro | Mali G615 MC6 | Balanced |
| All Devices | Balanced Performance | Redmi Note 12 Pro 5G | Generic Android | Performance |
| All Devices | Low End | Redmi 13C | Generic Android | Ultra Performance |

- **Scalability groups (`sg.*`):** one ladder across both folders. View Distance / Anti-Aliasing / Post Process / Shading are 3, 3, 2, 1 from High End down to Low End. Shadow is 3, 2, 2, 1. Foliage is 3, 2, 2, 1. Texture is 4, 3, 2, 1. **Effects is capped at 2 in every tier** (values above 2 crash the game) and is 1 on Low End.
- **Shadow consistency:** Engine.ini shadow quality and cascade count are set to match the `sg.ShadowQuality` value in `DeviceProfiles.ini`, since Engine.ini overrides DeviceProfiles on the same CVar.
- **Vulkan:** forced on for Snapdragon High End and Balanced Visual. Left at the default on the other tiers, since OpenGL ES is the safer default on budget chips.
- **Frame Generation:** KuroFI is on for Snapdragon High End, "test first" on Snapdragon Balanced Visual and Balanced Performance, and off on both Low End tiers. On All Devices it is off by default because of known KuroFI init failures on some MediaTek chipsets. FSR3 Frame Interpolation is off in every tier, since it conflicts with KuroFI.
- **Upscaling:** SGSR2 is off on all All Devices tiers (not optimal on Mali) and off on Snapdragon High End (pointless at native resolution).
- **Always off in every tier:** depth of field, lens flares, motion blur, contact shadows, HDR swapchain, GPU crash debug logging, robust buffer access, and the Vulkan validation layer.
- **Thermal limit removal** (`r.DontLimitOnBattery`) is off by default. It is treated as an optional user toggle on High End only, because of the extra heat and battery drain.
- **Device Score spoofing** is left off; the 3.6 `dp.Override` structure already assigns the profile directly.
- **Numeric values left as-is:** `r.StaticMeshLODDistanceScale`, skeletal LOD bias and the streaming range scale were kept from the existing tested files rather than re-guessed.

**Not verified:** the device-to-chip matching and the generator's `DeviceProfile` names (only `Android_Adreno_750` was confirmed on screen), the starting quick presets (Eye Candy / Balanced / Smooth 60), the resolution-scale steps on Balanced Performance and Low End, and the experimental toggles (shader pre-compilation hint, Async Compute, Big.LITTLE affinity). Confirm the active profile in `Client.log` after installing.

---

## ⚠️ Known Issues Left As-Is

These were flagged during review but **not** silently resolved, since guessing the "correct" value risks being wrong in the opposite direction:

**Engine.ini vs. DeviceProfiles.ini conflicts** (same CVar, different value, in different files — priority between the two isn't consistently documented upstream):

| Tier | CVar(s) | Engine.ini | DeviceProfiles.ini |
|---|---|---|---|
| All Devices Balanced Visual | `foliage.DensityScale` | 0.5 | 1.0 |
| | `r.StaticMeshLODDistanceScale` | 1.0 | 0.8 |
| All Devices High End | `r.LightShaftNumSamples` | 16 | 12 (in-file, different section) |
| | `r.LightShaftQuality` | 1 | 2 (in-file, different section) |
| | `r.Mobile.WaterSSRStep` | 32 | 128 (in-file, different section) |
| | `wp.Runtime.LoadingRangeScale`/`PlannedLoadingRangeScale` | 0.8 / 1.1 | 0.85 / 1.05 |
| Snapdragon Balanced Visual | `foliage.DensityScale` | 0.5 | 1.4 (post-tuning) |
| | `r.StaticMeshLODDistanceScale` | 1.0 | 0.6 (post-tuning) |
| Snapdragon High End | `r.StaticMeshLODDistanceScale` | 0.95 | 0.5 |

**Unverified CVars carried forward** (plausible, not confirmed against any tested reference — watch closely if you install):
- `r.GSR.Enabled` (Snapdragon tiers) — Qualcomm's GSR upscaler plugin exists in-engine, but no `r.GSR.*` CVar is confirmed in any reference source.
- `r.PSO.LRUCapacity` — plausible shader-cache CVar, not seen in any reference file.
- `fx.Niagara.QualityLevel` (Balanced Visual and up) — not confirmed in current-gen tiers.

**VRS is disabled by default** on Balanced Visual and High End (both folders). Left as commented-out lines using the actual deprecated CVar names (`r.VRS.EnableImage`, `r.VRS.ContrastAdaptiveShading`) rather than the commonly-requested-but-nonexistent `r.VRS.EnableMaterial`/`r.VRS.EnableMesh`, in case you want to test separately at your own risk.

**Minor naming oddities noted, not changed:**
- All Devices High End: `r.Kuro.Foliage.MobileSuperFarCullDistanceMax` equals `MobileFarCullDistanceMax` exactly (15000) — "Super Far" usually should exceed "Far."
- Snapdragon High End: `r.Kuro.Foliage.MobileNearCullDistanceMax` equals `MobileMiddleCullDistanceMax` exactly (15000) — same pattern.
- Snapdragon High End: `r.Kuro.KuroBloomStreak=0`, down from `1` at Balanced Visual — bloom streak effectively turns off going up a tier, which reads backwards but may be intentional (bloom streak can look overblown at high internal resolution).

---

## ⚠️ Important Warning

> These configs are provided as-is. Choosing the wrong preset — or a config with an unresolved conflict above — may cause:
> - Reduced performance
> - Overheating
> - Increased battery drain
> - Visual issues
> - Game instability
>
> Always back up your original configuration files before replacing anything.

---

## 🙏 Credits

- **Arglax** — [Mobile-WuWa-Config](https://github.com/Arglax/Mobile-WuWa-Config), primary source for the All Devices tiers and the 3.6 `dp.Override` restructure.
- **AlteriaX** — Command reference, documentation, and the archived config methodology much of the Snapdragon-tier tuning style is built on.
- **Kuro Game** — Wuthering Waves.
- Compilation, cross-tier auditing, bug fixes, and this README by the maintainer of this personal build.

---

## 📖 Further Reading

- Command reference: https://alteriax.github.io/WuWa-Config-Info/
- Arglax's repo (source for All Devices / structural changes): https://github.com/Arglax/Mobile-WuWa-Config