# OBD-II Connector Pinout Diagram

```
          ╔═══════════════════════════════════════╗
          ║     OBD-II 16-PIN CONNECTOR (J1962)   ║
          ║                                       ║
          ║    ┌───┬───┬───┬───┬───┬───┬───┬───┐  ║
          ║    │ 1 │ 2 │ 3 │ 4 │ 5 │ 6 │ 7 │ 8 │  ║
          ║    └───┴───┴───┴───┴───┴───┴───┴───┘  ║
          ║    ┌───┬───┬───┬───┬───┬───┬───┬───┐  ║
          ║    │ 9 │10 │11 │12 │13 │14 │15 │16 │  ║
          ║    └───┴───┴───┴───┴───┴───┴───┴───┘  ║
          ╚═══════════════════════════════════════╝
```

## Pin Assignments

| Pin | Signal | Description | Color |
|-----|--------|-------------|-------|
| 1 | - | Manufacturer Specific | - |
| 2 | J1850+ | J1850 Bus Positive | Orange |
| 3 | - | Manufacturer Specific | - |
| 4 | CGND | Chassis Ground | Black |
| 5 | SGND | Signal Ground | Black |
| 6 | CAN-H | CAN High (ISO 15765) | Green |
| 7 | K-Line | ISO 9141-2 K-Line | Red |
| 8 | - | Manufacturer Specific | - |
| 9 | - | Manufacturer Specific | - |
| 10 | J1850- | J1850 Bus Negative | Yellow |
| 11 | - | Manufacturer Specific | - |
| 12 | - | Manufacturer Specific | - |
| 13 | - | Manufacturer Specific | - |
| 14 | CAN-L | CAN Low (ISO 15765) | Brown |
| 15 | L-Line | ISO 9141-2 L-Line | Blue |
| 16 | VBAT | Battery Power (+12V) | Red |

## Protocol Detection by Pin

### CAN Bus (Most Modern Vehicles 2008+)
- Pins 6 & 14: CAN High & CAN Low
- Speed: 250 kbps or 500 kbps

### K-Line (Older European/Asian)
- Pin 7: K-Line (bidirectional)
- Pin 15: L-Line (initialization only)
- Speed: 10.4 kbps

### J1850 PWM (Ford)
- Pins 2 & 10: J1850 Bus +/-
- Speed: 41.6 kbps

### J1850 VPW (GM)
- Pin 2: J1850 Bus +
- Speed: 10.4 kbps

---

## Vehicle-Specific Pins (Manufacturer Pins)

### Ford (Pins 1, 3, 11, 13)
| Pin | Signal |
|-----|--------|
| 1 | MS-CAN High |
| 3 | MS-CAN Low |
| 11 | HS-CAN High (Secondary) |
| 13 | Battery Power (Secondary) |

### GM (Pins 1, 3, 8, 9, 12)
| Pin | Signal |
|-----|--------|
| 1 | GMLAN (Single Wire CAN) |
| 3 | ALDL Serial Data |
| 8 | LS-CAN High |
| 9 | LS-CAN Low |
| 12 | GMLAN (Secondary) |

### Chrysler/Dodge/Jeep (Pins 3, 11, 12, 13)
| Pin | Signal |
|-----|--------|
| 3 | CCD Bus + |
| 11 | CCD Bus - |
| 12 | SCI Receive |
| 13 | SCI Transmit |

### BMW/Mercedes (Pins 1, 3, 8, 9, 12)
| Pin | Signal |
|-----|--------|
| 1 | D-CAN Low |
| 3 | D-CAN High |
| 8 | PT-CAN Low |
| 9 | PT-CAN High |
| 12 | K-Line Secondary |

### Toyota/Lexus (Pins 1, 3, 9, 12, 13)
| Pin | Signal |
|-----|--------|
| 1 | Manufacturer Reserved |
| 3 | AVC-LAN |
| 9 | CAN-H (Body) |
| 12 | CAN-L (Body) |
| 13 | TC Signal |

---

*BlackFlag ECU - Wiring Reference v2.1*
