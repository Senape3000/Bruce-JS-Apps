<p align="center">
  <img src="logo.png" width="128" height="128" alt="BruteRF Logo"/>
</p>

<h1 align="center">BruteRF</h1>

<p align="center">
  <strong>Complete RF Brute-Force Tool for Bruce Firmware</strong><br/>
  <em>34 protocols &bull; 7 categories &bull; De Bruijn attack &bull; RAW mode &bull; Responsive UI</em>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/version-1.0.0-blue?style=flat-square" alt="Version"/>
  <img src="https://img.shields.io/badge/protocols-34-green?style=flat-square" alt="Protocols"/>
  <img src="https://img.shields.io/badge/categories-7-orange?style=flat-square" alt="Categories"/>
  <img src="https://img.shields.io/badge/platform-Bruce_1.4+-purple?style=flat-square" alt="Platform"/>
  <img src="https://img.shields.io/badge/language-JavaScript-yellow?style=flat-square" alt="Language"/>
</p>

---

## Overview

BruteRF is a comprehensive RF brute-force tool written in JavaScript for **Bruce Firmware 1.4+**. It replaces the firmware's built-in `rf_bruteforce.cpp` with a more feature-rich external JS app, supporting **34 protocols** across **7 categories** with multiple attack modes.

Responsive layout system supports **6 screen resolutions** (240x135, 240x240, 320x170, 320x240, 480x222, 480x320) covering **18 devices**.

---

## Features

| Feature | Description |
|---------|-------------|
| **34 Protocols** | All ECRF-bruter protocols ported to JS (100% timing match) |
| **7 Categories** | EU Garage, US Garage, Home Auto, Alarm, 868 MHz, Misc, ALL |
| **Binary Brute-Force** | Sequential code enumeration with progress tracking |
| **Tristate Brute-Force** | Tristate code enumeration (0, 1, F states) |
| **De Bruijn Attack** | B(2,n) sequence — covers all n-bit windows in minimal transmissions |
| **Universal Sweep** | Sweep across all codes for any protocol |
| **RAW Brute-Force** | Hex-value brute-force via `subghz.transmit()` API |
| **Pause Mode** | Pause during attack: -1/+1 navigate codes, Replay, Save, Resume |
| **Save .sub Files** | Export current code as `.sub` file (SD card with LittleFS fallback) |
| **Responsive Layout** | Adaptive UI for all screen sizes (240x135 to 480x320) |
| **Protocol Categories** | Graphic icons for each category |
| **Progress Tracking** | Real-time progress bar, speed (codes/s), ETA |

---

## Supported Protocols

### EU Garage Doors
Ansonic, BETT, Came, Came-TWEE, Doorhan, Faac SLH, GateTX, Holtek HT12X, NICE FLO, NICE-Smilo, Princeton

### US Garage Doors
Chamberlain, Genie, Linear, LiftMaster, Stanley

### Home Automation
Holtek, CAME-Atomo, Somfy Telis

### Alarm Systems
Honeywell, GE Security, Ademco, Visonic

### 868 MHz
Marantec, Hörmann, Sommer, Tedsen

### Miscellaneous
Additional protocols and variations

---

## Installation

### From Bruce App Store (Recommended)
Install directly from the **Bruce App Store** on your device.

### Manual — SD Card
Copy `BruteRF.js` to your SD card:
```
/BruceJS/RF/BruteRF.js
```

Then on your device: **Others** → **JS Interpreter** → select the file.

---

## Usage

### Controls

| Button | Action |
|--------|--------|
| **PREV** (↑) | Navigate up / Previous option |
| **NEXT** (↓) | Navigate down / Next option |
| **SEL** (●) | Select / Confirm / Pause attack |
| **ESC** (←) | Back / Cancel |

### Main Menu

| Menu Item | Description |
|-----------|-------------|
| **Select Protocol** | Browse protocols by category |
| **Quick Attack** | Start brute-force on selected protocol |
| **De Bruijn Attack** | B(2,n) optimized attack |
| **Universal Sweep** | Sweep all codes |
| **RAW Bruteforce** | Hex-based brute-force with configurable parameters |
| **Settings** | Configure attack parameters |
| **Exit** | Return to Bruce menu |

### RAW Brute-Force Settings

| Setting | Description | Default |
|---------|-------------|---------|
| Prefix | Hex prefix for codes | 0x445700 |
| Range Bits | Bits to brute-force | 8 |
| Delay | Inter-code delay (ms) | 200 |
| Frequency | TX frequency (Hz) | 433920000 |
| TE | Timing element (µs) | 174 |
| TX Count | Transmissions per code | 10 |

### Pause Mode

During any attack, press **SEL** to pause. In pause mode:
- **-1 Code** / **+1 Code**: Navigate through codes (auto-transmit)
- **Replay**: Retransmit current code
- **Save .sub**: Export current code as `.sub` file
- **Resume**: Continue attack
- **Cancel**: Abort attack

---

## Technical Details

- **De Bruijn**: Pure JS "prefer-ones" greedy algorithm generating B(2,n) sequences
- **Pulse encoding**: Direct CC1101 bitbanging via `subghz.txSetup()` / `subghz.txPulses()` / `subghz.txEnd()`
- **RAW mode**: Uses high-level `subghz.transmit()` API
- **Layout system**: ~95 computed properties from screen dimensions, baseline 320x170
- **Memory efficient**: Runs from SD card, 0 firmware Flash used

---

## Legal Notice

> **WARNING**: This software is for **educational and authorized security research only**.
>
> - Transmitting RF signals without authorization may be **illegal**
> - Only use on devices you **own** or have **explicit written permission** to test
> - You are solely responsible for complying with all applicable laws
> - The authors assume no liability for misuse

---

## Credits

- **ECRF-bruter**: Protocol database and timing reference
- **Bruce Firmware**: [@pr3y](https://github.com/pr3y), [@bmorcelli](https://github.com/bmorcelli), [@IncursioHack](https://github.com/IncursioHack)
- **Author**: [@Senape3000](https://github.com/Senape3000)

---

## Version History

### v1.0.0 — Initial Release
- 34 protocols across 7 categories with graphic icons
- Binary, Tristate, De Bruijn, and Universal Sweep attack modes
- RAW Bruteforce mode with configurable parameters
- Pause mode with code navigation, replay, and .sub saving
- Progress bar with speed and ETA tracking
- Responsive layout for 6 screen resolutions (18 devices)
- Firmware bug fix: Chamberlain now uses correct timings (not Ansonic)
