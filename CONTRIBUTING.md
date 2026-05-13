# Contributing

**Project:** PS2 Layzr Savre  
**Owner:** FatBaldDad  
**Status:** Early research / planning / prototype development  

---

## Overview

Thank you for your interest in contributing to PS2 Layzr Savre.

Layzr Savre is an experimental PlayStation 2 optical-drive protection and telemetry project. The goal is to study, monitor, and eventually help protect the PS2 laser, servo, focusing, tracking, and coil-drive systems while preserving the console’s original ability to read discs.

This project is currently in the research and prototype planning stage. Contributions, ideas, test data, issue reports, and technical feedback are welcome, but the project is not yet a finished product or public kit.

---

## Important Notice

This project interacts with sensitive areas of the PlayStation 2 optical-drive and servo system.

Incorrect information, wiring, testing, firmware, or hardware design could damage a console.

For that reason, contributions should be handled carefully, documented clearly, and tested honestly.

---

## Ways to Contribute

Helpful contributions may include:

- PS2 board-revision information
- Optical-drive signal research
- DSP, servo, Mechacon, or Syscon notes
- Laser and coil-drive measurements
- PS11 current-monitoring information
- Oscilloscope captures
- Logic-analyzer captures
- Multimeter measurements
- Photos of relevant board areas
- Connector and pinout information
- Datasheet references
- Hardware design suggestions
- Firmware suggestions
- ESP32 logging ideas
- Safety concerns
- Documentation improvements
- Installation feedback
- Testing results
- Bug reports
- Compatibility reports

---

## Project Priorities

Layzr Savre should follow these priorities:

1. Preserve original PS2 disc-reading functionality.
2. Observe before controlling.
3. Collect data before making assumptions.
4. Avoid false protection claims.
5. Document board-revision differences.
6. Test on sacrificial or non-critical hardware first.
7. Keep safety and failure behavior in mind.
8. Make the project useful to the PS2 repair and preservation community.
9. Be honest about what is proven and what is still experimental.
10. Avoid rushing into a product before validation.

---

## What Not to Submit

Please do not submit:

- Untested claims presented as proven facts
- Unsafe wiring suggestions without warnings
- Console-damaging experiments without clear notes
- AI-generated technical claims without verification
- Copied documentation without permission
- Proprietary files that you do not have permission to share
- Sony copyrighted service-manual material uploaded directly to the repo
- BIOS, ROM, firmware dumps, or copyrighted console files
- Piracy-related files or instructions
- Commercial clone files based on this project
- Pull requests that remove attribution or project ownership notices

---

## Reporting Issues

Use GitHub Issues to report problems, ideas, questions, test results, or compatibility information.

A good issue report should include:

- Clear title
- PS2 model number
- Board revision, if known
- Optical-drive type, if known
- Laser model, if known
- What you tested
- What happened
- What you expected to happen
- Photos, logs, or scope captures if available
- Any wiring or hardware changes made
- Whether the console still works normally after testing

---

## Suggested Issue Labels

Useful labels may include:

- hardware
- firmware
- documentation
- testing
- research
- safety
- bug
- enhancement
- question
- board-revision
- signal-analysis
- current-sensing
- flatline-detection
- esp32-interface
- kit-planning

---

## Submitting Test Data

Test data is especially useful for this project.

Useful test data may include:

- Scope captures of tracking coil activity
- Scope captures of focusing coil activity
- Current measurements from PS11 or related servo power paths
- Voltage readings during startup and disc reads
- Logs from working optical drives
- Logs from weak optical drives
- Logs from failed reads
- Logs from dirty or scratched discs
- Notes comparing different PS2 models or board revisions

When submitting test data, please include as much context as possible.

---

## Test Data Context Template

Use this format when possible:

## Console Information

- PS2 model:
- Board revision:
- Region:
- Optical-drive assembly:
- Laser model:
- Modchip installed:
- Other mods installed:

## Test Setup

- Test equipment used:
- Probe points:
- Ground reference:
- Disc type:
- Disc condition:
- Power supply used:
- Console state before test:

## Test Result

- What was measured:
- What happened:
- Any abnormal behavior:
- Did the console recover:
- Files or images attached:

## Notes

- Extra observations:
- Concerns:
- Possible follow-up tests:

---

## Hardware Contributions

Hardware contributions may include schematic ideas, PCB review, connector research, circuit suggestions, or board-revision notes.

When suggesting hardware changes, please include:

- Purpose of the change
- Affected circuit area
- Expected benefit
- Possible risk
- Parts used
- Voltage and current assumptions
- Whether it has been tested
- Photos or diagrams if available

Hardware suggestions should be treated as experimental unless tested.

---

## Firmware Contributions

Firmware contributions may include ESP32 logging code, signal-processing ideas, web interface ideas, serial output improvements, or diagnostic tools.

Firmware work should prioritize:

- Reliable logging
- Clear debug output
- Safe default states
- No unexpected control of the console
- Watchdog-safe behavior
- Protection against false triggers
- Clear comments
- Easy testing
- Clear separation between monitoring and active cutoff logic

Early firmware should be treated as research firmware, not production firmware.

---

## Documentation Contributions

Documentation contributions are very welcome.

Helpful documentation work may include:

- Fixing spelling and grammar
- Improving install notes
- Adding board-revision details
- Adding safety warnings
- Clarifying signal names
- Improving test procedures
- Adding diagrams
- Adding troubleshooting steps
- Improving the README files
- Organizing references

Documentation should be clear, honest, and careful not to overpromise what the project can do.

---

## Safety Contributions

Safety concerns are important and should be reported.

Examples of safety-related concerns:

- A signal path may be loaded incorrectly
- A cutoff method may damage the console
- A test point may be unsafe
- A board revision may behave differently
- A false trigger may interrupt normal drive behavior
- A current-sense circuit may affect normal operation
- ESP32 inputs may need better protection
- A connector orientation may be confusing
- A kit instruction may be unclear or risky

Safety-related issues should be clearly labeled and documented.

---

## Pull Requests

Pull requests may be accepted for documentation, research notes, firmware, software, hardware notes, or project organization.

Before submitting a pull request:

- Keep the change focused.
- Explain what was changed.
- Explain why it was changed.
- Include testing notes if applicable.
- Avoid mixing unrelated changes.
- Do not remove warnings or limitations without discussion.
- Do not remove attribution or ownership notices.
- Do not add copyrighted material that cannot be redistributed.

---

## Commit Message Style

Use clear commit messages.

Good examples:

- Add passive interposer research notes
- Update PS11 current-monitoring documentation
- Fix README spelling and formatting
- Add ESP32 logging notes
- Add scope capture notes for DVD read test
- Update roadmap with v0.2 logging milestone
- Add safety warning for coil cutoff testing

Avoid vague messages like:

- update
- stuff
- fixed things
- more changes

---

## Branch Suggestions

Suggested branch names:

- docs/project-overview
- docs/testing-plan
- hardware/passive-interposer-v0.1
- hardware/ps11-current-sense
- firmware/esp32-logging
- testing/scope-captures
- safety/cutoff-notes
- release/beta-kit-planning

---

## Coding Style

Firmware and software should be written with clarity first.

Preferred style:

- Clear variable names
- Comments for important hardware behavior
- Constants for pin numbers and thresholds
- Separate files for major functions
- No hidden magic numbers
- Safe defaults
- Debug output during development
- Clear notes for experimental features

---

## Hardware Documentation Style

Hardware notes should include:

- Board name
- Revision number
- Purpose
- Supported PS2 models, if known
- Unsupported PS2 models, if known
- Signal names
- Connector orientation
- Power requirements
- Known risks
- Test procedure
- Revision history

---

## Version and Revision Naming

Suggested hardware revision naming:

- Layzr Savre Interposer v0.1 - Passive Monitor
- Layzr Savre Interposer v0.2 - ESP32 Logging
- Layzr Savre Interposer v0.3 - PS11 Current Monitor
- Layzr Savre Interposer v0.4 - Detection Prototype
- Layzr Savre Interposer v0.5 - Cutoff Prototype

Suggested firmware revision naming:

- ESP32 Logger v0.1
- ESP32 Logger v0.2
- ESP32 Detection Test v0.1
- ESP32 Interface Prototype v0.1

---

## Attribution

Contributors may be credited in project documentation, release notes, or a future contributors file.

Possible future file:

- CONTRIBUTORS.md

Credit may be given for:

- Testing
- Research
- Hardware review
- Firmware work
- Documentation
- Safety feedback
- Board-revision information
- Community support

---

## Contribution Ownership

By submitting feedback, issue reports, documentation, code, design suggestions, test data, pull requests, or other contributions, you understand that the project owner may use those contributions to improve PS2 Layzr Savre.

Submitting a contribution does not automatically grant ownership of the project, branding, product, hardware design, firmware, documentation, or commercial kit.

This project is currently license pending / all rights reserved. See `LICENSE.md` for the current license status.

---

## Commercial Use

No permission is currently granted to manufacture, sell, clone, repackage, or commercially distribute Layzr Savre hardware, firmware, software, documentation, or kit materials.

Commercial-use terms may be defined later.

Until then, assume the project is not open for commercial reuse.

---

## Communication

GitHub Issues should be used for organized technical discussion, bug reports, test results, and documentation updates.

Good communication helps the project move forward.

Please keep discussion:

- Clear
- Respectful
- Technical
- Honest
- Safety-minded
- Focused on PS2 preservation and repair

---

## Project Philosophy

Layzr Savre is being developed as a preservation-first project.

The goal is to better understand the PS2 optical-drive system and help preserve the console’s original ability to read discs.

This project should be built on real testing, careful documentation, community feedback, and honest limitations.

---

## Summary

Contributions are welcome, especially research, test data, documentation, safety feedback, and board-revision information.

The project is still experimental, so all contributions should be treated carefully and documented clearly.

The long-term goal is to develop Layzr Savre into a useful, honest, and well-tested kit for the PS2 community.
