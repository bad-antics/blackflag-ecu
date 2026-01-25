# J2534 Pass-Thru Interface

## Architecture Overview

```
    Application Layer (BlackFlag ECU)
                |
                | J2534 API Calls
                v
    Driver Layer (Vendor DLL)
                |
                | USB/Ethernet
                v
    Hardware Layer (VCI Device)
                |
                | Physical Protocols
                v
    Vehicle (OBD-II / ECU)
```

---

## Supported Protocols

### J2534-1 (Original)
| Protocol | ID | Speed | Use |
|----------|:--:|-------|-----|
| J1850 VPW | 0x01 | 10.4 kbps | GM |
| J1850 PWM | 0x02 | 41.6 kbps | Ford |
| ISO9141 | 0x03 | 10.4 kbps | Euro OBD |
| ISO14230 | 0x04 | 1.2-10.4 kbps | KWP2000 |
| CAN | 0x05 | 250/500 kbps | ISO15765 |
| ISO15765 | 0x06 | - | CAN Transport |
| SCI_A_ENGINE | 0x07 | - | Chrysler |
| SCI_A_TRANS | 0x08 | - | Chrysler |
| SCI_B_ENGINE | 0x09 | - | Chrysler |
| SCI_B_TRANS | 0x0A | - | Chrysler |

### J2534-2 (Extended)
| Protocol | ID | Speed | Use |
|----------|:--:|-------|-----|
| J2610 | 0x10000 | - | DRB-III |
| ISO14230-4 | 0x10001 | - | ISO-TP/K-Line |
| J1939 | 0x10002 | 250 kbps | Heavy Duty |
| J1708 | 0x10003 | - | HD Serial |
| TP2.0 | 0x10004 | - | VAG |
| GM_LAN | 0x10006 | - | SW-CAN |
| CAN_FD | 0x10007 | 8 Mbps | Modern |

---

## API Call Sequence

```
PassThruOpen(DeviceID)
    |
PassThruConnect(DeviceID, Protocol, Flags, Baudrate, ChannelID)
    |
PassThruStartMsgFilter(ChannelID, FilterType, ...)
    |
    +-- PassThruWriteMsgs(ChannelID, Msgs, NumMsgs, Timeout)
    |
    +-- PassThruReadMsgs(ChannelID, Msgs, NumMsgs, Timeout)
    |
PassThruStopMsgFilter(ChannelID, FilterID)
    |
PassThruDisconnect(ChannelID)
    |
PassThruClose(DeviceID)
```

---

## OBD-II to J2534 Cable Wiring

| OBD-II Pin | Signal | J2534 Pin |
|:----------:|--------|:---------:|
| 1 | SW-CAN | SW-CAN |
| 2 | J1850+ | J1850 BUS+ |
| 3 | MS-CAN H | MS-CAN H |
| 4 | CGND | Chassis GND |
| 5 | SGND | Signal GND |
| 6 | CAN-H | CAN HIGH |
| 7 | K-LINE | ISO K-LINE |
| 10 | J1850- | J1850 BUS- |
| 11 | MS-CAN L | MS-CAN L |
| 14 | CAN-L | CAN LOW |
| 15 | L-LINE | ISO L-LINE |
| 16 | +12V | BATTERY |

---

## Common Error Codes

| Code | Name | Description |
|:----:|------|-------------|
| 0x00 | STATUS_NOERROR | Success |
| 0x01 | ERR_NOT_SUPPORTED | Not supported |
| 0x02 | ERR_INVALID_CHANNEL_ID | Bad channel |
| 0x03 | ERR_INVALID_PROTOCOL_ID | Bad protocol |
| 0x07 | ERR_FAILED | General failure |
| 0x08 | ERR_DEVICE_NOT_CONNECTED | No device |
| 0x09 | ERR_TIMEOUT | Timeout |
| 0x0E | ERR_DEVICE_IN_USE | Already in use |
| 0x10 | ERR_BUFFER_EMPTY | No messages |
| 0x11 | ERR_BUFFER_FULL | TX buffer full |
| 0x19 | ERR_INVALID_BAUDRATE | Bad baudrate |

---

*BlackFlag ECU - J2534 Reference v2.2*
