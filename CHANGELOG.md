# Changelog

All notable changes to the PS2 Layzr Savre project will be documented in this file.

This project is currently in early research and prototype planning. The changelog will be used to track documentation updates, hardware revisions, firmware changes, test results, kit changes, and release milestones.

---

## Changelog Format

Each update should use this general format:

## [Version or Date] - Short Description

### Added

- New files, features, folders, documentation, hardware, firmware, or test data.

### Changed

- Changes to existing documentation, hardware design, firmware behavior, project structure, or testing process.

### Fixed

- Corrections to mistakes, broken links, incorrect notes, schematic issues, firmware bugs, or documentation problems.

### Removed

- Removed files, abandoned design ideas, replaced parts, deleted features, or outdated information.

### Notes

- Extra context, warnings, lessons learned, or development comments.

---

# Unreleased

Current development work that has not been assigned to a formal version yet.

## Added

- Initial GitHub repository structure.
- Main project README.
- Project status document.
- Roadmap document.
- Hardware folders for interposer, ESP32 interface, PS11 current sensing, and mechanical work.
- Firmware folders for ESP32 and test firmware.
- Documentation, references, images, manufacturing, test data, software, and release package folders.

## Changed

- Nothing yet.

## Fixed

- Nothing yet.

## Removed

- Nothing yet.

## Notes

- The project is currently in the planning and documentation stage.
- No production-ready hardware has been released.
- No production-ready firmware has been released.
- No public kit is available yet.
- Early documentation is being written as a development guide and project reference.

---

# Version History

## [v0.1] - Passive Monitor Interposer

**Status:** Planned

### Goal

Create the first passive or mostly passive Layzr Savre interposer board for monitoring PS2 optical-drive and servo-related signals without interfering with normal console operation.

### Planned Additions

- Passive interposer board concept.
- Tracking and focusing coil signal breakout.
- Test pads for oscilloscope and logic-analyzer use.
- Ground reference points.
- Optional ESP32 signal output headers.
- First hardware documentation.
- First assembly notes.
- First install and test checklist.

### Notes

- This revision should be for observation only.
- This revision should not cut power, reset the console, or control the optical-drive system.
- The main purpose of this revision is to collect real data before active protection features are designed.

---

## [v0.2] - ESP32 Logging Prototype

**Status:** Planned

### Goal

Add ESP32-based logging and diagnostic output for monitored signals.

### Planned Additions

- ESP32 firmware test structure.
- Serial debug output.
- Basic signal logging.
- Current and voltage logging where applicable.
- Timestamped event output.
- Early diagnostic interface.

### Notes

- This version should focus on collecting data.
- Protection decisions should not depend on the ESP32 until the input circuits and detection logic are validated.

---

## [v0.3] - PS11 Current Monitoring

**Status:** Planned

### Goal

Add current-monitoring hardware and documentation for the PS11 or servo power path.

### Planned Additions

- PS11 current-sense research.
- Current-sense circuit prototype.
- Current measurement test procedure.
- Current behavior logs.
- Notes for different PS2 board revisions.

### Notes

- PS11 behavior may vary by board revision.
- Current monitoring must be validated carefully before being used as part of a protection trigger.

---

## [v0.4] - Flatline Detection Prototype

**Status:** Planned

### Goal

Develop and test logic for detecting possible stuck, missing, or abnormal coil-drive behavior.

### Planned Additions

- Flatline detection theory.
- Test firmware for detection experiments.
- Detection timing notes.
- False-trigger testing.
- Normal vs abnormal signal comparisons.
- Threshold documentation.

### Notes

- This stage should be based on real captured test data.
- Detection should not trigger during normal startup, disc loading, seeking, or short glitches.

---

## [v0.5] - Coil/Servo Cutoff Prototype

**Status:** Planned

### Goal

Add a controlled cutoff method for the coil or servo power path after detection behavior has been validated.

### Planned Additions

- Cutoff circuit prototype.
- Fault response testing.
- Recovery testing.
- Fail-safe behavior notes.
- Fault indicator notes.
- Safety documentation updates.

### Notes

- This phase should only be tested after passive monitoring, logging, and detection behavior are understood.
- Testing should start on sacrificial or non-critical boards.

---

## [v0.6] - Integrated Prototype

**Status:** Planned

### Goal

Combine interposer monitoring, current sensing, ESP32 logging, flatline detection, and early cutoff behavior into a single prototype system.

### Planned Additions

- Integrated schematic.
- Integrated PCB layout.
- Combined firmware test build.
- Combined test procedure.
- System-level fault testing.
- Compatibility notes.

### Notes

- This version should still be considered experimental.
- Installation and use should be limited to experienced testers.

---

## [v0.7] - Validation Prototype

**Status:** Planned

### Goal

Validate the project across multiple PS2 models, board revisions, optical-drive assemblies, and disc types.

### Planned Additions

- Multi-console test matrix.
- Supported board revision notes.
- Unsupported board revision notes.
- Laser condition comparisons.
- Disc type comparisons.
- Long-duration testing notes.
- False-trigger test results.

### Notes

- This stage is important before any beta kit is considered.
- Compatibility should be documented honestly.

---

## [v0.8] - Documentation Prototype

**Status:** Planned

### Goal

Prepare the documentation needed for a skilled modder or beta tester to install and test Layzr Savre.

### Planned Additions

- Installation guide draft.
- Required tools list.
- First-power-on checklist.
- Troubleshooting guide.
- ESP32 flashing guide.
- Test data collection guide.
- Safety and limitations updates.
- Kit contents draft.

### Notes

- Documentation should explain both what the project does and what it does not do.
- The project should not be presented as a finished protection product at this stage.

---

## [v0.9] - Beta Kit

**Status:** Future Goal

### Goal

Prepare a small controlled beta kit for trusted testers.

### Planned Additions

- Beta hardware package.
- Beta firmware package.
- Beta tester instructions.
- Feedback process.
- Issue templates.
- Known issues list.
- Compatibility list.
- Kit packaging draft.

### Notes

- Beta testers should understand that this is experimental hardware.
- Feedback should be used to improve the hardware, firmware, and documentation before public release.

---

## [v1.0] - Community Release

**Status:** Future Goal

### Goal

Release Layzr Savre as a documented kit for the PS2 community.

### Planned Additions

- Stable hardware revision.
- Stable firmware release.
- Complete installation guide.
- Complete troubleshooting guide.
- Known-compatible model list.
- Known-unsupported model list.
- Final kit contents.
- Final packaging documentation.
- Website, Etsy, and eBay listing copy.
- Support process documentation.

### Notes

- v1.0 should only happen after real testing and validation.
- The release should clearly state the limits of the system and avoid overpromising protection.

---

# How to Add Future Entries

When making a new changelog entry, copy this template and place it near the top of the file under `Unreleased` or under the correct version.

## [Version or Date] - Short Description

### Added

- Item added.

### Changed

- Item changed.

### Fixed

- Item fixed.

### Removed

- Item removed.

### Notes

- Extra notes.
