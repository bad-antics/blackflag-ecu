# CAN Bus Network Topology

## Standard Vehicle Architecture

```
                        OBD-II PORT (Pins 6, 14)
                               |
                               | 500 kbps
                               v
    ================================================================
                      HIGH-SPEED CAN (Powertrain)
    ================================================================
         |         |         |         |         |         |
        ECM       TCM       ABS       SRS      TPMS    Cluster
      (Engine)  (Trans)  (Brakes)  (Airbag)  (Tires)   (IC)


    ================================================================
                      LOW-SPEED CAN (Body - 125 kbps)  
    ================================================================
         |         |         |         |         |         |
        BCM      HVAC      Door      Seat     Mirror   Lights
       (Body)  (Climate)  Module    Module   Module   Module


    ================================================================
                   INFOTAINMENT CAN / MOST (Fiber)
    ================================================================
         |         |         |         |         |
        Head      Amp       Nav      Camera  Bluetooth
        Unit             System      (Rear)   Module


                        GATEWAY MODULE
                    (Bridges all networks)
```

---

## GM Architecture (2014+)

```
                          OBD-II
                            |
          +-----------------+------------------+
          |                 |                  |
       HS-CAN           MS-CAN              GMLAN
      500 kbps          95 kbps            33.3 kbps
          |                 |                  |
    +-----+-----+     +-----+-----+     +------+------+
    |     |     |     |     |     |     |      |      |
   ECM   TCM   ABS   BCM   IPC   HMI   PDM    RDM    SDM
```

**Module Legend:**
- ECM = Engine Control
- TCM = Transmission Control
- ABS = Anti-lock Brakes
- BCM = Body Control
- IPC = Instrument Panel
- HMI = Human Machine Interface
- PDM = Passenger Door
- RDM = Rear Door
- SDM = Sensing Diagnostic

---

## Ford Architecture (2015+)

```
                          OBD-II
                            |
          +-----------------+------------------+
          |                 |                  |
       HS-CAN           MS-CAN            HS-CAN 2
      500 kbps         125 kbps           500 kbps
     Pins 6,14        Pins 3,11          Secondary
          |                 |                  |
    +-----+-----+     +-----+-----+     +------+------+
    |     |     |     |     |     |     |      |      |
   PCM   ABS   EPS   BCM   IPC   A/C   APIM  SYNC    TCU
```

---

## CAN-FD Architecture (EVs / 2020+)

```
                          OBD-II
                            |
                     CAN-FD GATEWAY
                      (5 Mbps max)
                            |
     +----------+----------+----------+----------+
     |          |          |          |          |
 Powertrain  Chassis     ADAS      Battery   Infotain
  CAN-FD     CAN-FD     CAN-FD     CAN-FD    Ethernet
  2 Mbps     2 Mbps     5 Mbps     2 Mbps     100Mb
     |          |          |          |          |
   +--+--+   +--+--+   +--+--+   +--+--+    +--+--+
   |     |   |     |   |     |   |     |    |     |
  ECU   INV ABS  EPS  RAD  CAM  BMS  OBC   HU   TCU
```

**EV Module Legend:**
- INV = Inverter
- RAD = Radar
- CAM = Camera
- BMS = Battery Management
- OBC = Onboard Charger
- HU = Head Unit
- TCU = Telematics

---

## CAN Message Frame Structure

**Standard Frame (11-bit ID):**
```
SOF | 11-bit ID | RTR | IDE | DLC | DATA (0-8 bytes) | CRC | EOF
 1      11        1     1     4        0-64 bits       15    7
```

**Extended Frame (29-bit ID):**
```
SOF | 11-bit ID | SRR | IDE | 18-bit ID | RTR | DLC | DATA | CRC | EOF
 1      11        1     1       18        1     4    0-64    15    7
```

---

*BlackFlag ECU - CAN Topology Reference v2.2*
