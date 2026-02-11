# Getting Started

## Hardware Requirements

- OBD-II adapter (ELM327 v1.5+, J2534, or SocketCAN)
- USB or Bluetooth connection
- Vehicle with OBD-II port (1996+ for US, 2001+ for EU)

## Installation

```bash
git clone https://github.com/bad-antics/blackflag-ecu
cd blackflag-ecu
pip install -r requirements.txt
```

## First Connection

```bash
# Auto-detect adapter
python3 blackflag.py detect

# Connect via USB
python3 blackflag.py connect --port /dev/ttyUSB0

# Connect via Bluetooth
python3 blackflag.py connect --bt AA:BB:CC:DD:EE:FF

# Read DTCs
python3 blackflag.py dtc --read

# Live data
python3 blackflag.py live --pids rpm,speed,coolant_temp
```
