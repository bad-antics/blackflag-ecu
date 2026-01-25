# BlackFlag ECU - Frequently Asked Questions

## General

### What is BlackFlag ECU?
BlackFlag ECU is a professional ECU diagnostics and tuning suite supporting 200+ vehicles across 45 manufacturers. It provides OBD-II scanning, live data monitoring, DTC management, and ECU calibration capabilities.

### Is it free?
Yes, BlackFlag ECU is open source and free to use under the MIT license.

### What vehicles are supported?
We support most 1996+ vehicles with OBD-II compliance, including:
- Domestic: Ford, GM, Chrysler/Stellantis, Tesla
- Japanese: Toyota, Honda, Nissan, Mazda, Subaru, Mitsubishi
- European: BMW, Mercedes, Audi/VW, Porsche, Volvo
- Korean: Hyundai, Kia, Genesis
- And 30+ more manufacturers

## Hardware

### What hardware do I need?
- A J2534 passthru device (recommended: DrewTech, Bosch, Autel)
- Or an ELM327-compatible adapter (limited functionality)
- CANtact/CANable for advanced CAN bus work

### Can I use a cheap ELM327?
Basic OBD-II functions work with ELM327 clones, but for full functionality (ECU flashing, advanced diagnostics), a proper J2534 device is recommended.

### Does it work on Linux?
Yes! Native Linux support with SocketCAN. Also works on Windows and macOS.

## Usage

### How do I connect to my vehicle?
1. Connect your OBD-II adapter to the vehicle's diagnostic port (usually under the dashboard)
2. Start BlackFlag ECU
3. Select your adapter from the connection menu
4. Click "Connect" to establish communication

### Can I damage my vehicle?
Reading data is completely safe. Writing to the ECU (flashing, clearing codes) should only be done if you understand the implications. Always have a backup of your original calibration.

### Why am I getting "Communication Error"?
Common causes:
- Vehicle not powered on (key in "On" position)
- Wrong protocol selected
- Faulty OBD-II adapter
- CAN bus issues (check for DTCs in other modules)

## Tuning

### Can I tune my car with this?
BlackFlag ECU provides the tools to read/write ECU calibrations. Actual tuning requires knowledge of the specific ECU parameters. We provide reference data but recommend professional guidance for significant modifications.

### Will tuning void my warranty?
Modifying ECU calibrations typically voids the powertrain warranty. Many manufacturers can detect reflashes via "Flash Write Counter" parameters.

### Is this legal?
For off-road/competition use only. Street legality varies by jurisdiction. Emissions modifications are federally regulated in the US (Clean Air Act).

## Troubleshooting

### The app won't start
- Ensure you have the required dependencies (see INSTALL.md)
- Check that your adapter drivers are installed
- Try running as administrator/root

### I can't see any PIDs
- Verify the vehicle supports the requested PIDs
- Some manufacturers use non-standard PIDs
- Try different diagnostic modes (Mode 01, 22, etc.)

### DTCs won't clear
- Ensure ignition is in "On" position
- Some DTCs are "permanent" and require drive cycles
- Check for active fault conditions that prevent clearing

## Contributing

### How can I help?
- Add vehicle definitions to the database
- Improve documentation
- Report bugs and issues
- Submit pull requests with fixes or features

### Where do I report bugs?
Open an issue on GitHub: github.com/bad-antics/blackflag-ecu/issues

---

For more help, join our Discord: discord.gg/killers
