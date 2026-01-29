# Reject Verification System – v2

## Overview
This project implements a reject verification system for a conveyor-based machine using Siemens LOGO!.  
The system monitors product detection and reject confirmation to ensure safe operation.  

The machine stops automatically when a fault condition is detected, including:

- Reject not verified by the reject sensor
- Two products simultaneously present in the reject zone
- Three consecutive rejected products
- Unknown outfeed caused by product or outfeed sensor errors

Visual indicators (LEDs and traffic lights) provide operator feedback for system state and fault conditions.  
Reset is only permitted when the machine is stopped to prevent unsafe operation.  
The system follows a **positive security (fail-safe) model**, ensuring that any unverified or ambiguous condition results in a safe stop.

---

## Core Functionality
- Detects products entering the reject zone
- Verifies that rejected products trigger the reject confirmation sensor
- Stops the machine on fault conditions
- Prevents unsafe resets during operation
- Provides visual feedback via LEDs and traffic lights
- Supports testing with extended timer durations; timers will be adjusted for real-world commissioning

---

## Logical I/O Mapping

### Inputs
| Signal | Description |
|------|------------|
| Camera | Camera classification input (Good / Bad) |
| ProductSensor | Detects product entering reject zone |
| RejectSensor | Confirms reject actuation |
| OutfeedSensor | Detects product leaving conveyor |
| StopButton | Operator stop input |
| ResetButton | Operator reset input |
| StartSignal | Conveyor start signal |

### Outputs
| Signal | Description |
|------|------------|
| PusherReject | Reject pusher actuator |
| Stop | Machine stop / interlock |
| LEDRedStop | Stop / fault LED |
| TrafficRed | Fault indication |
| TrafficYellow | Ready / transitional state |
| TrafficGreen | Running state |

---

## Internal Flags
| Flag | Purpose |
|----|--------|
| Fault_UnknownOut | Unknown product state detected |
| BadCamera | Camera fault or invalid classification |
| Fault_ConsecutiveRejects | Multiple rejects detected consecutively |
| Fault_RejectZoneOccupied | Reject zone blocked |
| Fault_RejectNotVerified | Reject not confirmed by sensor |
| ResetOnStop | Enables reset only when stopped |

---

## Timing Parameters (Commissioning Values)
- Timers are set to **extended durations** for testing and manual triggering
- In production, these values would be reduced according to conveyor speed and sensor response

| Timer | Function | Test Value |
|-----|--------|-----------|
| FaultRejectNotVerified (B028) | Delay before triggering reject-not-verified fault | 2.0 s |
| FaultNoOutfeedGoodProduct (B031) | Delay before fault on missing outfeed | 2.0 s |
| Reject Pusher (B021) | Delay and pulse for reject actuator | Delay: 50 ms, Pulse: 10 ms |

---

## System States
- **Stopped:** System is safe; reset is permitted
- **Ready:** Reset completed; waiting for Start input
- **Running:** Conveyor moving; reject logic active
- **Fault:** Any monitored fault detected; machine stopped and visual indicators active

---

## Version History
- v2.0: Improved reset safety, added visual indicators, refactored reject-zone fault logic  
- See `CHANGELOG.md` for detailed change history