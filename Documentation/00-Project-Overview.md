# Project Overview

**Project:** PS2 Layzr Savre  
**Owner:** FatBaldDad  
**Status:** Early research / planning / prototype development  
**Document:** 00 - Project Overview  

---

## Overview

PS2 Layzr Savre is an experimental optical-drive protection and telemetry project for the PlayStation 2.

The goal of the project is to better understand, monitor, log, and eventually help protect the PS2 optical-drive system. This includes the laser, DSP, servo system, tracking coils, focusing coils, current consumption, and related fault behavior.

The long-term goal is to develop Layzr Savre into a documented hardware and firmware kit for the PS2 community.

Layzr Savre is being developed with a preservation-first mindset. The purpose is not to remove the optical drive or replace the console’s original disc-reading function. The purpose is to preserve that function by learning how the PS2 laser and servo system behaves, then using that information to detect dangerous conditions before damage occurs.

---

## Project Purpose

The PlayStation 2 optical-drive system is a complex combination of laser control, servo control, focus control, tracking control, disc detection, spindle control, sled movement, and feedback from the DSP and Mechacon/Syscon systems.

When a fault occurs, some PS2 models and board revisions may continue driving the optical-drive system in a way that can place stress on the laser, coils, or servo circuitry.

Layzr Savre is intended to study this behavior and eventually provide a controlled way to respond to dangerous conditions.

The project is focused on:

- Monitoring tracking and focusing coil activity.
- Watching for possible flatline or stuck-drive behavior.
- Monitoring current consumption through the PS11 or related servo power path.
- Logging voltage, current, and signal behavior.
- Using an ESP32 for data collection, communication, and interface features.
- Building enough test data to understand normal and abnormal optical-drive behavior.
- Developing safe detection logic before adding active protection.
- Creating a future kit that can be documented, tested, and offered to the PS2 community.

---

## Main Goal

The main goal of Layzr Savre is to help preserve the PS2’s original ability to read game discs.

This project is not intended to replace the optical drive with an ODE-style solution. It is intended to help keep original disc-reading hardware alive for people who still want to use the console as it was originally designed.

---

## Core Concept

The basic concept is to place a monitoring board, or interposer, near the PS2 optical-drive signal path.

The interposer will allow important signals to be observed, measured, logged, and eventually used for fault detection.

The first hardware revisions should focus on passive monitoring only.

Active control features, such as cutting coil or servo power, should only be added after normal and abnormal behavior has been studied and documented.

---

## Planned System Areas

Layzr Savre is expected to include several development areas.

### Interposer Board

The interposer board is the main hardware interface between the PS2 optical-drive system and the monitoring/protection circuit.

Planned functions may include:

- Signal breakout.
- Test pads.
- Tracking coil monitoring.
- Focusing coil monitoring.
- Current-sense connection points.
- ESP32 interface connections.
- Future cutoff-control routing.

The first revision should be passive or mostly passive.

---

### Tracking and Focusing Coil Monitoring

The tracking and focusing coils are important parts of the optical-drive system.

Layzr Savre aims to monitor coil activity to help identify whether the drive is behaving normally or entering a dangerous stuck or flatline condition.

Possible observations may include:

- Normal seeking behavior.
- Normal focusing behavior.
- Startup behavior.
- Disc-detection behavior.
- Read-retry behavior.
- Failed-read behavior.
- Missing activity.
- Stuck-high or stuck-low behavior.
- Loss of dynamic movement.

---

### PS11 Current Monitoring

One planned feature is monitoring current through PS11 or a related servo power path.

Current monitoring may help identify abnormal behavior that is not obvious from one signal alone.

Possible uses include:

- Measuring normal current draw.
- Measuring current during disc reads.
- Measuring current during failed reads.
- Comparing good and weak lasers.
- Detecting abnormal sustained current.
- Adding another input to fault-detection logic.

Current monitoring should be treated as one part of the overall detection system, not the only source of truth.

---

### Flatline Detection

Flatline detection is one of the major goals of the project.

A flatline condition may refer to a coil-drive or servo-related signal that becomes stuck, stops changing, or behaves abnormally when activity is expected.

The detection logic must be developed carefully because normal PS2 optical-drive behavior may include pauses, retries, startup delays, and low-activity periods.

A useful flatline-detection system should avoid false triggers during:

- Startup.
- Disc detection.
- No-disc state.
- Normal seeking.
- Disc spin-up.
- Disc spin-down.
- Read retries.
- Game loading transitions.
- Browser behavior.

A confirmed fault should likely require multiple conditions, such as signal behavior, timing, and current behavior.

---

### Coil or Servo Power Cutoff

A future revision may include a controlled method of cutting power to the coil or servo path when a confirmed unsafe condition is detected.

This feature is not part of the first passive-monitoring stage.

This feature must be validated carefully because cutting the wrong rail, cutting too early, or cutting during normal drive behavior could cause console problems or damage.

The cutoff system should be designed around safe failure behavior.

Important questions include:

- What happens if the ESP32 is not powered?
- What happens while the ESP32 is booting?
- What happens if firmware crashes?
- What happens if the cutoff signal floats?
- What happens after the fault clears?
- Can the console recover cleanly?
- Does the cutoff create any unwanted current path?
- Does the cutoff affect normal disc reading?

---

### ESP32 Interface

The ESP32 is planned as the main data logging and interface controller.

Possible ESP32 functions include:

- Reading monitored signals.
- Reading current-sense data.
- Reading voltage-sense data.
- Logging optical-drive behavior.
- Sending serial debug output.
- Hosting a simple web interface.
- Providing configuration options.
- Reporting fault states.
- Saving or streaming test logs.
- Communicating with the console through UART where useful.

The ESP32 should not be trusted with active protection decisions until the hardware inputs, firmware timing, and detection logic are tested.

---

### Data Logging

Data logging is a major part of this project.

The project should collect real-world data before making protection claims.

Useful data may include:

- Tracking coil activity.
- Focusing coil activity.
- PS11 current levels.
- Relevant voltage levels.
- Disc startup behavior.
- Read behavior.
- Failed-read behavior.
- Weak-laser behavior.
- Dirty-disc behavior.
- Scratched-disc behavior.
- No-disc behavior.
- Fault-trigger behavior.
- Recovery behavior.

Logs should include enough context to be useful later.

---

### User Interface

A future interface may be added to make the system easier to test and configure.

Possible interface options include:

- Serial monitor output.
- ESP32 web interface.
- Diagnostic status page.
- Live current display.
- Live voltage display.
- Live signal activity display.
- Fault history.
- Log export.
- Threshold settings.
- Board-revision profile settings.
- Installation verification mode.

The first version does not need a polished interface. Early development should prioritize accurate data collection.

---

### Kit Development

The long-term goal is to develop Layzr Savre into a kit for advanced PS2 modders, repair technicians, and preservation-focused builders.

A future kit may include:

- Interposer board.
- ESP32 interface board.
- Current-sense hardware.
- Required connectors or wiring.
- Installation guide.
- Testing checklist.
- Firmware flashing guide.
- Troubleshooting guide.
- Safety and limitations document.
- Compatibility list.
- Kit packaging.

A public kit should only be considered after the project has been tested, documented, and validated.

---

## Development Philosophy

Layzr Savre should be developed carefully and honestly.

The project philosophy is:

1. Preserve original disc-reading hardware.
2. Observe before controlling.
3. Collect data before making assumptions.
4. Treat early hardware as experimental.
5. Avoid overpromising protection.
6. Document board-revision differences.
7. Test with real consoles and real optical drives.
8. Report failures as well as successes.
9. Design for safe failure behavior.
10. Build something useful for the PS2 community.

---

## What This Project Is

Layzr Savre is intended to be:

- A PS2 optical-drive research project.
- A laser and servo telemetry project.
- A signal-monitoring project.
- A current-monitoring project.
- A future fault-detection project.
- A possible future protection system.
- A preservation-focused hardware project.
- A future kit for advanced users.

---

## What This Project Is Not

Layzr Savre is not currently:

- A finished product.
- A guaranteed laser-protection device.
- A universal PS2 repair solution.
- A beginner-friendly install.
- A replacement for proper laser calibration.
- A replacement for optical-drive maintenance.
- A replacement for good discs and clean hardware.
- A confirmed public kit.
- A validated protection system.
- An official Sony product.

---

## Expected Development Path

The project should follow a phased development path.

| Stage | Purpose |
|---|---|
| Research | Understand the PS2 optical-drive and servo system |
| Passive Monitoring | Observe signals without changing console behavior |
| Data Collection | Capture real-world signal, voltage, and current behavior |
| ESP32 Logging | Add repeatable data logging and diagnostics |
| Detection Logic | Develop and test flatline or fault detection |
| Active Cutoff | Add controlled coil or servo cutoff only after validation |
| Multi-Console Testing | Test across PS2 models and board revisions |
| Documentation | Create install, test, safety, and troubleshooting guides |
| Beta Kit | Release to trusted testers |
| Public Kit | Offer a validated kit to the PS2 community |

---

## Early Development Priorities

The current early priorities are:

- Build the GitHub repository structure.
- Draft the main project documentation.
- Define the first target board revision.
- Identify the most useful signals to monitor.
- Define the passive interposer board requirements.
- Document PS11 current-monitoring options.
- Create a testing and validation plan.
- Design the first passive monitoring board.
- Collect initial oscilloscope and current data.
- Begin ESP32 logging experiments.

---

## First Prototype Goal

The first practical prototype should be a passive monitoring interposer.

Suggested name:

Layzr Savre Interposer v0.1 - Passive Monitor

The purpose of this board is to observe and measure. It should not attempt to protect, cut power, or control the optical-drive system yet.

Expected features:

- Signal breakout.
- Test pads.
- Ground references.
- Optional ESP32 header.
- Minimal loading of monitored signals.
- Clear silkscreen labels.
- Easy probing.
- Safe install and removal.

---

## Future Prototype Goals

Future revisions may add:

- ESP32 logging.
- Current monitoring.
- Voltage monitoring.
- Signal conditioning.
- Flatline detection.
- Fault indicators.
- Controlled cutoff.
- Recovery behavior.
- Web interface.
- Kit-ready layout.
- Board-revision-specific versions.

Each version should be documented separately.

---

## Testing Requirements

Testing should include normal and abnormal conditions.

Planned test cases include:

- No disc.
- Known-good PS2 DVD.
- Known-good PS2 CD.
- Known-good PS1 disc.
- Audio CD.
- DVD video.
- Dirty disc.
- Scratched disc.
- Weak laser.
- Failed read.
- Startup behavior.
- Browser behavior.
- Long-duration testing.
- Recovery after fault.
- Multiple board revisions.

Testing should be done on sacrificial or non-critical consoles first.

---

## Documentation Requirements

The project should include documentation for:

- Project overview.
- Problem statement.
- PS2 laser system basics.
- Signal research.
- Flatline detection theory.
- PS11 current monitoring.
- Coil power cutoff method.
- ESP32 interface.
- Data logging.
- Testing plan.
- Kit assembly concept.
- Safety and limitations.
- Frequently asked questions.

Documentation should be updated as the project changes.

---

## Release Strategy

Layzr Savre should not be released as a public kit until the following items are ready:

- Stable hardware revision.
- Stable firmware revision.
- Tested detection behavior.
- Tested cutoff behavior, if included.
- Compatibility list.
- Unsupported model list.
- Installation guide.
- First-power-on checklist.
- Troubleshooting guide.
- Safety warnings.
- Known limitations.
- Kit contents list.
- Quality-control checklist.

A public release should be honest about what the project can and cannot do.

---

## Community Value

Layzr Savre can provide value to the PS2 community even before it becomes a finished kit.

Useful community benefits may include:

- Better documentation of PS2 optical-drive behavior.
- Better understanding of laser and servo failure modes.
- Shared test data.
- Board-revision comparisons.
- Repair and troubleshooting insight.
- Safer experimentation.
- Preservation of original disc-reading hardware.
- A future tool for advanced PS2 builders.

---

## Summary

PS2 Layzr Savre is an early-stage preservation-focused project for studying and eventually helping protect the PlayStation 2 optical-drive system.

The project will begin with research, passive monitoring, and data collection. Active protection features should only be added after testing and validation.

The long-term goal is to create a useful, honest, and well-documented kit for the PS2 community while preserving the original disc-reading function of the console.
