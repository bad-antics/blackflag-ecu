# Bench Flash & Boot Mode Harness Diagrams

## Universal Bench Flash Harness

```
                              ┌─────────────────┐
                              │   J2534 Device  │
                              │  (PassThru API) │
                              └────────┬────────┘
                                       │
                                 USB / Ethernet
                                       │
                              ┌────────┴────────┐
                              │    PC / Laptop  │
                              │  + Flash Tool   │
                              └────────┬────────┘
                                       │
                    ┌──────────────────┼──────────────────┐
                    │                  │                  │
                    ▼                  ▼                  ▼
           ┌──────────────┐   ┌──────────────┐   ┌──────────────┐
           │   CAN BUS    │   │    K-LINE    │   │   BDM/JTAG   │
           │   Adapter    │   │   Adapter    │   │   Adapter    │
           └──────┬───────┘   └──────┬───────┘   └──────┬───────┘
                  │                  │                  │
    ┌─────────────┴─────────────┐    │    ┌─────────────┴─────────────┐
    │                           │    │    │                           │
   CAN_H                     CAN_L   K   BDM                       GND
    │                           │    │    │                           │
    └───────────────────────────┴────┴────┴───────────────────────────┘
                                     │
                              ┌──────┴──────┐
                              │     ECU     │
                              │  (On Bench) │
                              └─────────────┘
```

---

## Bosch ME7/MED9 Boot Mode Wiring

```
                    ECU Connector (Top View)
    ┌─────────────────────────────────────────────────────────┐
    │                                                         │
    │   [1]   [2]   [3]   [4]   [5]   [6]   [7]   [8]   [9]   │
    │    ○     ○     ○     ○     ○     ○     ○     ○     ○    │
    │                                                         │
    │   [10]  [11]  [12]  [13]  [14]  [15]  [16]  [17]  [18]  │
    │    ○     ○     ○     ○     ○     ○     ○     ○     ○    │
    │                                                         │
    │   [19]  [20]  [21]  [22]  [23]  [24]  [25]  [26]  [27]  │
    │    ○     ○     ○     ○     ○     ○     ○     ○     ○    │
    │                                                         │
    └─────────────────────────────────────────────────────────┘

    BOOT MODE PINS:
    ┌─────────────────────────────────────────────────────────┐
    │  Pin   │  Function       │  Connection                  │
    ├────────┼─────────────────┼──────────────────────────────┤
    │   1    │  BATT+          │  +12V (Battery)              │
    │   2    │  BATT+          │  +12V (Battery)              │
    │   4    │  IGN+           │  +12V (Ignition)             │
    │   6    │  K-LINE         │  K-LINE Adapter              │
    │   9    │  GND            │  Ground                      │
    │   18   │  GND            │  Ground                      │
    │   27   │  GND            │  Ground                      │
    │   15   │  BOOT (BSL)     │  Pull to GND via 1kΩ         │
    └────────┴─────────────────┴──────────────────────────────┘

    BOOT MODE SEQUENCE:
    1. Connect GND first
    2. Pull BOOT pin to GND via 1kΩ resistor
    3. Apply +12V to BATT pins
    4. Apply +12V to IGN pin
    5. Wait 500ms
    6. Start boot mode communication
```

---

## Siemens/Continental Tricore Boot

```
                    154-Pin ECU Connector
    ┌────────────────────────────────────────────────────────────────────┐
    │   A1  A2  A3  A4  A5  A6  A7  A8  A9  A10 A11 A12 A13 A14 A15 A16  │
    │   ○   ○   ○   ○   ○   ○   ○   ○   ○   ○   ○   ○   ○   ○   ○   ○   │
    │   B1  B2  B3  B4  B5  B6  B7  B8  B9  B10 B11 B12 B13 B14 B15 B16  │
    │   ○   ○   ○   ○   ○   ○   ○   ○   ○   ○   ○   ○   ○   ○   ○   ○   │
    │   C1  C2  C3  C4  C5  C6  C7  C8  C9  C10 C11 C12 C13 C14 C15 C16  │
    │   ○   ○   ○   ○   ○   ○   ○   ○   ○   ○   ○   ○   ○   ○   ○   ○   │
    │   D1  D2  D3  D4  D5  D6  D7  D8  D9  D10 D11 D12 D13 D14 D15 D16  │
    │   ○   ○   ○   ○   ○   ○   ○   ○   ○   ○   ○   ○   ○   ○   ○   ○   │
    └────────────────────────────────────────────────────────────────────┘

    TRICORE BOOT PINS (Typical):
    ┌─────────────────────────────────────────────────────────┐
    │  Pin   │  Function       │  Boot Mode                   │
    ├────────┼─────────────────┼──────────────────────────────┤
    │  A1    │  VBATT+         │  +12V Power                  │
    │  A2    │  VBATT+         │  +12V Power                  │
    │  A9    │  GND            │  Chassis Ground              │
    │  A10   │  GND            │  Signal Ground               │
    │  B3    │  CAN-H          │  500 kbps High               │
    │  B4    │  CAN-L          │  500 kbps Low                │
    │  C7    │  BOOT_CFG0      │  Pull HIGH (3.3V)            │
    │  C8    │  BOOT_CFG1      │  Pull LOW (GND)              │
    │  D12   │  HWCFG          │  Ground for ASC Boot         │
    │  D14   │  ESR0           │  External Reset              │
    └────────┴─────────────────┴──────────────────────────────┘

    BOOT MODES:
    ┌────────────────┬────────────┬────────────┬───────────────┐
    │  BOOT_CFG0     │ BOOT_CFG1  │   HWCFG    │  Boot Mode    │
    ├────────────────┼────────────┼────────────┼───────────────┤
    │     HIGH       │    LOW     │    GND     │  ASC (Serial) │
    │     HIGH       │    HIGH    │    GND     │  CAN Boot     │
    │     LOW        │    LOW     │    Open    │  Internal Fls │
    │     LOW        │    HIGH    │    Open    │  External Fls │
    └────────────────┴────────────┴────────────┴───────────────┘
```

---

## BDM Connection for Motorola/Freescale MPC5xx

```
    ┌─────────────────────────────────────────────────────────┐
    │              BDM CONNECTOR (10-PIN)                     │
    │                                                         │
    │           ┌───┬───┬───┬───┬───┐                         │
    │           │ 1 │ 2 │ 3 │ 4 │ 5 │                         │
    │           ├───┼───┼───┼───┼───┤                         │
    │           │ 6 │ 7 │ 8 │ 9 │10 │                         │
    │           └───┴───┴───┴───┴───┘                         │
    │                                                         │
    │   PIN ASSIGNMENTS:                                      │
    │   ┌──────┬────────────────────┬────────────────────┐    │
    │   │ Pin  │ Signal             │ Description        │    │
    │   ├──────┼────────────────────┼────────────────────┤    │
    │   │  1   │ BKPT/DSDI          │ Breakpoint Input   │    │
    │   │  2   │ GND                │ Ground             │    │
    │   │  3   │ DSDO               │ Data Out           │    │
    │   │  4   │ VDD                │ Target Voltage Ref │    │
    │   │  5   │ N/C                │ Not Connected      │    │
    │   │  6   │ N/C                │ Not Connected      │    │
    │   │  7   │ RESET              │ Reset Line         │    │
    │   │  8   │ N/C                │ Not Connected      │    │
    │   │  9   │ DSCLK              │ Debug Clock        │    │
    │   │ 10   │ VPP                │ Flash Program Volt │    │
    │   └──────┴────────────────────┴────────────────────┘    │
    │                                                         │
    └─────────────────────────────────────────────────────────┘

    WIRING TO ECU:
    ┌─────────────────────────────────────────────────────────────────┐
    │                                                                 │
    │   BDM Adapter                ECU Board                          │
    │   ┌─────────┐                ┌─────────────────────────────┐    │
    │   │ DSDI ○──┼────────────────┼──○ BKPT/DSDI                │    │
    │   │ DSDO ○──┼────────────────┼──○ TDO                      │    │
    │   │ DSCLK○──┼────────────────┼──○ TCK                      │    │
    │   │ RESET○──┼────────────────┼──○ RESET                    │    │
    │   │ VDD  ○──┼────────────────┼──○ 3.3V/5V                  │    │
    │   │ GND  ○──┼────────────────┼──○ GND                      │    │
    │   │ VPP  ○──┼───[Use ONLY for│flash erase if needed]       │    │
    │   └─────────┘                └─────────────────────────────┘    │
    │                                                                 │
    └─────────────────────────────────────────────────────────────────┘
```

---

## Power Supply Requirements

```
    ┌─────────────────────────────────────────────────────────────────┐
    │                   BENCH POWER SUPPLY SETUP                      │
    ├─────────────────────────────────────────────────────────────────┤
    │                                                                 │
    │      ┌─────────────────┐                                        │
    │      │  Lab PSU        │                                        │
    │      │  13.8V / 10A    │                                        │
    │      │  Adjustable     │                                        │
    │      └───────┬─────────┘                                        │
    │              │                                                  │
    │       ┌──────┴──────┐                                           │
    │       │   +    -    │                                           │
    │       │   │    │    │                                           │
    │       │   │    │    │                                           │
    │   ┌───┴───┘    └────┴───┐                                       │
    │   │                     │                                       │
    │   │  ┌───────────────┐  │                                       │
    │   └──┤ Fuse (5-10A)  ├──┤                                       │
    │      └───────────────┘  │                                       │
    │                         │                                       │
    │   TO ECU:               │                                       │
    │   ┌─────────────────────┴─────────────────────┐                 │
    │   │  BATT+  ──── +13.8V (through fuse)        │                 │
    │   │  IGN+   ──── +13.8V (switched)            │                 │
    │   │  GND    ──── PSU GND (multiple points)    │                 │
    │   │  CAN-H  ──── 120Ω terminated              │                 │
    │   │  CAN-L  ──── 120Ω terminated              │                 │
    │   └───────────────────────────────────────────┘                 │
    │                                                                 │
    │   CRITICAL NOTES:                                               │
    │   • Always use fused power connections                          │
    │   • Current limit PSU to 5A initially                           │
    │   • Monitor current draw (idle: 0.5-2A typical)                 │
    │   • Use proper CAN termination (120Ω each end)                  │
    │   • Ground all GND pins for stable operation                    │
    │                                                                 │
    └─────────────────────────────────────────────────────────────────┘
```

---

## Safety Checklist

⚠️ **BEFORE POWERING ECU:**
- [ ] Verify all ground connections are secure
- [ ] Confirm power polarity is correct
- [ ] Set current limit on power supply
- [ ] Install inline fuse on BATT+ line
- [ ] Double-check boot mode pin configurations
- [ ] Ensure CAN bus is properly terminated
- [ ] Have fire extinguisher accessible

---

*BlackFlag ECU - Bench Flash Reference v2.1*
