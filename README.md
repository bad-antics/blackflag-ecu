# 🏴 BlackFlag ECU - Professional Automotive Diagnostic & Tuning Suite

<div align="center">

**Advanced ECU Diagnostics | Performance Tuning | Real-Time Data Analysis**

[![.NET 8.0](https://img.shields.io/badge/.NET-8.0-512BD4)](https://dotnet.microsoft.com/)
[![Platform](https://img.shields.io/badge/platform-Windows-0078D4)](https://www.microsoft.com/windows)
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)
[![Built by](https://img.shields.io/badge/Built%20by-Bad%20Antics%20Development-orange)](https://github.com/bad-antics)

</div>

---

## 🚀 Overview

**BlackFlag ECU** is a comprehensive, native Windows application for automotive diagnostics, ECU tuning, and performance optimization. Built with C# and WPF on .NET 8.0, it provides professional-grade tools for mechanics, tuners, and automotive enthusiasts.

### ✨ Key Features

- **🔍 ECU Scanner** - Scan and identify ECU types across all major manufacturers
- **🔓 ECU Unlock** - Unlock write-protection on supported processors (Tricore, MPC5xx, SH7xxx)
- **📊 Live Data** - Real-time voltage meter and diagnostic data streaming
- **🎯 VIN Decoder** - Comprehensive vehicle identification and specs lookup
- **🔌 Wiring Diagrams** - Interactive pinout diagrams for connectors and modules
- **⚡ Tune Manager** - Create, edit, and flash custom ECU tunes
- **💾 ECU Cloning** - Backup and restore complete ECU configurations
- **📈 Performance Dashboard** - Real-time charts for horsepower, torque, boost, and AFR

---

## 📋 System Requirements

- **OS:** Windows 10/11 (64-bit)
- **.NET:** .NET 8.0 Runtime (included in standalone build)
- **RAM:** 4GB minimum, 8GB recommended
- **Storage:** 200MB available space
- **Hardware:** J2534-compatible interface (for live diagnostics)

---

## 🔧 Installation

### Standalone Executable

1. Download `BlackFlag.exe` from the [Releases](https://github.com/bad-antics/blackflag-ecu/releases) page
2. Run `BlackFlag.exe` - No installation required
3. All dependencies are included in the single-file executable

### First Launch

On first launch, BlackFlag will create the following directories:
```
%LOCALAPPDATA%\BlackFlag\
├── vehicles.json     # Vehicle database
├── history.json      # Scan/tune history
├── ecuprofiles.json  # ECU profile library
├── tunes.json        # Custom tune library
└── settings.json     # Application settings
```

---

## 🎯 Quick Start Guide

### 1. Dashboard
The main dashboard provides quick access to all features and displays recent activity.

### 2. VIN Decoder
- Enter a 17-character VIN
- Instantly retrieve vehicle specs (make, model, year, engine, transmission)
- View supported ECU types and systems

### 3. ECU Scanner
- Connect J2534 interface to OBD-II port
- Select communication protocol (CAN, K-Line, J1850)
- Click **Scan** to identify ECU type and software version
- View live diagnostic codes

### 4. Tune Manager
- Load stock ECU file
- Modify parameters (boost, timing, fuel, rev limit)
- Preview changes in real-time
- Flash to ECU with progress tracking

### 5. ECU Unlock
- Select processor vendor (Infineon, NXP/Freescale, Renesas, STMicroelectronics)
- Choose specific processor model
- Click **Unlock** to disable write protection
- Monitor unlock progress

---

## 📊 Features Overview

### ECU Support

**Supported Manufacturers:**
- Bosch (EDC17, MED17, ME17, MD1)
- Denso
- Continental
- Delphi
- Magneti Marelli
- Siemens/Continental
- Hitachi
- OEM-specific ECUs (Ford, GM, Chrysler, etc.)

**Supported Processors:**
- Infineon Tricore (TC1766, TC1796, TC1797, TC1798)
- NXP/Freescale MPC5xx (MPC5534, MPC5554, MPC5566)
- Renesas SH7xxx (SH7058, SH7059, SH72531)
- STMicroelectronics ST10

### Communication Protocols

- **CAN Bus** (ISO 15765, High/Mid/Low Speed)
- **K-Line** (ISO 9141, ISO 14230 KWP2000)
- **J1850 PWM/VPW**
- **LIN Bus**
- **FlexRay** (read-only)

### Diagnostic Features

- **DTC Reading** - Read and clear diagnostic trouble codes
- **Live Data** - Real-time sensor values (O2, MAF, MAP, IAT, ECT, TPS, etc.)
- **Freeze Frame** - Capture engine state at fault occurrence
- **Oxygen Sensor Tests** - Monitor O2 heater and response
- **EVAP Tests** - Leak detection and purge valve control
- **Readiness Monitors** - Emissions system readiness status

---

## 🎨 Themes

BlackFlag includes 4 professionally designed themes:

1. **Dark Theme** - Modern dark mode (default)
2. **Retro Green Theme** - Classic terminal aesthetic
3. **Ford Blue Theme** - OEM Ford blue styling
4. **Orange Tech Theme** - High-contrast orange accents

Switch themes from **Dashboard → Theme Selector**

---

## 🛠️ Technical Details

### Architecture

- **Framework:** .NET 8.0 Windows Desktop
- **UI:** WPF (Windows Presentation Foundation)
- **Charts:** LiveChartsCore v2.0.0-rc2
- **Serial:** System.IO.Ports
- **JSON:** Newtonsoft.Json
- **Size:** 155.56 MB (standalone executable)

### Data Storage

All data is stored in JSON format in `%LOCALAPPDATA%\BlackFlag\`:
- **vehicles.json** - 900+ vehicle database entries
- **ecuprofiles.json** - ECU configuration profiles
- **tunes.json** - Custom tune files
- **history.json** - Scan and flash history

---

## 🔒 Security & Legal

### Safety Features

- **Read-Only Mode** - Preview ECU data without modification
- **Backup Before Flash** - Automatic ECU backup before any write operation
- **Checksum Validation** - Verify tune file integrity before flashing
- **Live Monitoring** - Abort flash if voltage drops or connection lost

### Legal Notice

**BlackFlag ECU is intended for off-road use, racing, and professional tuning only.**

- Modifying emissions-related systems may violate local laws
- Users are responsible for compliance with EPA, CARB, and local regulations
- Warranty on modified vehicles may be voided
- Use at your own risk

---

## 📝 License

MIT License - Free and Open Source

```
Copyright (c) 2025 Bad Antics Development

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

## 🤝 Support

- **Issues:** [GitHub Issues](https://github.com/bad-antics/blackflag-ecu/issues)
- **Discussions:** [GitHub Discussions](https://github.com/bad-antics/blackflag-ecu/discussions)
- **Author:** Built by antx @ Bad Antics Development

---

## 🚀 Version History

### v2.1 (Current)
- Initial standalone release
- 155.56 MB single-file executable
- 900+ vehicle database
- 4 premium themes
- Full J2534 support
- ECU unlock for Tricore, MPC5xx, SH7xxx processors

---

<div align="center">

**🏴 BlackFlag ECU - Professional Automotive Power**

*Built by [Bad Antics Development](https://github.com/bad-antics)*

</div>
