# J2534 Pass-Thru Interface Diagrams

## J2534 Architecture Overview

```
    ┌─────────────────────────────────────────────────────────────────────────┐
    │                       J2534 PASS-THRU ARCHITECTURE                      │
    └─────────────────────────────────────────────────────────────────────────┘

              APPLICATION LAYER
    ┌─────────────────────────────────────────┐
    │    BlackFlag ECU / OEM Flash Tool       │
    │    (Windows Application)                │
    └──────────────────┬──────────────────────┘
                       │
                       │ J2534 API Calls
                       │ (PassThruOpen, PassThruConnect, etc.)
                       ▼
              DRIVER LAYER
    ┌─────────────────────────────────────────┐
    │    J2534 Device Driver (DLL)            │
    │    - Vendor-specific implementation     │
    │    - Windows Registry entries           │
    └──────────────────┬──────────────────────┘
                       │
                       │ USB / Ethernet / Bluetooth
                       ▼
              HARDWARE LAYER
    ┌─────────────────────────────────────────┐
    │    J2534 Device Hardware                │
    │    (VCI, Pass-Thru Device)              │
    └──────────────────┬──────────────────────┘
                       │
                       │ Physical Protocols
                       │ (CAN, ISO, PWM, VPW, etc.)
                       ▼
              VEHICLE LAYER
    ┌─────────────────────────────────────────┐
    │    Vehicle OBD-II / ECU                 │
    │    (J1962 Connector)                    │
    └─────────────────────────────────────────┘
```

---

## Supported Protocol Channels

```
    ┌───────────────────────────────────────────────────────────────────────┐
    │                     J2534 PROTOCOL CHANNELS                           │
    ├───────────────────────────────────────────────────────────────────────┤
    │                                                                       │
    │   ┌─────────────────────────────────────────────────────────────┐     │
    │   │  J2534-1 (Original)                                         │     │
    │   ├─────────────────────────────────────────────────────────────┤     │
    │   │  Protocol       │  ID      │  Description                   │     │
    │   ├─────────────────┼──────────┼────────────────────────────────┤     │
    │   │  J1850 VPW      │  0x01    │  GM vehicles (10.4 kbps)       │     │
    │   │  J1850 PWM      │  0x02    │  Ford vehicles (41.6 kbps)     │     │
    │   │  ISO9141        │  0x03    │  European OBD (10.4 kbps)      │     │
    │   │  ISO14230       │  0x04    │  KWP2000 (1.2-10.4 kbps)       │     │
    │   │  CAN            │  0x05    │  ISO15765 (250/500 kbps)       │     │
    │   │  ISO15765       │  0x06    │  CAN Transport Protocol        │     │
    │   │  SCI_A_ENGINE   │  0x07    │  Chrysler SCI Engine           │     │
    │   │  SCI_A_TRANS    │  0x08    │  Chrysler SCI Trans            │     │
    │   │  SCI_B_ENGINE   │  0x09    │  Chrysler SCI Engine (alt)     │     │
    │   │  SCI_B_TRANS    │  0x0A    │  Chrysler SCI Trans (alt)      │     │
    │   └─────────────────┴──────────┴────────────────────────────────┘     │
    │                                                                       │
    │   ┌─────────────────────────────────────────────────────────────┐     │
    │   │  J2534-2 (Extended)                                         │     │
    │   ├─────────────────────────────────────────────────────────────┤     │
    │   │  Protocol       │  ID      │  Description                   │     │
    │   ├─────────────────┼──────────┼────────────────────────────────┤     │
    │   │  J2610 (DLC)    │  0x10000 │  Chrysler DRB-III              │     │
    │   │  ISO14230-4     │  0x10001 │  ISO-TP over K-Line            │     │
    │   │  J1939          │  0x10002 │  Heavy Duty CAN (250 kbps)     │     │
    │   │  J1708          │  0x10003 │  Heavy Duty Serial             │     │
    │   │  TP2.0          │  0x10004 │  VAG TP2.0 Protocol            │     │
    │   │  FT_CAN         │  0x10005 │  Ford Transit CAN              │     │
    │   │  GM_LAN         │  0x10006 │  GM Single Wire CAN            │     │
    │   │  CAN_FD         │  0x10007 │  CAN Flexible Data (up to 8Mb) │     │
    │   └─────────────────┴──────────┴────────────────────────────────┘     │
    │                                                                       │
    └───────────────────────────────────────────────────────────────────────┘
```

---

## J2534 API Flow Diagram

```
    ┌─────────────────────────────────────────────────────────────────────────┐
    │                        J2534 API CALL SEQUENCE                          │
    └─────────────────────────────────────────────────────────────────────────┘

        APPLICATION                           J2534 DEVICE
            │                                      │
            │   PassThruOpen(DeviceID)             │
            │─────────────────────────────────────>│
            │                       STATUS_NOERROR │
            │<─────────────────────────────────────│
            │                                      │
            │   PassThruConnect(DeviceID,          │
            │     Protocol, Flags, Baudrate,       │
            │     ChannelID)                       │
            │─────────────────────────────────────>│
            │                       STATUS_NOERROR │
            │<─────────────────────────────────────│
            │                                      │
            │   PassThruStartMsgFilter(ChannelID,  │
            │     FilterType, MaskMsg, PatternMsg, │
            │     FlowControlMsg, FilterID)        │
            │─────────────────────────────────────>│
            │                       STATUS_NOERROR │
            │<─────────────────────────────────────│
            │                                      │
            │   ┌────────────────────────────────┐ │
            │   │  COMMUNICATION LOOP            │ │
            │   │                                │ │
            │   │  PassThruWriteMsgs(ChannelID,  │ │
            │   │    Msgs, NumMsgs, Timeout)     │ │
            │───┼───────────────────────────────>│ │
            │   │                                │ │
            │   │  PassThruReadMsgs(ChannelID,   │ │
            │   │    Msgs, NumMsgs, Timeout)     │ │
            │───┼───────────────────────────────>│ │
            │<──┼────────────────────────────────│ │
            │   │                                │ │
            │   └────────────────────────────────┘ │
            │                                      │
            │   PassThruStopMsgFilter(ChannelID,   │
            │     FilterID)                        │
            │─────────────────────────────────────>│
            │                                      │
            │   PassThruDisconnect(ChannelID)      │
            │─────────────────────────────────────>│
            │                                      │
            │   PassThruClose(DeviceID)            │
            │─────────────────────────────────────>│
            │                                      │
```

---

## Common J2534 Devices Pin-Out

### Drew Technologies CarDAQ-Plus3

```
    ┌────────────────────────────────────────────────────────────────┐
    │                  CARDAQ-PLUS3 CONNECTOR                        │
    │                                                                │
    │   DB-25 CONNECTOR (Vehicle Side)                               │
    │   ┌─────────────────────────────────────────────────────┐      │
    │   │  1   2   3   4   5   6   7   8   9  10  11  12  13  │      │
    │   │  ○   ○   ○   ○   ○   ○   ○   ○   ○   ○   ○   ○   ○  │      │
    │   │ 14  15  16  17  18  19  20  21  22  23  24  25      │      │
    │   │  ○   ○   ○   ○   ○   ○   ○   ○   ○   ○   ○   ○      │      │
    │   └─────────────────────────────────────────────────────┘      │
    │                                                                │
    │   PIN ASSIGNMENTS:                                             │
    │   ┌──────┬────────────────┬─────────────────────────────┐      │
    │   │ Pin  │ Signal         │ OBD-II Pin                  │      │
    │   ├──────┼────────────────┼─────────────────────────────┤      │
    │   │  1   │ J1850 BUS+     │ Pin 2                       │      │
    │   │  2   │ J1850 BUS-     │ Pin 10                      │      │
    │   │  3   │ ISO K-LINE     │ Pin 7                       │      │
    │   │  4   │ CHASSIS GND    │ Pin 4                       │      │
    │   │  5   │ SIGNAL GND     │ Pin 5                       │      │
    │   │  6   │ CAN HIGH       │ Pin 6                       │      │
    │   │  7   │ CAN LOW        │ Pin 14                      │      │
    │   │  8   │ +12V BATTERY   │ Pin 16                      │      │
    │   │  9   │ ISO L-LINE     │ Pin 15                      │      │
    │   │ 10   │ J1939 CAN HIGH │ -                           │      │
    │   │ 11   │ J1939 CAN LOW  │ -                           │      │
    │   │ 12   │ SW-CAN         │ Pin 1 (GM)                  │      │
    │   └──────┴────────────────┴─────────────────────────────┘      │
    │                                                                │
    └────────────────────────────────────────────────────────────────┘
```

### Standard OBD-II to J2534 Cable

```
    ┌─────────────────────────────────────────────────────────────────────────┐
    │                    OBD-II TO J2534 CABLE WIRING                         │
    └─────────────────────────────────────────────────────────────────────────┘

         OBD-II (J1962)                              J2534 Device
         Female Connector                            Connector
    ┌──────────────────────┐                    ┌──────────────────────┐
    │                      │                    │                      │
    │   Pin 1  (SW-CAN) ───┼────────────────────┼─── SW-CAN            │
    │   Pin 2  (J1850+) ───┼────────────────────┼─── J1850 BUS+        │
    │   Pin 3  (Ford MS)───┼────────────────────┼─── MS-CAN HIGH       │
    │   Pin 4  (CGND)   ───┼────────────────────┼─── CHASSIS GND       │
    │   Pin 5  (SGND)   ───┼────────────────────┼─── SIGNAL GND        │
    │   Pin 6  (CAN+)   ───┼────────────────────┼─── CAN HIGH          │
    │   Pin 7  (K-LINE) ───┼────────────────────┼─── ISO K-LINE        │
    │                      │                    │                      │
    │   Pin 10 (J1850-) ───┼────────────────────┼─── J1850 BUS-        │
    │   Pin 11 (Ford MS)───┼────────────────────┼─── MS-CAN LOW        │
    │   Pin 14 (CAN-)   ───┼────────────────────┼─── CAN LOW           │
    │   Pin 15 (L-LINE) ───┼────────────────────┼─── ISO L-LINE        │
    │   Pin 16 (+12V)   ───┼────────────────────┼─── +12V BATTERY      │
    │                      │                    │                      │
    └──────────────────────┘                    └──────────────────────┘

    SHIELDING:
    • Cable shield connected to Pin 4 (Chassis Ground)
    • CAN pairs twisted (Pin 6/14)
    • Keep cable length under 3 meters for reliability
```

---

## J2534 Error Codes

```
    ┌───────────────────────────────────────────────────────────────────────┐
    │                      J2534 ERROR CODES                                │
    ├───────────────────────────────────────────────────────────────────────┤
    │  Code  │ Name                    │ Description                       │
    ├────────┼─────────────────────────┼───────────────────────────────────┤
    │  0x00  │ STATUS_NOERROR          │ Function completed successfully   │
    │  0x01  │ ERR_NOT_SUPPORTED       │ Function not supported            │
    │  0x02  │ ERR_INVALID_CHANNEL_ID  │ Invalid channel ID                │
    │  0x03  │ ERR_INVALID_PROTOCOL_ID │ Protocol not supported            │
    │  0x04  │ ERR_NULL_PARAMETER      │ NULL pointer in parameter         │
    │  0x05  │ ERR_INVALID_IOCTL_VALUE │ Invalid IOCTL value               │
    │  0x06  │ ERR_INVALID_FLAGS       │ Invalid flags parameter           │
    │  0x07  │ ERR_FAILED              │ General failure                   │
    │  0x08  │ ERR_DEVICE_NOT_CONNECTED│ Device not connected              │
    │  0x09  │ ERR_TIMEOUT             │ Operation timed out               │
    │  0x0A  │ ERR_INVALID_MSG         │ Invalid message structure         │
    │  0x0B  │ ERR_INVALID_TIME_INTERVA│ Invalid time interval             │
    │  0x0C  │ ERR_EXCEEDED_LIMIT      │ Too many filters/periodic msgs    │
    │  0x0D  │ ERR_INVALID_MSG_ID      │ Invalid message ID                │
    │  0x0E  │ ERR_DEVICE_IN_USE       │ Device already in use             │
    │  0x0F  │ ERR_INVALID_IOCTL_ID    │ Invalid IOCTL ID                  │
    │  0x10  │ ERR_BUFFER_EMPTY        │ No messages in receive buffer     │
    │  0x11  │ ERR_BUFFER_FULL         │ Transmit buffer full              │
    │  0x12  │ ERR_BUFFER_OVERFLOW     │ Buffer overflow                   │
    │  0x13  │ ERR_PIN_INVALID         │ Invalid pin number                │
    │  0x14  │ ERR_CHANNEL_IN_USE      │ Channel already in use            │
    │  0x15  │ ERR_MSG_PROTOCOL_ID     │ Message protocol mismatch         │
    │  0x16  │ ERR_INVALID_FILTER_ID   │ Invalid filter ID                 │
    │  0x17  │ ERR_NO_FLOW_CONTROL     │ No flow control filter set        │
    │  0x18  │ ERR_NOT_UNIQUE          │ Filter already exists             │
    │  0x19  │ ERR_INVALID_BAUDRATE    │ Unsupported baudrate              │
    │  0x1A  │ ERR_INVALID_DEVICE_ID   │ Invalid device ID                 │
    └────────┴─────────────────────────┴───────────────────────────────────┘
```

---

*BlackFlag ECU - J2534 Interface Reference v2.1*
