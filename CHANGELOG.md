# Changelog

All notable changes to this project are documented here.
Versioning reflects functional and commissioning-related updates.

---

## [v2.0] - Latest

### Added
- LED and traffic light outputs for system state and fault indication
- Single pulse to control all Flashing lights for clarity and asthetics

### Changed

- Refactored reject-zone verification to use counter-based logic for "FaultRejectZoneOccupied" (M5)  
  - Improved readability and robustness  
  - Previous implementation had OFF at 3 count.
- Reset functionality gated through AND logic with Stop Mode active (B023)  
  - Prevents timers, counters, and latches from being reset while the machine is running
- Reject-zone fault logic reworked using a counter  
  - LOGO! does not support negative values  
  - Counter-based approach proved clearer and reduced unexpected stoppages

### Notes
- Start / Go input currently only affects visual indicators  
  - Does not influence reject logic  
  - Reset places system into a ready state, requiring Start input to resume
