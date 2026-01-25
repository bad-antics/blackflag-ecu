# Bench Flash Harness Guide

## Universal Bench Setup

```
    PC/Laptop + Flash Tool
           |
           | USB/Ethernet
           v
    J2534 Pass-Thru Device
           |
    +------+------+------+
    |      |      |      |
  CAN-H  CAN-L  K-LINE  BDM
    |      |      |      |
    +------+------+------+
           |
           v
    ECU (On Bench)
```

---

## Bosch ME7/MED9 Boot Mode

### Required Connections
| Pin | Function | Connection |
|:---:|----------|------------|
| 1 | BATT+ | +12V |
| 2 | BATT+ | +12V |
| 4 | IGN+ | +12V (switched) |
| 6 | K-LINE | Adapter |
| 9 | GND | Ground |
| 18 | GND | Ground |
| 27 | GND | Ground |
| 15 | BOOT | GND via 1kΩ |

### Boot Sequence
1. Connect all GND pins
2. Pull BOOT pin to GND via 1kΩ
3. Apply +12V to BATT pins
4. Apply +12V to IGN pin
5. Wait 500ms
6. Begin boot communication

---

## Tricore (Siemens/Continental) Boot

### Boot Configuration Pins
| BOOT_CFG0 | BOOT_CFG1 | HWCFG | Mode |
|:---------:|:---------:|:-----:|------|
| HIGH | LOW | GND | ASC (Serial) |
| HIGH | HIGH | GND | CAN Boot |
| LOW | LOW | Open | Internal Flash |
| LOW | HIGH | Open | External Flash |

### Required Connections
| Pin | Function | Connection |
|:---:|----------|------------|
| A1-A2 | VBATT | +12V |
| A9-A10 | GND | Ground |
| B3 | CAN-H | 500 kbps |
| B4 | CAN-L | 500 kbps |
| C7 | BOOT_CFG0 | Per table |
| C8 | BOOT_CFG1 | Per table |
| D12 | HWCFG | GND for ASC |
| D14 | ESR0 | External Reset |

---

## BDM (MPC5xx/Freescale)

### 10-Pin BDM Connector
| Pin | Signal | Description |
|:---:|--------|-------------|
| 1 | BKPT/DSDI | Breakpoint Input |
| 2 | GND | Ground |
| 3 | DSDO | Data Out |
| 4 | VDD | Target Voltage |
| 5 | N/C | - |
| 6 | N/C | - |
| 7 | RESET | Reset Line |
| 8 | N/C | - |
| 9 | DSCLK | Debug Clock |
| 10 | VPP | Flash Program (if needed) |

---

## Power Supply Setup

### Requirements
- Adjustable PSU: 13.8V / 10A
- Inline fuse: 5-10A
- Current limit: Start at 5A

### Connections
| Wire | Connection |
|------|------------|
| BATT+ | +13.8V (fused) |
| IGN+ | +13.8V (switched) |
| GND | PSU negative (multiple points) |
| CAN-H | 120Ω terminated |
| CAN-L | 120Ω terminated |

### Safety Notes
- Current limit PSU before connecting
- Normal idle draw: 0.5-2A
- Ground all GND pins
- Use proper CAN termination (120Ω each end)

---

## Pre-Power Checklist

- [ ] All ground connections secure
- [ ] Power polarity verified
- [ ] Current limit set
- [ ] Inline fuse installed
- [ ] Boot mode pins configured
- [ ] CAN bus terminated

---

*BlackFlag ECU - Bench Flash Reference v2.2*
