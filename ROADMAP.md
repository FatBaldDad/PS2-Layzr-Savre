# Roadmap

**Project:** PS2 Layzr Savre  
**Purpose:** PS2 optical-drive protection, monitoring, telemetry, and preservation  
**Current Stage:** Early research and prototype planning  
**Release Target:** Future community kit after testing and validation  

---

## Roadmap Overview

PS2 Layzr Savre is being developed in phases.

The goal is to avoid rushing into a protection product before the PS2 laser, DSP, servo, focusing, tracking, current behavior, and failure modes are properly studied and documented.

The early versions of this project will focus on observation and data collection. Active protection features, such as cutting coil or servo power, should only be added after enough test data has been collected to understand normal and abnormal behavior.

---

## Project Development Phases

| Phase | Name | Goal | Status |
|---|---|---|---|
| Phase 0 | Research and Documentation | Define the problem, collect references, and document PS2 laser/servo behavior | In Progress |
| Phase 1 | Passive Interposer Board | Create a non-invasive board for signal observation and testing | Planned |
| Phase 2 | Signal and Current Logging | Collect real-world laser, coil, voltage, and current data | Planned |
| Phase 3 | ESP32 Interface | Connect monitored signals to ESP32 for logging and diagnostics | Planned |
| Phase 4 | Flatline Detection | Develop and test safe detection logic for stuck or missing coil activity | Planned |
| Phase 5 | Coil/Servo Power Cutoff | Add controlled fault response after detection logic is validated | Planned |
| Phase 6 | Multi-Console Testing | Test across multiple PS2 models, board revisions, and drive conditions | Planned |
| Phase 7 | Installation and Kit Documentation | Create install guides, test procedures, and troubleshooting documents | Planned |
| Phase 8 | Beta Kit | Prepare a small beta release for trusted testers | Future Goal |
| Phase 9 | Public Kit Release | Release a documented kit for the PS2 community | Future Goal |

---

# Phase 0 - Research and Documentation

## Goal

Build a solid technical foundation before designing active protection hardware.

This phase focuses on understanding the PS2 optical-drive system, identifying useful signals, documenting risks, and defining what Layzr Savre should and should not do.

## Tasks

- [ ] Document the purpose of Layzr Savre.
- [ ] Document the PS2 laser and optical-drive problem being addressed.
- [ ] Identify target PS2 models and board revisions.
- [ ] Document known PS2 laser, DSP, Mechacon/Syscon, and servo-driver behavior.
- [ ] Identify the tracking and focusing coil signal paths.
- [ ] Identify the PS11/servo power path on supported board revisions.
- [ ] Collect relevant datasheets and reference material.
- [ ] Define safe test points for oscilloscope and logic-analyzer work.
- [ ] Define what signals are monitor-only.
- [ ] Define what signals may eventually be interrupted or controlled.
- [ ] Create a safety and limitations document.
- [ ] Create a testing and validation plan.

## Exit Criteria

Phase 0 is complete when the project has enough documentation to begin designing a passive monitoring board without guessing blindly.

---

# Phase 1 - Passive Interposer Board

## Goal

Create the first Layzr Savre hardware revision as a passive or mostly passive signal-monitoring interposer.

This first board should be used for observation only. It should not cut power, reset the console, or interfere with normal disc operation.

## Planned Board Name

Layzr Savre Interposer v0.1 - Passive Monitor

## Tasks

- [ ] Define the connector style and board placement.
- [ ] Map the required optical-drive signal paths.
- [ ] Break out tracking and focusing coil-related signals.
- [ ] Add oscilloscope-friendly test pads.
- [ ] Add logic-analyzer-friendly test pads where appropriate.
- [ ] Add labeled ground reference points.
- [ ] Add optional ESP32 signal output headers.
- [ ] Add clear silkscreen labels.
- [ ] Keep signal paths short and clean.
- [ ] Avoid changing normal circuit behavior.
- [ ] Create schematic.
- [ ] Create PCB layout.
- [ ] Run ERC/DRC checks.
- [ ] Generate prototype Gerbers.
- [ ] Order prototype boards.
- [ ] Document assembly notes.
- [ ] Document first-install test procedure.

## Exit Criteria

Phase 1 is complete when the passive interposer can be installed and the PS2 can still operate normally while signals are observed.

---

# Phase 2 - Signal and Current Logging

## Goal

Collect real-world behavior data from working and failing optical-drive conditions.

This phase is where Layzr Savre starts learning what normal and abnormal PS2 laser/servo behavior looks like.

## Test Conditions

- [ ] No disc inserted.
- [ ] Known-good PS2 DVD game.
- [ ] Known-good PS2 CD game.
- [ ] Known-good PS1 game.
- [ ] Audio CD.
- [ ] DVD video.
- [ ] Dirty disc.
- [ ] Scratched disc.
- [ ] Weak laser.
- [ ] Failed read.
- [ ] Bad or disconnected laser condition, where safe.
- [ ] Different board revisions.
- [ ] Different optical-drive assemblies.

## Signals and Data to Capture

- [ ] Tracking coil activity.
- [ ] Focusing coil activity.
- [ ] Servo-driver behavior.
- [ ] PS11 current behavior.
- [ ] Relevant voltage rails.
- [ ] Startup behavior.
- [ ] Disc detection behavior.
- [ ] Seeking behavior.
- [ ] Read retry behavior.
- [ ] Failed read behavior.
- [ ] Possible flatline conditions.

## Output Folder Structure

Test data should eventually be organized into this structure:

    Test-Data/
    ├── Raw-Logs/
    ├── Processed-Logs/
    ├── Scope-Captures/
    ├── Current-Measurements/
    └── Notes/

## Exit Criteria

Phase 2 is complete when enough test data exists to clearly separate normal behavior from suspicious or unsafe behavior.

---

# Phase 3 - ESP32 Interface

## Goal

Develop the ESP32 side of Layzr Savre for logging, communication, diagnostics, and future configuration.

The ESP32 should not be trusted with protection decisions until the input circuits and detection logic are validated.

## Planned Features

- [ ] Read monitored signal inputs.
- [ ] Read current-sense data.
- [ ] Read voltage-sense data where useful.
- [ ] Timestamp important events.
- [ ] Stream debug output over serial.
- [ ] Support basic UART communication where useful.
- [ ] Provide a simple development log output.
- [ ] Store test logs.
- [ ] Support future web interface.
- [ ] Support future threshold tuning.
- [ ] Support future fault-state reporting.

## Firmware Folder Structure

    Firmware/
    ├── ESP32/
    │   ├── src/
    │   ├── include/
    │   ├── platformio.ini
    │   └── README.md
    │
    └── Test-Firmware/
        └── README.md

## Exit Criteria

Phase 3 is complete when the ESP32 can reliably collect and output useful test data without affecting normal PS2 operation.

---

# Phase 4 - Flatline Detection

## Goal

Develop detection logic for dangerous stuck, missing, or abnormal coil-drive behavior.

This phase must be handled carefully. The goal is to detect a real unsafe condition without false-triggering during normal disc behavior.

## Detection Concepts to Explore

- [ ] Loss of expected coil activity.
- [ ] Stuck-high condition.
- [ ] Stuck-low condition.
- [ ] Missing dynamic activity.
- [ ] Abnormal current draw.
- [ ] Abnormal voltage behavior.
- [ ] Sustained fault timing.
- [ ] Startup ignore window.
- [ ] Disc-loading ignore window.
- [ ] Retry-behavior filtering.
- [ ] Multi-signal confirmation before fault trigger.

## Requirements

- [ ] Detection must not trigger during normal seeking.
- [ ] Detection must not trigger during normal startup.
- [ ] Detection must not trigger during brief glitches.
- [ ] Detection should require a confirmed sustained fault.
- [ ] Detection should consider current behavior, not just signal state.
- [ ] Detection should be adjustable during development.
- [ ] Detection thresholds must be documented.

## Exit Criteria

Phase 4 is complete when flatline detection can be demonstrated repeatedly on test data without false positives during normal operation.

---

# Phase 5 - Coil/Servo Power Cutoff

## Goal

Add controlled fault response after the detection system has been validated.

This is the phase where Layzr Savre may begin actively protecting the optical-drive system by cutting power to the coil/servo path when a confirmed unsafe condition is detected.

## Important Warning

This phase should not be rushed.

Cutting the wrong signal, cutting the wrong rail, or triggering at the wrong time could damage the console, optical drive, laser assembly, servo driver, or related circuitry.

## Tasks

- [ ] Define the safest cutoff point.
- [ ] Confirm PS11/servo power behavior on target board revisions.
- [ ] Design a cutoff circuit.
- [ ] Make the cutoff fail-safe where possible.
- [ ] Make sure normal console behavior is not affected.
- [ ] Confirm that the cutoff responds quickly enough to be useful.
- [ ] Confirm that the console can recover after a fault.
- [ ] Add a clear fault indicator.
- [ ] Add a manual reset or recovery method if needed.
- [ ] Document what happens after a fault.
- [ ] Test on sacrificial boards before using good consoles.

## Exit Criteria

Phase 5 is complete when a controlled cutoff can be triggered safely and repeatedly under test conditions.

---

# Phase 6 - Multi-Console Testing

## Goal

Validate Layzr Savre across different PS2 models, board revisions, and optical-drive conditions.

## Planned Test Matrix

| Test Area | Goal |
|---|---|
| Board revision testing | Confirm compatibility differences between PS2 board revisions |
| Laser condition testing | Compare good, weak, and failing lasers |
| Disc type testing | Compare PS1 CD, PS2 CD, PS2 DVD, audio CD, and DVD video |
| Current testing | Compare PS11 behavior under different conditions |
| False-trigger testing | Make sure protection does not activate during normal use |
| Fault-trigger testing | Make sure real fault behavior can be detected |
| Recovery testing | Confirm the console can recover after protection activates |
| Long-duration testing | Confirm stability over extended sessions |

## Exit Criteria

Phase 6 is complete when Layzr Savre has been tested on enough hardware to define supported and unsupported configurations.

---

# Phase 7 - Installation and Kit Documentation

## Goal

Prepare the project for real-world use by advanced modders and testers.

## Documentation to Create

- [ ] Installation guide.
- [ ] Board-revision compatibility list.
- [ ] Required tools list.
- [ ] Soldering guide.
- [ ] Test-point guide.
- [ ] First-power-on checklist.
- [ ] Calibration or setup guide, if required.
- [ ] ESP32 flashing guide.
- [ ] Web interface guide, if used.
- [ ] Troubleshooting guide.
- [ ] Known issues document.
- [ ] Removal guide.
- [ ] Safety and limitations guide.
- [ ] Kit contents list.

## Exit Criteria

Phase 7 is complete when a skilled modder can install and test the system by following the documentation.

---

# Phase 8 - Beta Kit

## Goal

Release a small controlled beta kit to trusted testers.

The beta stage should be used to find installation problems, documentation gaps, compatibility issues, and unexpected PS2 board-revision behavior.

## Beta Kit Contents

Possible beta kit contents:

- [ ] Layzr Savre interposer board.
- [ ] ESP32/interface board.
- [ ] Required connectors or wiring.
- [ ] Current-sense hardware.
- [ ] Install guide.
- [ ] Test checklist.
- [ ] Firmware flashing instructions.
- [ ] Troubleshooting guide.
- [ ] Feedback form or issue template.

## Beta Tester Requirements

Beta testers should ideally be able to:

- [ ] Solder fine-pitch PS2 hardware.
- [ ] Use a multimeter.
- [ ] Use an oscilloscope or logic analyzer if possible.
- [ ] Provide clear photos.
- [ ] Provide test results.
- [ ] Report board revision and console model.
- [ ] Understand that this is experimental hardware.

## Exit Criteria

Phase 8 is complete when beta feedback has been collected, reviewed, and used to improve the hardware, firmware, and documentation.

---

# Phase 9 - Public Kit Release

## Goal

Prepare Layzr Savre as a documented kit for the PS2 community.

## Public Release Requirements

- [ ] Hardware revision is stable.
- [ ] Firmware is stable enough for release.
- [ ] Supported PS2 models are documented.
- [ ] Unsupported models are documented.
- [ ] Install guide is complete.
- [ ] Test procedure is complete.
- [ ] Known risks are documented.
- [ ] Known limitations are documented.
- [ ] Kit contents are finalized.
- [ ] Packaging is finalized.
- [ ] Website/Etsy/eBay copy is prepared.
- [ ] Community support process is planned.

## Exit Criteria

Phase 9 is complete when Layzr Savre can be offered as a clearly documented kit with honest limitations and support expectations.

---

# Version Milestones

| Version | Name | Purpose | Status |
|---|---|---|---|
| v0.1 | Passive Monitor | First interposer for signal observation only | Planned |
| v0.2 | Logging Prototype | ESP32 data logging and serial output | Planned |
| v0.3 | Current Monitor | PS11 current-sense testing | Planned |
| v0.4 | Detection Prototype | Flatline detection research firmware | Planned |
| v0.5 | Cutoff Prototype | First controlled coil/servo cutoff test | Planned |
| v0.6 | Integrated Prototype | Interposer, current monitoring, ESP32, and detection combined | Planned |
| v0.7 | Validation Prototype | Multi-console and multi-board-revision testing | Planned |
| v0.8 | Documentation Prototype | Install guide and troubleshooting guide draft | Planned |
| v0.9 | Beta Kit | Small controlled tester release | Future Goal |
| v1.0 | Community Release | Public kit release | Future Goal |

---

# Priority List

## Current Priorities

- [ ] Finish the repository structure.
- [ ] Fill in rough draft documentation files.
- [ ] Define the first target PS2 board revision.
- [ ] Document known laser/servo signal paths.
- [ ] Define the passive interposer board requirements.
- [ ] Start the first schematic for the passive monitor board.
- [ ] Create a safety and limitations document.
- [ ] Create a testing plan before ordering active protection hardware.

## Near-Term Priorities

- [ ] Build the first passive interposer prototype.
- [ ] Capture oscilloscope data from a working console.
- [ ] Capture PS11 current data from a working console.
- [ ] Compare normal read behavior against failed-read behavior.
- [ ] Begin ESP32 logging experiments.
- [ ] Create test logs and upload sample data.

## Long-Term Priorities

- [ ] Develop reliable flatline detection.
- [ ] Validate cutoff behavior safely.
- [ ] Test across multiple PS2 models.
- [ ] Prepare beta kits.
- [ ] Create final installation documentation.
- [ ] Offer a finished kit to the PS2 community.

---

# Development Rules

To keep the project safe and useful, Layzr Savre should follow these rules:

1. Observation comes before control.
2. Data comes before assumptions.
3. Passive prototypes come before active cutoff prototypes.
4. Active protection should not be added until false triggers are understood.
5. Board-revision differences must be documented.
6. Safety limitations must be stated clearly.
7. Test results should be saved, even when they show problems.
8. The project should preserve original disc-reading functionality.
9. The project should be honest about what is proven and what is still experimental.
10. Community feedback should be documented and used to improve the design.

---

# Future Ideas

These ideas are not required for the first release, but may be explored later:

- Web-based ESP32 diagnostic interface.
- Live laser/servo activity display.
- Current graphing.
- Fault-event history.
- Exportable logs.
- Adjustable fault thresholds.
- Board-revision profiles.
- Installation verification mode.
- OLED or touchscreen display support.
- UART communication with other PS2 service tools.
- Integration with other FBD PS2 control projects.
- Kit packaging for website, Etsy, and eBay sales.

---

# Roadmap Summary

Layzr Savre will begin as a research and monitoring project, then move toward logging, detection, validation, and finally safe protection hardware.

The project should not be considered a finished product until the hardware, firmware, detection logic, cutoff behavior, and installation process have been tested across real PS2 consoles and documented clearly.

The long-term goal is to create a useful, honest, and well-documented preservation kit for the PS2 community.
