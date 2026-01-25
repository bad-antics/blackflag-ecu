# ECU Connector Pinouts

## Bosch MED17/MG1 (154-Pin)

```
Connector Layout (Top View):
    A1  A2  A3  A4  ... A16
    B1  B2  B3  B4  ... B16
    C1  C2  C3  C4  ... C16
    D1  D2  D3  D4  ... D16
    (4 rows x 16 cols = 64 pins per connector)
```

### Critical Pins
| Pin | Function | Notes |
|-----|----------|-------|
| A1-A2 | VBATT | +12V Battery |
| A5-A6 | IGN | Ignition Power |
| A9-A10 | GND | Chassis Ground |
| B3 | CAN-H | 500 kbps |
| B4 | CAN-L | 500 kbps |
| B7 | K-LINE | ISO 9141 |
| C1-C8 | INJ 1-8 | Injector Outputs |
| D1-D8 | IGN 1-8 | Coil Outputs |

---

## Delphi E39A (80-Pin)

```
Connector Layout:
    Row A: 1-20
    Row B: 21-40
    Row C: 41-60
    Row D: 61-80
```

### Critical Pins
| Pin | Function | Notes |
|-----|----------|-------|
| 1-2 | VBATT | +12V Battery |
| 3 | IGN | Ignition Power |
| 19-20 | GND | Chassis Ground |
| 25 | CAN-H | HS-CAN |
| 26 | CAN-L | HS-CAN |
| 45 | SW-CAN | GMLAN |
| 41-48 | INJ | Injector Outputs |
| 61-68 | IGN | Coil Outputs |

---

## Continental SIM2K-260 (128-Pin)

```
Connector Layout:
    Row A: 1-32
    Row B: 33-64
    Row C: 65-96
    Row D: 97-128
```

### Critical Pins
| Pin | Function | Notes |
|-----|----------|-------|
| 1-4 | VBATT | +12V Battery |
| 5-6 | IGN | Ignition Power |
| 31-32 | GND | Chassis Ground |
| 40 | CAN-H | Powertrain |
| 41 | CAN-L | Powertrain |
| 72 | CAN2-H | Body CAN |
| 73 | CAN2-L | Body CAN |
| 65-72 | INJ | Injector Outputs |
| 97-104 | IGN | Coil Outputs |

---

## Denso SH7058 (76-Pin)

```
Connector Layout:
    Row A: 1-19
    Row B: 20-38
    Row C: 39-57
    Row D: 58-76
```

### Critical Pins
| Pin | Function | Notes |
|-----|----------|-------|
| 1-2 | VBATT | +12V Battery |
| 3 | IGN | Key-On Power |
| 18-19 | GND | Chassis Ground |
| 24 | CAN-H | 500 kbps |
| 25 | CAN-L | 500 kbps |
| 39-42 | INJ 1-4 | Injector Outputs |
| 58-61 | IGN 1-4 | Coil Outputs |
| 70 | IAT | Intake Air Temp |
| 71 | MAP | Manifold Pressure |
| 72 | TPS | Throttle Position |

---

## Generic Pin Functions Reference

| Function | Typical Gauge |
|----------|---------------|
| VBATT | 16 AWG (power) |
| GND | 16 AWG (ground) |
| CAN-H/L | 20-22 AWG (twisted) |
| Injectors | 18 AWG |
| Coils | 18 AWG |
| Sensors | 20-22 AWG |

---

*BlackFlag ECU - Connector Reference v2.2*
