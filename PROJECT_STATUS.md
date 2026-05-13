# Project Status

**Project:** PS2 Layzr Savre  
**Status:** Early research / planning / prototype development  
**Current Stage:** Repository setup and project documentation  
**Target Audience:** Advanced PS2 modders, repair technicians, hardware developers, and preservation-minded console builders

---

## Current Project State

PS2 Layzr Savre is currently in the early development stage.

The project is being organized as a complete hardware, firmware, software, testing, and kit-development effort. The current focus is documenting the problem, defining the design goals, organizing research, and preparing the repo structure before hardware revisions are finalized.

At this stage, Layzr Savre should be considered an experimental research and development project, not a finished protection product.

---

## Project Goal

The goal of Layzr Savre is to better understand and monitor the PlayStation 2 optical-drive system in order to help preserve the console’s original disc-reading functionality.

The project is intended to monitor laser/servo behavior, observe tracking and focusing coil activity, watch for possible unsafe flatline conditions, monitor current draw through the PS11/servo power path, and eventually provide a controlled method of cutting power to the coil/servo path when a confirmed fault condition is detected.

The long-term goal is to develop this into a documented kit that can be offered to the PS2 community.

---

## Development Areas

Layzr Savre is being developed across several major areas:

- PS2 optical-drive signal research
- DSP-to-servo signal observation
- Tracking and focusing coil activity monitoring
- Flatline detection theory and validation
- PS11 current monitoring
- Coil/servo power cutoff design
- ESP32 communication and logging
- UART communication with the console where useful
- Web or serial interface for diagnostics
- Test data collection and analysis
- Installation and kit documentation
- Product packaging for future community release

---

## Current Repo Progress

| Area | Status | Notes |
|---|---|---|
| Repository structure | In Progress | Folder structure has been created for hardware, firmware, documentation, references, testing, manufacturing, and release packages. |
| Main README | Drafted | Initial project description and goals are being established. |
| Project status tracking | In Progress | This file will be updated as the project moves forward. |
| Roadmap | Planned | Development phases still need to be written and refined. |
| Safety documentation | Planned | Safety notes and limitations need to be clearly documented before hardware testing. |
| Hardware design | Research Stage | Interposer-board concept is being defined. No finalized production board yet. |
| Firmware | Not Started / Planning | ESP32 logging and interface concepts are planned but not yet implemented. |
| Software interface | Not Started / Planning | Web interface, data viewer, or serial tools are planned for future development. |
| Test data | Not Started | Real scope captures, current readings, and logs still need to be collected. |
| Kit packaging | Future Goal | Kit planning will begin after prototype validation. |

---

## Hardware Status

### Interposer Board

**Current Status:** Concept / planning stage

The interposer board is intended to sit between the PS2 optical-drive system and the relevant laser/servo signals. The first revision should be passive or mostly passive so the signals can be observed without affecting normal drive behavior.

Planned goals for the first hardware revision:

- Break out tracking/focusing coil-related signals
- Provide safe oscilloscope and logic-analyzer test points
- Provide connection points for an ESP32 or external logger
- Avoid interfering with normal PS2 disc operation
- Support future fault-detection and cutoff testing

No final PCB revision has been released yet.

---

### PS11 Current Monitoring

**Current Status:** Research / planning stage

One goal of the project is to monitor current through the PS11/servo power path. This may help identify abnormal drive behavior, excessive current draw, or possible fault conditions related to the optical-drive system.

Planned work:

- Confirm PS11 behavior across target PS2 board revisions
- Identify safe current-monitoring methods
- Determine whether a low-side, high-side, or inline current-sense approach is best
- Log current behavior during normal reads, failed reads, and fault conditions
- Compare healthy and weak optical-drive assemblies

---

### Coil Power Cutoff

**Current Status:** Not implemented yet

A future revision of the hardware may include a controlled cutoff method for the coil/servo power path. This feature should only be added after the project has enough test data to avoid false triggers and unsafe behavior.

Planned requirements:

- Cut power only after a confirmed unsafe condition
- Avoid triggering during normal seeking, startup, or disc loading
- Fail safely if firmware crashes or communication is lost
- Allow the console to recover cleanly after a fault
- Clearly document supported PS2 models and board revisions

---

## Firmware Status

### ESP32 Firmware

**Current Status:** Planning stage

The ESP32 portion of the project is intended to collect data from the interposer board, communicate with the console where useful, and provide a way to view or export laser/servo behavior.

Planned features:

- Read monitored analog or digital signals
- Log current, voltage, and coil-activity behavior
- Detect flatline or abnormal signal conditions
- Provide serial output for development testing
- Provide a simple web interface or diagnostic page
- Store or stream test logs
- Allow future threshold tuning

No functional firmware release is available yet.

---

## Software / Interface Status

**Current Status:** Planning stage

The software side of Layzr Savre may include a web-based interface, serial monitor output, log viewer, or other diagnostic tools.

Possible future interface features:

- Live signal status
- Current draw display
- Voltage display
- Fault-state display
- Event log
- Flatline detection status
- Configuration page for thresholds
- Exportable logs for troubleshooting and research

---

## Testing Status

**Current Status:** Not started

Testing will be a major part of this project. Layzr Savre should not be considered useful or safe until real measurements are collected and compared across multiple consoles and optical-drive conditions.

Planned test categories:

- Normal PS2 DVD game read
- Normal PS2 CD game read
- PS1 disc read
- Audio CD read
- DVD video read
- Weak laser behavior
- Dirty lens behavior
- Failed read behavior
- No-disc behavior
- Stuck/flatline signal behavior
- PS11 current behavior during normal and abnormal operation
- Servo/coil activity during startup, seeking, and read failure

Test data will be stored in the `Test-Data/` folder when available.

---

## Known Limitations

This project is not yet validated.

Current limitations:

- No finalized interposer PCB has been released.
- No confirmed universal signal map has been published.
- No production-ready firmware exists yet.
- No confirmed flatline-detection threshold has been established.
- No confirmed safe cutoff method has been validated.
- PS2 board revisions may behave differently.
- Installing early prototypes may damage a console if done incorrectly.
- This project requires advanced soldering and PS2 hardware knowledge.

---

## Safety Notes

Layzr Savre is intended to interact with sensitive parts of the PS2 optical-drive and servo system.

Incorrect installation, incorrect signal interception, or incorrect power cutoff could damage the console, optical drive, laser assembly, servo driver, DSP, or related components.

Early revisions should only be used for research and measurement by people who understand the risks.

---

## Current Priority List

The current development priorities are:

1. Finish the GitHub documentation structure.
2. Write the project overview and problem statement.
3. Document the PS2 laser/servo system basics.
4. Identify target PS2 board revisions for early testing.
5. Define the first passive interposer-board revision.
6. Determine which signals should be monitored first.
7. Document PS11 current-monitoring options.
8. Begin collecting scope captures and current measurements.
9. Develop the ESP32 logging concept.
10. Create a safe testing and validation plan.

---

## Target First Prototype

The first practical prototype should be:

**Layzr Savre Interposer v0.1 — Passive Monitor**

Expected purpose:

- Observe signals only
- Break out test points
- Allow oscilloscope and logger connection
- Avoid controlling or cutting anything yet
- Help collect real-world data before active protection is added

This version should be used to learn before making any automatic protection claims.

---

## Future Milestones

| Milestone | Goal | Status |
|---|---|---|
| v0.1 | Passive interposer monitor board | Planned |
| v0.2 | ESP32 signal logging prototype | Planned |
| v0.3 | PS11 current-monitoring prototype | Planned |
| v0.4 | Flatline-detection test firmware | Planned |
| v0.5 | Coil/servo cutoff prototype | Planned |
| v0.6 | Multi-console validation | Planned |
| v0.7 | Installation guide draft | Planned |
| v0.8 | Beta tester package | Planned |
| v0.9 | Pre-release kit documentation | Planned |
| v1.0 | Community-ready release | Future goal |

---

## Project Philosophy

Layzr Savre is being developed with a preservation-first mindset.

The purpose is not to remove the PS2 optical drive or replace original disc-reading behavior. The purpose is to study, monitor, and protect the original hardware so that PS2 consoles can continue reading discs as they were designed to do.

This project will prioritize:

- Clear documentation
- Honest testing
- Board-revision awareness
- Safe failure behavior
- Repeatable measurements
- Community feedback
- Repairability
- Long-term PS2 preservation

---

## Status Summary

Layzr Savre is currently an early-stage experimental PS2 optical-drive protection and telemetry project.

The repo structure is being created, documentation is being drafted, and the first hardware goals are being defined. No production-ready hardware, firmware, or kit has been released yet.

The next major step is to document the research and build the first passive interposer board for safe signal observation.
