# OBD-II Connector Pinout Reference

## J1962 16-Pin Connector Layout

```
    Female Connector (Vehicle Side) - Looking into port
    
         1    2    3    4    5    6    7    8
        [o]  [o]  [o]  [o]  [o]  [o]  [o]  [o]
        [o]  [o]  [o]  [o]  [o]  [o]  [o]  [o]
         9   10   11   12   13   14   15   16
```

## Standard Pin Assignments

| Pin | Signal | Description | Protocol |
|:---:|--------|-------------|----------|
| 1 | MFG | Manufacturer Specific | Varies |
| 2 | J1850+ | J1850 Bus Positive | PWM/VPW |
| 3 | MFG | Manufacturer Specific | Varies |
| 4 | CGND | Chassis Ground | - |
| 5 | SGND | Signal Ground | - |
| 6 | CAN-H | CAN High | ISO 15765 |
| 7 | K-LINE | ISO K-Line | ISO 9141 |
| 8 | MFG | Manufacturer Specific | Varies |
| 9 | MFG | Manufacturer Specific | Varies |
| 10 | J1850- | J1850 Bus Negative | PWM |
| 11 | MFG | Manufacturer Specific | Varies |
| 12 | MFG | Manufacturer Specific | Varies |
| 13 | MFG | Manufacturer Specific | Varies |
| 14 | CAN-L | CAN Low | ISO 15765 |
| 15 | L-LINE | ISO L-Line | ISO 9141 |
| 16 | VBAT | Battery +12V | Power |

---

## Protocol Detection

**CAN Bus (2008+ vehicles)**
- Pins 6 + 14 = CAN-H / CAN-L
- Speed: 250 or 500 kbps

**K-Line (Pre-2008 European/Asian)**
- Pin 7 = K-Line (bidirectional)
- Pin 15 = L-Line (init only)
- Speed: 10.4 kbps

**J1850 PWM (Ford pre-2008)**
- Pins 2 + 10 = Bus +/-
- Speed: 41.6 kbps

**J1850 VPW (GM pre-2008)**
- Pin 2 only = Bus +
- Speed: 10.4 kbps

---

## Manufacturer-Specific Pins

### Ford
| Pin | Function |
|:---:|----------|
| 1 | MS-CAN High |
| 3 | MS-CAN Low |
| 11 | HS-CAN High (Secondary) |
| 13 | Battery (Secondary) |

### GM
| Pin | Function |
|:---:|----------|
| 1 | GMLAN (SW-CAN) |
| 3 | ALDL Serial |
| 8 | LS-CAN High |
| 9 | LS-CAN Low |
| 12 | GMLAN Secondary |

### Stellantis (Chrysler/Dodge/Jeep)
| Pin | Function |
|:---:|----------|
| 3 | CCD Bus + |
| 11 | CCD Bus - |
| 12 | SCI Receive |
| 13 | SCI Transmit |

### BMW / Mercedes
| Pin | Function |
|:---:|----------|
| 1 | D-CAN Low |
| 3 | D-CAN High |
| 8 | PT-CAN Low |
| 9 | PT-CAN High |
| 12 | K-Line Secondary |

### Toyota / Lexus
| Pin | Function |
|:---:|----------|
| 3 | AVC-LAN |
| 9 | Body CAN-H |
| 12 | Body CAN-L |
| 13 | TC Signal |

---

*BlackFlag ECU - OBD-II Reference v2.2*
