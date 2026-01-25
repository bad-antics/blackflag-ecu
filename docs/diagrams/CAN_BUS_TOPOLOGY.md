# CAN Bus Network Topology Diagrams

## Standard Vehicle CAN Architecture

```
                           ┌─────────────────────────────────────────┐
                           │            OBD-II PORT                  │
                           │         (Pins 6, 14)                    │
                           └──────────────┬──────────────────────────┘
                                          │
                                          │ 500 kbps
                                          ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                           HIGH-SPEED CAN BUS                                │
│                    (Powertrain CAN - 500 kbps)                              │
└─────────────────────────────────────────────────────────────────────────────┘
        │           │           │           │           │           │
        │           │           │           │           │           │
   ┌────┴────┐ ┌────┴────┐ ┌────┴────┐ ┌────┴────┐ ┌────┴────┐ ┌────┴────┐
   │   ECM   │ │   TCM   │ │   ABS   │ │   SRS   │ │  TPMS   │ │ Cluster │
   │ (Engine)│ │ (Trans) │ │ Module  │ │(Airbag) │ │ Module  │ │  (IC)   │
   └─────────┘ └─────────┘ └─────────┘ └─────────┘ └─────────┘ └─────────┘


┌─────────────────────────────────────────────────────────────────────────────┐
│                           LOW-SPEED CAN BUS                                 │
│                      (Body CAN - 125 kbps)                                  │
└─────────────────────────────────────────────────────────────────────────────┘
        │           │           │           │           │           │
        │           │           │           │           │           │
   ┌────┴────┐ ┌────┴────┐ ┌────┴────┐ ┌────┴────┐ ┌────┴────┐ ┌────┴────┐
   │   BCM   │ │  HVAC   │ │ Door    │ │ Seat    │ │ Mirror  │ │ Lights  │
   │  (Body) │ │ Control │ │ Module  │ │ Module  │ │ Module  │ │ Module  │
   └─────────┘ └─────────┘ └─────────┘ └─────────┘ └─────────┘ └─────────┘


┌─────────────────────────────────────────────────────────────────────────────┐
│                        INFOTAINMENT CAN / MOST                              │
│                        (125 kbps / Fiber)                                   │
└─────────────────────────────────────────────────────────────────────────────┘
        │           │           │           │           │
   ┌────┴────┐ ┌────┴────┐ ┌────┴────┐ ┌────┴────┐ ┌────┴────┐
   │  Head   │ │ Amplifier│ │  Nav   │ │ Rear    │ │ Bluetooth│
   │  Unit   │ │         │ │ System  │ │ Camera  │ │ Module  │
   └─────────┘ └─────────┘ └─────────┘ └─────────┘ └─────────┘


                    ┌────────────────┐
                    │    Gateway     │
                    │    Module      │◄─── Bridges all CAN networks
                    └────────────────┘
```

---

## GM CAN Architecture (2014+)

```
                              ┌─────────────┐
                              │  OBD-II     │
                              │  Connector  │
                              └──────┬──────┘
                                     │
                    ┌────────────────┼────────────────┐
                    │                │                │
                    ▼                ▼                ▼
         ┌──────────────┐  ┌──────────────┐  ┌──────────────┐
         │   HS-CAN     │  │   MS-CAN     │  │   GMLAN      │
         │  (500 kbps)  │  │  (95 kbps)   │  │  (33.3 kbps) │
         └──────┬───────┘  └──────┬───────┘  └──────┬───────┘
                │                 │                 │
    ┌───────────┼───────────┐     │     ┌───────────┼───────────┐
    │     │     │     │     │     │     │     │     │     │     │
  ┌─┴─┐ ┌─┴─┐ ┌─┴─┐ ┌─┴─┐ ┌─┴─┐ ┌─┴─┐ ┌─┴─┐ ┌─┴─┐ ┌─┴─┐ ┌─┴─┐ ┌─┴─┐
  │ECM│ │TCM│ │ABS│ │SRS│ │EPS│ │BCM│ │IPC│ │HMI│ │PDM│ │RDM│ │SDM│
  └───┘ └───┘ └───┘ └───┘ └───┘ └───┘ └───┘ └───┘ └───┘ └───┘ └───┘

  ECM = Engine Control Module        BCM = Body Control Module
  TCM = Transmission Control         IPC = Instrument Panel Cluster
  ABS = Anti-lock Brake System       HMI = Human Machine Interface
  SRS = Supplemental Restraint       PDM = Passenger Door Module
  EPS = Electric Power Steering      RDM = Rear Door Module
                                     SDM = Sensing Diagnostic Module
```

---

## Ford CAN Architecture (2015+)

```
                              ┌─────────────┐
                              │  OBD-II     │
                              │  Connector  │
                              └──────┬──────┘
                                     │
              ┌──────────────────────┼──────────────────────┐
              │                      │                      │
              ▼                      ▼                      ▼
    ┌──────────────────┐   ┌──────────────────┐   ┌──────────────────┐
    │    HS-CAN        │   │    MS-CAN        │   │    HS-CAN 2      │
    │   (500 kbps)     │   │   (125 kbps)     │   │   (500 kbps)     │
    │   Pins 6, 14     │   │   Pins 3, 11     │   │   Secondary      │
    └────────┬─────────┘   └────────┬─────────┘   └────────┬─────────┘
             │                      │                      │
    ┌────────┴────────┐    ┌────────┴────────┐    ┌────────┴────────┐
    │    │    │    │  │    │    │    │    │  │    │    │    │    │  │
  ┌─┴┐ ┌─┴┐ ┌─┴┐ ┌─┴┐ ┌┴┐ ┌─┴┐ ┌─┴┐ ┌─┴┐ ┌─┴┐ ┌┴┐ ┌─┴┐ ┌─┴┐ ┌─┴┐ ┌─┴┐
  │PM│ │TM│ │AB│ │RS│ │EP│ │BC│ │IC│ │AC│ │DD│ │PD│ │AP│ │SY│ │IP│ │RB│
  └──┘ └──┘ └──┘ └──┘ └──┘ └──┘ └──┘ └──┘ └──┘ └──┘ └──┘ └──┘ └──┘ └──┘

  PM = Powertrain Control (PCM)      BC = Body Control Module
  TM = Transmission Control          IC = Instrument Cluster
  AB = ABS Module                    AC = A/C Module
  RS = Restraints Control            DD = Driver Door Module
  EP = Electric Power Steering       PD = Passenger Door Module
                                     AP = Audio Panel
                                     SY = SYNC Module
                                     IP = Image Processing Module
                                     RB = Rear View Camera
```

---

## CAN-FD Architecture (Modern EVs/Performance)

```
                              ┌─────────────┐
                              │  OBD-II     │
                              │  Connector  │
                              └──────┬──────┘
                                     │
                                     ▼
                           ┌──────────────────┐
                           │   CAN-FD Gateway │
                           │   (5 Mbps max)   │
                           └────────┬─────────┘
                                    │
         ┌────────────┬─────────────┼─────────────┬────────────┐
         │            │             │             │            │
         ▼            ▼             ▼             ▼            ▼
  ┌────────────┐ ┌─────────┐ ┌───────────┐ ┌─────────┐ ┌─────────┐
  │ Powertrain │ │ Chassis │ │   ADAS    │ │ Battery │ │ Infotain│
  │  CAN-FD    │ │ CAN-FD  │ │  CAN-FD   │ │ CAN-FD  │ │ Ethernet│
  │  (2 Mbps)  │ │ (2 Mbps)│ │  (5 Mbps) │ │ (2 Mbps)│ │ (100Mb) │
  └─────┬──────┘ └────┬────┘ └─────┬─────┘ └────┬────┘ └────┬────┘
        │             │            │            │           │
   ┌────┼────┐   ┌────┼────┐  ┌────┼────┐  ┌────┼────┐ ┌────┼────┐
   │    │    │   │    │    │  │    │    │  │    │    │ │    │    │
  ECU  INV  CHG ABS  EPS  SC RAD  CAM  LDR BMS  OBC  DC HU  TCU  DSP

  ECU = Engine Control        ABS = Brakes         BMS = Battery Mgmt
  INV = Inverter              EPS = Steering       OBC = Onboard Charger
  CHG = Charger Control       SC  = Stability      DC  = DC-DC Converter
                              RAD = Radar          HU  = Head Unit
                              CAM = Camera         TCU = Telematics
                              LDR = LiDAR          DSP = Amplifier
```

---

## CAN Message Structure

```
┌────────────────────────────────────────────────────────────────────────────┐
│                        STANDARD CAN FRAME (11-bit ID)                      │
├────────────────────────────────────────────────────────────────────────────┤
│                                                                            │
│  ┌─────┬──────────┬───┬───┬──────┬────────────────────────┬─────┬────────┐│
│  │ SOF │ 11-bit   │RTR│IDE│ DLC  │     DATA (0-8 bytes)   │ CRC │  EOF   ││
│  │  1  │   ID     │ 1 │ 1 │  4   │      0-64 bits         │ 15  │   7    ││
│  └─────┴──────────┴───┴───┴──────┴────────────────────────┴─────┴────────┘│
│                                                                            │
│  SOF = Start of Frame    DLC = Data Length Code                            │
│  RTR = Remote Request    CRC = Cyclic Redundancy Check                     │
│  IDE = ID Extension      EOF = End of Frame                                │
└────────────────────────────────────────────────────────────────────────────┘

┌────────────────────────────────────────────────────────────────────────────┐
│                      EXTENDED CAN FRAME (29-bit ID)                        │
├────────────────────────────────────────────────────────────────────────────┤
│                                                                            │
│  ┌─────┬──────────┬───┬───┬───────────┬───┬──────┬──────────┬─────┬─────┐ │
│  │ SOF │ 11-bit   │SRR│IDE│  18-bit   │RTR│ DLC  │   DATA   │ CRC │ EOF │ │
│  │  1  │   ID     │ 1 │ 1 │   ID Ext  │ 1 │  4   │  0-64b   │ 15  │  7  │ │
│  └─────┴──────────┴───┴───┴───────────┴───┴──────┴──────────┴─────┴─────┘ │
│                                                                            │
│  SRR = Substitute Remote Request (always recessive)                        │
│  Total ID space: 29 bits = 536,870,912 unique identifiers                  │
└────────────────────────────────────────────────────────────────────────────┘
```

---

*BlackFlag ECU - Network Topology Reference v2.1*
