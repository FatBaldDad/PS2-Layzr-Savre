# PS2 Layzr Savre

**PS2 Layzr Savre** is an experimental PlayStation 2 optical-drive telemetry, monitoring, and future protection project.

The goal of this project is to better understand the PS2 laser, optical pickup, focus coils, tracking coils, driver IC behavior, PS11 current behavior, and related failure conditions so the console’s original disc-reading function can be preserved where possible.

Layzr Savre is being developed as a hardware, firmware, testing, and kit-development project for the PS2 community.

---

## Project Status

**Current Status:** Early research / planning / prototype development

At this stage, Layzr Savre is not a finished product and should not be treated as a guaranteed laser-protection device.

Current focus:

- Organizing the GitHub repository.
- Documenting the project goals.
- Defining the first passive interposer concept.
- Researching focus and tracking coil behavior.
- Researching PS11 current monitoring.
- Planning ESP32 logging.
- Building a proper testing and validation process.
- Preparing the project for future prototype hardware.

---

## Main Goal

The main goal of Layzr Savre is to help preserve the PS2’s original ability to read discs.

This project is not intended to replace the optical drive with an ODE-style solution.

It is intended to study, monitor, log, and eventually help protect the original optical-drive hardware so PS2 consoles can continue reading original discs as they were designed to do.

---

## What Layzr Savre Is Intended To Do

Layzr Savre is being designed to eventually support:

- Monitoring PS2 optical-drive signals.
- Monitoring focus coil activity.
- Monitoring tracking coil activity.
- Monitoring current through the PS11 fuse path.
- Logging current, voltage, signal, and timing data.
- Using an ESP32 for logging and diagnostics.
- Studying normal and abnormal optical-drive behavior.
- Detecting possible flatline or stuck-drive conditions.
- Simulating future protection behavior before enabling real cutoff.
- Possibly cutting driver or coil-related power after a confirmed fault, only after validation.
- Becoming a documented kit for advanced PS2 modders and preservation-focused builders.

---

## What Layzr Savre Is Not

Layzr Savre is not currently:

- A finished product.
- A public release kit.
- A guaranteed laser-protection device.
- A universal PS2 repair solution.
- A replacement for proper laser calibration.
- A replacement for optical-drive cleaning or maintenance.
- A way to make every bad laser work again.
- A beginner-friendly install.
- An official Sony product.
- A proven protection system.

This project is experimental and should be treated carefully.

---

## Why This Project Exists

The PlayStation 2 optical-drive system is valuable, complex, aging, and not fully documented from a modern preservation point of view.

Modern loading methods such as HDD, SMB, UDPBD, MX4SIO, MMCE, and other homebrew solutions are useful, but they do not preserve the original disc-reading function.

Many users still care about:

- Reading original PS1 discs.
- Reading original PS2 CD and DVD games.
- Reading audio CDs.
- Reading DVD video.
- Testing repaired consoles.
- Preserving the console as it originally functioned.
- Keeping optical-drive hardware from being discarded unnecessarily.

Layzr Savre is being developed to support that preservation goal.

---

## Core Project Concept

The basic idea is to create an interposer and monitoring system that can observe important PS2 optical-drive behavior without interfering with normal operation.

The first hardware revisions should focus on passive monitoring and data collection.

Active protection features should come later, after normal and abnormal behavior has been measured and documented.

Development order:

1. Observe signals.
2. Log data.
3. Study normal and abnormal behavior.
4. Test detection logic in logging-only mode.
5. Simulate cutoff behavior.
6. Add active cutoff only after validation.

---

## PS11 Current Monitoring

PS11 is a physical fuse on the PS2 motherboard.

For this project, PS11 is currently being studied because it provides power to the driver IC in the area being researched.

The current plan is to lift one side of PS11 and use that fuse location as a current-monitoring point. By measuring the voltage drop across a known low-value current-sense path, Layzr Savre may be able to estimate current through the PS11 fuse path during different optical-drive conditions.

Important notes:

- PS11 is a fuse.
- PS11 provides power to the driver IC in the area being studied.
- PS11 is currently a current-monitoring research point.
- PS11 current does not represent the entire optical-drive system.
- PS11 current alone should not be treated as proof of a fault.
- The original fuse protection role must be preserved.
- PS11 should not automatically be assumed to be the final cutoff point.

---

## Flatline Detection Theory

One of the major research goals is to detect possible flatline or stuck-drive behavior.

In this project, a flatline condition generally means a signal or drive output becomes stuck, inactive, or abnormal when activity is expected.

Possible examples:

- Focus activity stops changing when it should be active.
- Tracking activity stops changing when it should be active.
- A driver output appears stuck high.
- A driver output appears stuck low.
- PS11 current remains abnormal during a failed read.
- The drive continues trying to operate during a suspected fault.

Flatline detection is not yet proven.

The project must collect real data before reliable detection thresholds or protection behavior can be trusted.

---

## ESP32 Interface

The ESP32 is planned to act as the logging and interface controller for Layzr Savre.

Planned ESP32 roles include:

- Reading conditioned focus activity signals.
- Reading conditioned tracking activity signals.
- Reading PS11 current-monitoring data.
- Reading voltage-monitoring data where useful.
- Logging optical-drive behavior.
- Sending serial debug output.
- Hosting a future web interface.
- Supporting future board profiles.
- Supporting future flatline detection.
- Supporting future cutoff simulation.
- Supporting future active cutoff only after validation.

The ESP32 should first be used as a logger, not as a protection controller.

---

## Planned Development Phases

| Phase | Name | Goal | Status |
|---|---|---|---|
| Phase 0 | Research and Documentation | Define the project, collect references, and document PS2 optical-drive behavior | In Progress |
| Phase 1 | Passive Interposer Board | Create a non-invasive board for signal observation and testing | Planned |
| Phase 2 | Signal and Current Logging | Collect real-world focus, tracking, voltage, and PS11 current data | Planned |
| Phase 3 | ESP32 Interface | Add logging, diagnostics, and communication features | Planned |
| Phase 4 | Flatline Detection | Test fault detection logic in logging-only mode | Planned |
| Phase 5 | Cutoff Simulation | Log when cutoff would have happened without cutting power | Future |
| Phase 6 | Active Cutoff Prototype | Test real cutoff only on sacrificial hardware | Future |
| Phase 7 | Multi-Console Validation | Test across multiple PS2 models and board revisions | Future |
| Phase 8 | Beta Kit | Prepare limited kits for trusted testers | Future |
| Phase 9 | Public Kit Release | Release a documented kit for the PS2 community | Future Goal |

---

## Planned Version Milestones

| Version | Name | Purpose | Status |
|---|---|---|---|
| v0.1 | Passive Monitor | First interposer for signal observation only | Planned |
| v0.2 | Logging Prototype | ESP32 data logging and serial output | Planned |
| v0.3 | Current Monitor | PS11 current-sense testing | Planned |
| v0.4 | Detection Prototype | Flatline detection research firmware | Planned |
| v0.5 | Cutoff Simulation | Simulate protection events without cutting power | Planned |
| v0.6 | Cutoff Prototype | First controlled cutoff test on sacrificial hardware | Future |
| v0.7 | Integrated Prototype | Interposer, current monitoring, ESP32, and detection combined | Future |
| v0.8 | Validation Prototype | Multi-console and board-revision testing | Future |
| v0.9 | Beta Kit | Small controlled tester release | Future |
| v1.0 | Community Release | Public documented kit release | Future Goal |

---

## Repository Structure

Current planned repository structure:

    PS2-Layzr-Savre/
    ├── README.md
    ├── PROJECT_STATUS.md
    ├── ROADMAP.md
    ├── CHANGELOG.md
    ├── LICENSE.md
    ├── CONTRIBUTING.md
    ├── SAFETY_AND_LIMITATIONS.md
    │
    ├── Documentation/
    │   ├── 00-Project-Overview.md
    │   ├── 01-Problem-Statement.md
    │   ├── 02-PS2-Laser-System-Basics.md
    │   ├── 03-Signal-Research.md
    │   ├── 04-Flatline-Detection-Theory.md
    │   ├── 05-PS11-Current-Monitoring.md
    │   ├── 06-Coil-Power-Cutoff-Method.md
    │   ├── 07-ESP32-Interface.md
    │   ├── 08-Data-Logging.md
    │   ├── 09-Testing-Plan.md
    │   ├── 10-Kit-Assembly-Concept.md
    │   └── 11-FAQ.md
    │
    ├── Hardware/
    │   ├── Interposer-Board/
    │   ├── PS11-Current-Sense/
    │   ├── ESP32-Interface-Board/
    │   └── Mechanical/
    │
    ├── Firmware/
    │   ├── ESP32/
    │   ├── Test-Firmware/
    │   └── Firmware-Notes.md
    │
    ├── Software/
    │   ├── Web-Interface/
    │   ├── Data-Viewer/
    │   └── Tools/
    │
    ├── Test-Data/
    │   ├── Raw-Logs/
    │   ├── Processed-Logs/
    │   ├── Scope-Captures/
    │   ├── Current-Measurements/
    │   └── README.md
    │
    ├── References/
    │   ├── Datasheets/
    │   ├── PS2-Board-Notes/
    │   ├── Pinouts/
    │   └── Research-Links.md
    │
    ├── Images/
    │   ├── Concept-Renders/
    │   ├── PCB-Renders/
    │   ├── Install-Photos/
    │   └── Diagrams/
    │
    ├── Release-Packages/
    │   ├── Prototype-v0.1/
    │   ├── Beta-v0.5/
    │   └── Kit-v1.0/
    │
    └── Manufacturing/
        ├── Assembly-Instructions/
        ├── Kit-Packaging/
        ├── Labels/
        ├── Etsy-eBay-Website-Copy/
        └── QA-Checklist.md

---

## Documentation

Important project documents:

| Document | Purpose |
|---|---|
| PROJECT_STATUS.md | Current project status and progress |
| ROADMAP.md | Planned development phases and milestones |
| CHANGELOG.md | Future change tracking |
| LICENSE.md | Current license status |
| CONTRIBUTING.md | Contribution rules and guidance |
| SAFETY_AND_LIMITATIONS.md | Safety warnings and project limitations |
| Documentation/00-Project-Overview.md | Full project overview |
| Documentation/01-Problem-Statement.md | Problem Layzr Savre is trying to solve |
| Documentation/02-PS2-Laser-System-Basics.md | Basic PS2 optical-drive system overview |
| Documentation/03-Signal-Research.md | Signal research and mapping notes |
| Documentation/04-Flatline-Detection-Theory.md | Theory behind fault and flatline detection |
| Documentation/05-PS11-Current-Monitoring.md | PS11 current monitoring plan |
| Documentation/06-Coil-Power-Cutoff-Method.md | Future cutoff method planning |
| Documentation/07-ESP32-Interface.md | ESP32 logging and interface planning |
| Documentation/08-Data-Logging.md | Test data organization |
| Documentation/09-Testing-Plan.md | Testing process and templates |
| Documentation/10-Kit-Assembly-Concept.md | Future kit planning |
| Documentation/11-FAQ.md | Frequently asked questions |

---

## Hardware Plan

The hardware side of Layzr Savre may eventually include:

- Passive interposer board.
- Focus and tracking signal breakout.
- PS11 current-sense section.
- ESP32 interface board.
- Signal-conditioning circuits.
- Test pads.
- Fault LED.
- Manual reset.
- Cutoff enable jumper.
- Future cutoff switch or load switch.
- Mechanical mounting aids.
- Kit-ready wiring and connector layout.

The first useful hardware revision should be passive or mostly passive.

---

## Firmware Plan

The firmware side of Layzr Savre may eventually include:

- ESP32 bench test firmware.
- ESP32 serial logger.
- PS11 current logger.
- Focus activity logger.
- Tracking activity logger.
- Flatline detection test firmware.
- Cutoff simulation firmware.
- Active cutoff test firmware for sacrificial hardware only.
- Future web interface.
- Future board profiles.
- Future beta and release firmware.

The first firmware should be safe logging firmware only.

---

## Testing Plan

Testing should happen in stages.

Early tests should include:

- Baseline console testing.
- Board revision documentation.
- Passive signal observation.
- Focus activity capture.
- Tracking activity capture.
- PS11 current measurement.
- ESP32 bench logging.
- ESP32 console logging.
- Logging-only flatline detection.
- Cutoff simulation.

Active cutoff should only be tested later, only on sacrificial hardware, and only after detection behavior has been validated.

---

## Safety Warning

Layzr Savre may interact with sensitive parts of the PS2 optical-drive system.

Incorrect installation, probing, firmware, current monitoring, or cutoff behavior may damage the console.

Possible damage includes:

- Optical-drive failure.
- Laser failure.
- Driver IC damage.
- Blown fuses.
- Damaged PS11 pads.
- Damaged traces.
- Console lockups.
- Partial power states.
- ESP32 damage.
- Motherboard damage.

Use early versions only if you understand the risks.

Do not test experimental hardware on a valuable or customer console first.

---

## Contribution

Community feedback and technical contributions are welcome.

Useful contributions may include:

- PS2 board-revision information.
- Driver IC information.
- PS11 location notes.
- Pinout research.
- Scope captures.
- PS11 current measurements.
- ESP32 firmware suggestions.
- Signal-conditioning ideas.
- Safety concerns.
- Documentation improvements.
- Test reports.
- Compatibility reports.

See `CONTRIBUTING.md` for contribution guidelines.

---

## License

This project is currently license pending / all rights reserved.

At this stage, no permission is granted to manufacture, sell, clone, repackage, or commercially distribute Layzr Savre hardware, firmware, software, documentation, or kit materials.

See `LICENSE.md` for the current license status.

---

## Trademark Notice

PlayStation, PlayStation 2, PS2, and related names are trademarks of their respective owners.

Layzr Savre is an independent preservation and hardware research project.

This project is not affiliated with, endorsed by, sponsored by, or approved by Sony Interactive Entertainment or any related company.

---

## Current Development Rule

The main development rule for Layzr Savre is:

Observe first.  
Log second.  
Detect third.  
Simulate cutoff fourth.  
Cut power last.

---

## Summary

PS2 Layzr Savre is an early-stage preservation-focused project for studying, monitoring, logging, and eventually helping protect the PlayStation 2 optical-drive system.

The project begins with research, passive monitoring, PS11 current observation, and ESP32 logging.

Protection behavior, especially active cutoff, should only come after real test data proves the detection logic is reliable and safe.

The long-term goal is to create a useful, honest, well-documented kit for the PS2 community while preserving the console’s original disc-reading function.

## AI Assistance and Attribution Disclaimer

This project uses AI tools to help with writing, organization, documentation, research, code examples, and design planning. While I review and edit the information, some details may still be incorrect, incomplete, or outdated.

Not all ideas, code, research, methods, or technical information in this project should be credited only to me. This project may reference, build on, or be inspired by community knowledge, open-source projects, datasheets, forum posts, Discord discussions, manufacturer documentation, and the work of other developers and modders.

Credit will be given whenever a source is known. If something is missing credit or needs correction, please let me know so I can update the documentation.
