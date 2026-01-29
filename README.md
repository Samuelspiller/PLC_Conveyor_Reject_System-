# Reject Verification System – v2

## Overview
This project implements a reject verification system for a conveyor-based machine using Siemens LOGO!.  
The system runs as a Positive Security Model.
The system monitors product detection and reject confirmation to ensure that rejected products are physically removed.  
If a reject is not verified, the machine is safely stopped and a fault is indicated.

Version 2 focuses on improving reset safety, fault clarity, and operator feedback.

---

## Core Functionality
- Detects products entering the reject zone
- Verifies that rejected products trigger the reject confirmation sensor
- Stops the machine if a reject is not verified
- Prevents unsafe resets while the machine is running
- Provides visual feedback via LED / traffic light outputs

---

## Key Design Changes in v2

### Reset Safety
- Reset logic is gated through an AND condition requiring **Stop Mode active** (B023)
- Prevents timers, counters, and latches from being reset while the machine is running
- Ensures predictable and safe system behaviour during operation

### Reject Zone Fault Handling
- Reworked the "2 products in reject zone" fault using **counter-based logic**
- Chosen due to LOGO! limitations (no support for negative values)
- Counter approach proved easier to follow and reduced unexpected stoppages compared to a logic-loop implementation

### Visual Indicators
- Added LED and traffic light outputs to indicate:
  - Ready state
  - Running state
  - Fault / stop condition
- Indicators are driven by system state and fault conditions only (no independent control logic)

---

## System States
- **Stopped:** System is safe, reset is permitted
- **Ready:** Reset completed, waiting for Start input
- **Running:** Conveyor moving, reject logic active
- **Fault:** Reject not verified or zone error detected; machine stopped

---

## Inputs and Outputs (High-Level)

### Inputs
- Product sensor
- Reject confirmation sensor
- Start input
- Stop input
- Reset input

### Outputs
- Stop output (machine interlock)
- Reject actuator (pusher)
- LED / traffic light indicators

---

## Known Limitations / Notes
- Start / Go input does not influence reject logic  
  - Used only to indicate conveyor movement via lights
- Reset returns the system to a ready state; Start must be pressed to resume operation
- No customer or machine-specific details included due to confidentiality

---

## Version History
- v2.0: Improved reset safety, added visual indicators, refactored reject-zone fault logic  
- See `CHANGELOG.md` for detailed change history
