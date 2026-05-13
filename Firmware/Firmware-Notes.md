# Firmware Notes

**Project:** PS2 Layzr Savre  
**Owner:** FatBaldDad  
**Status:** Early research / planning / prototype development  
**Folder:** Firmware  

---

## Overview

This document is a general firmware planning and notes file for the PS2 Layzr Savre project.

The firmware side of Layzr Savre is expected to support data logging, signal monitoring, PS11 current monitoring, future flatline detection, future cutoff simulation, and possibly future active protection control.

At this stage, all firmware should be treated as experimental.

The first firmware goal is safe logging and diagnostics only.

---

## Purpose of This Document

This file is intended to collect general firmware notes that apply across the whole Layzr Savre firmware folder.

It is meant to document:

- Overall firmware goals.
- Firmware development stages.
- Safety rules.
- ESP32 design assumptions.
- Logging plans.
- Detection theory.
- Cutoff simulation plans.
- Active cutoff warnings.
- File organization.
- Versioning ideas.
- Future firmware features.
- Open firmware questions.

More specific firmware notes should be placed in the related folder README files.

---

## Firmware Folder Structure

Current planned firmware structure:

    Firmware/
    ├── ESP32/
    │   ├── src/
    │   ├── include/
    │   ├── platformio.ini
    │   └── README.md
    │
    ├── Test-Firmware/
    │   └── README.md
    │
    └── Firmware-Notes.md

The `ESP32/` folder is intended for the main firmware.

The `Test-Firmware/` folder is intended for experiments, proof-of-concept builds, pin testing, ADC testing, detection testing, and cutoff simulation testing.

This file is for general notes that apply to both areas.

---

## Main Firmware Goal

The main firmware goal is to make Layzr Savre a useful optical-drive telemetry and diagnostic system before it becomes a protection system.

The firmware should eventually help monitor:

- Focus activity.
- Tracking activity.
- PS11 current.
- Driver IC voltage, if useful.
- Related voltage rails, if useful.
- Fault timing.
- Startup timing.
- Disc-detection timing.
- Read-retry timing.
- Possible flatline behavior.
- Future cutoff status.

The firmware should help collect real data before any active protection claims are made.

---

## Development Rule

The firmware should follow this rule:

Observe first.  
Log second.  
Detect third.  
Simulate cutoff fourth.  
Cut power last.

This rule should guide every firmware decision.

---

## Current Firmware Status

Current status:

- Main ESP32 firmware is not finalized.
- Test firmware is not finalized.
- Platform choice is still being planned.
- Pin assignments are not finalized.
- Signal-conditioning hardware is not finalized.
- PS11 current measurement method is not finalized.
- Flatline detection thresholds are not finalized.
- Cutoff behavior is not validated.
- No production firmware exists.
- No public release firmware exists.

Any firmware written at this stage should be treated as development firmware.

---

## Planned Firmware Stages

| Stage | Name | Purpose | Status |
|---|---|---|---|
| Stage 0 | Bench Test | Confirm ESP32 boot, serial output, and safe pin states | Planned |
| Stage 1 | Basic Logger | Log safe test inputs over serial | Planned |
| Stage 2 | PS11 Current Logger | Log conditioned PS11 current-sense data | Planned |
| Stage 3 | Activity Logger | Log conditioned focus and tracking activity | Planned |
| Stage 4 | Detection Test | Detect suspected faults in logging-only mode | Planned |
| Stage 5 | Cutoff Simulation | Log when cutoff would have happened without cutting power | Future |
| Stage 6 | Active Cutoff Test | Test active cutoff on sacrificial hardware only | Future |
| Stage 7 | Beta Firmware | Controlled firmware for trusted testers | Future |
| Stage 8 | Release Firmware | Stable firmware for public kit release | Future Goal |

---

## Firmware Safety Rules

All Layzr Savre firmware should follow these safety rules:

1. Active cutoff must be disabled by default.
2. Unknown board profiles must default to logging-only mode.
3. Firmware must print its name and version at boot.
4. Firmware must print whether active cutoff is enabled or disabled.
5. Firmware must not drive unknown PS2 signals.
6. Firmware must not connect directly to raw optical-drive signals.
7. Firmware must not assume PS11 current alone proves a fault.
8. Firmware must not assume coil activity alone proves a fault.
9. Firmware must not enable dangerous features silently.
10. Firmware must be tested on the bench before being connected to a PS2.

---

## Safe Default Behavior

Safe default behavior should be a core firmware requirement.

Safe defaults may include:

- Logging-only mode on first boot.
- Active cutoff disabled.
- Cutoff simulation disabled unless selected.
- Unknown board profile selected by default.
- Unsupported board profiles locked to logging-only mode.
- Fault thresholds set to conservative values.
- GPIO outputs placed in safe states.
- Cutoff control output disabled at boot.
- Web interface settings locked until configured.
- Serial output showing all safety states clearly.

If firmware settings become corrupted, the firmware should return to safe defaults.

---

## Firmware Boot Message

Every firmware build should print a clear boot message.

Suggested boot message fields:

- Firmware name.
- Firmware version.
- Build date.
- Hardware revision.
- Target ESP32 board.
- Board profile.
- Operating mode.
- Active cutoff status.
- Cutoff simulation status.
- Logging status.
- Safety warning.

Example boot message format:

    boot firmware=LayzrSavre_Logger version=0.1.0
    build_date=2026-05-13 target=esp32dev
    hardware_revision=PROTO board_profile=UNKNOWN
    mode=LOGGING_ONLY active_cutoff=DISABLED cutoff_simulation=DISABLED
    warning=EXPERIMENTAL_FIRMWARE

---

## Firmware Types

Layzr Savre may eventually have several firmware types.

| Firmware Type | Purpose | Active Cutoff |
|---|---|---|
| Bench Test | Test ESP32 without PS2 connection | Disabled |
| Logger | Log conditioned inputs | Disabled |
| Current Logger | Log PS11 current-sense data | Disabled |
| Activity Logger | Log focus and tracking activity | Disabled |
| Detection Test | Detect suspected faults and log them | Disabled |
| Cutoff Simulation | Log when cutoff would have happened | Disabled |
| Cutoff Test | Test active cutoff on sacrificial hardware | Optional with hardware enable |
| Beta | Controlled tester firmware | Restricted |
| Release | Stable public firmware | Only after validation |

Firmware names must make the risk level clear.

---

## Firmware Naming Convention

Suggested firmware names:

- LayzrSavre_BenchTest
- LayzrSavre_Logger
- LayzrSavre_CurrentLogger
- LayzrSavre_ActivityLogger
- LayzrSavre_DetectionTest
- LayzrSavre_CutoffSimulation
- LayzrSavre_CutoffTest
- LayzrSavre_Beta
- LayzrSavre_Release

Avoid unclear names such as:

- test
- final
- final2
- new
- working
- fixed
- upload

---

## Firmware Versioning

Suggested version format:

| Version Range | Purpose |
|---|---|
| 0.0.x | Early bench tests and experiments |
| 0.1.x | Basic serial logging |
| 0.2.x | PS11 current logging |
| 0.3.x | Focus and tracking activity logging |
| 0.4.x | Flatline detection in logging-only mode |
| 0.5.x | Cutoff simulation mode |
| 0.6.x | Active cutoff test firmware |
| 0.7.x | Integrated prototype firmware |
| 0.8.x | Documentation and validation firmware |
| 0.9.x | Beta firmware |
| 1.0.x | Public release firmware |

Firmware version numbers should be updated when behavior changes.

---

## Build Information

Each firmware build should include build information.

Recommended build fields:

- Firmware name.
- Firmware version.
- Build date.
- Build time, if useful.
- Target board.
- Hardware revision.
- Git commit, if available.
- Active cutoff compiled in or not.
- Default operating mode.
- Supported board profiles.
- Notes.

This information should be available in serial output and possibly the web interface.

---

## Platform Choice

The planned firmware platform is currently expected to be PlatformIO.

PlatformIO is useful because it provides:

- Good folder structure.
- VS Code integration.
- Repeatable builds.
- Library management.
- Multiple environment support.
- Good support for ESP32 targets.

Other possible options:

| Platform | Notes |
|---|---|
| PlatformIO | Preferred starting point |
| Arduino IDE | Simple, but less organized for a larger repo |
| ESP-IDF | Powerful, but more complex |
| Custom build system | Not needed early on |

The final choice can be updated later.

---

## ESP32 Target Notes

The exact ESP32 module is not finalized.

Possible ESP32 targets:

| Target | Notes |
|---|---|
| ESP32-WROOM-32 | Common and widely supported |
| ESP32-WROOM-32E | Common module option |
| ESP32-S3 | More modern option with extra features |
| ESP32 DevKit | Good for early bench testing |
| Custom ESP32 board | Possible future kit hardware |

The firmware should clearly document the intended target.

---

## Pin Assignment Notes

Pin assignments are not finalized.

Every pin should be documented before hardware is finalized.

Pin documentation should include:

- ESP32 pin number.
- Signal name.
- Direction.
- Function.
- Boot behavior.
- Pull-up or pull-down state.
- ADC support.
- Strapping pin status.
- Safe state.
- Connected hardware.
- Risk level.

Do not assign active cutoff control to a pin until its boot behavior is fully understood.

---

## Pin Assignment Template

Use this table when pins are selected.

| ESP32 Pin | Signal Name | Direction | Function | Boot Concern | Risk Level | Status |
|---|---|---|---|---|---|---|
| TBD | FOCUS_ACTIVITY | Input | Focus activity monitor | Unknown | Medium | Planned |
| TBD | TRACK_ACTIVITY | Input | Tracking activity monitor | Unknown | Medium | Planned |
| TBD | PS11_CURRENT | ADC Input | PS11 current monitor | Unknown | Medium | Planned |
| TBD | DRIVER_VOLTAGE | ADC Input | Driver IC voltage monitor | Unknown | Medium | Future |
| TBD | FAULT_LED | Output | Fault indicator | Unknown | Low | Future |
| TBD | MODE_SELECT | Input | Mode selection | Unknown | Low | Future |
| TBD | MANUAL_RESET | Input | Clear fault latch | Unknown | Low | Future |
| TBD | CUTOFF_ENABLE | Output | Future cutoff control | High risk | High | Future |
| TBD | UART_TX | Output | Serial debug | Low | Low | Planned |
| TBD | UART_RX | Input | Serial debug | Low | Low | Planned |

---

## GPIO Boot Safety

ESP32 GPIO behavior during boot must be reviewed.

Possible risks:

- GPIO pin pulses during boot.
- GPIO pin floats before firmware starts.
- GPIO pin is used as a strapping pin.
- GPIO pin affects boot mode.
- GPIO pin is connected to flash memory.
- GPIO pin backfeeds the PS2.
- GPIO pin enables cutoff accidentally.
- GPIO pin causes a false fault state.

Firmware alone may not solve boot-state problems. Hardware pull-ups, pull-downs, buffers, or gates may be required.

---

## Input Safety

ESP32 inputs should only receive safe conditioned signals.

The ESP32 should not directly receive:

- Raw focus coil outputs.
- Raw tracking coil outputs.
- Driver IC outputs.
- PS11 fuse voltage.
- Unknown DSP signals.
- Unknown Mechacon or Syscon signals.
- Motor-drive outputs.
- Signals above ESP32 input limits.
- Signals that may go negative.
- Signals that may be noisy or inductive without protection.

Inputs may require signal conditioning before connection.

---

## Signal Conditioning Notes

Possible signal-conditioning methods:

- High-impedance buffer.
- Voltage divider.
- RC filter.
- Comparator.
- Differential amplifier.
- Current-sense amplifier.
- External ADC.
- Clamp diode.
- Protection resistor.
- ESD protection.
- Optocoupler or isolation, if needed.

The correct method depends on the signal being monitored.

---

## PS11 Current Firmware Notes

PS11 is a physical fuse on the PS2 motherboard.

For this project, PS11 provides power to the driver IC in the area being studied.

The plan is to lift one side of PS11 and use that fuse location as a current-monitoring point.

Firmware should treat PS11 current as one measurement point only.

Important notes:

- PS11 current does not represent the entire optical-drive system.
- PS11 current does not prove a fault by itself.
- PS11 current should be logged before it is used for detection.
- PS11 current must be measured through safe signal conditioning.
- Firmware should store the shunt value or current-sense scale factor.
- Firmware should report raw and converted values where useful.
- Firmware should allow calibration later.

---

## Current Conversion Notes

If PS11 current is measured through a shunt, firmware may estimate current using:

    current = shunt_voltage / shunt_resistance

If a current-sense amplifier is used, firmware must also account for gain:

    current = measured_voltage / amplifier_gain / shunt_resistance

Firmware should document:

- Shunt resistance.
- Shunt tolerance.
- Amplifier gain.
- ADC reference.
- ADC scale factor.
- Calibration offset.
- Units used.

Early firmware should print raw ADC values along with calculated current.

---

## ADC Notes

ESP32 ADC readings may be noisy.

Firmware may need:

- Averaging.
- Oversampling.
- Filtering.
- Calibration.
- Offset correction.
- Range checking.
- Error reporting.
- External ADC support.

ADC readings should be compared against a multimeter or oscilloscope during testing.

---

## Logging Notes

The first firmware interface should be serial logging.

Logging should be simple and easy to read.

Possible log formats:

| Format | Use |
|---|---|
| Plain text | Early debugging |
| CSV | Graphing and spreadsheet review |
| JSON | Structured logs and future web interface |
| Event log | Fault and state transitions |
| Summary log | Test session summary |

Plain text should come first.

---

## Suggested Log Fields

Useful log fields:

- timestamp_ms
- firmware_name
- firmware_version
- hardware_revision
- board_profile
- mode
- active_cutoff_status
- focus_activity
- tracking_activity
- ps11_current_raw
- ps11_current_ma
- driver_voltage
- fault_state
- event_type
- notes

Not every log needs every field at the beginning.

---

## Event Logging Notes

Events may be more useful than constant raw logging for some firmware stages.

Possible events:

| Event | Meaning |
|---|---|
| BOOT | Firmware started |
| CONFIG_LOADED | Configuration loaded |
| LOGGING_STARTED | Logging began |
| INPUT_ACTIVE | Monitored input became active |
| INPUT_INACTIVE | Monitored input became inactive |
| CURRENT_SAMPLE | Current sample recorded |
| CURRENT_ABNORMAL | Current outside expected range |
| SUSPECT_FAULT | Possible fault detected |
| FAULT_CONFIRMED | Fault confirmed by timing and logic |
| CUTOFF_SIMULATED | Firmware would have cut power |
| CUTOFF_ACTIVE | Active cutoff triggered in future hardware |
| FAULT_RESET | Fault was cleared |
| ERROR | Firmware error condition |

Event names should stay consistent once chosen.

---

## Fault Detection Notes

Flatline detection should begin in logging-only mode.

Firmware may eventually compare:

- Focus activity.
- Tracking activity.
- PS11 current.
- Driver voltage.
- Timing windows.
- Board profile.
- Current threshold.
- Activity threshold.

A suspected fault should be logged first.

A confirmed fault should not control hardware until cutoff simulation and active cutoff testing are complete.

---

## Detection Timing Notes

Timing windows are required to avoid false triggers.

Possible timing settings:

| Setting | Purpose |
|---|---|
| STARTUP_IGNORE_MS | Ignore normal boot behavior |
| DISC_DETECT_IGNORE_MS | Ignore normal disc-detection behavior |
| RETRY_IGNORE_MS | Ignore normal retry pauses |
| ACTIVITY_TIMEOUT_MS | Time before missing activity is suspicious |
| CURRENT_TIMEOUT_MS | Time before abnormal current is suspicious |
| FAULT_CONFIRM_MS | Time before suspected fault becomes confirmed |
| FAULT_LATCH_MS | Time fault remains latched |
| RECOVERY_DELAY_MS | Delay before allowing recovery |

Timing values must come from real test data.

---

## Board Profile Notes

Different PS2 board revisions may need different settings.

A future board profile may include:

- PS2 model.
- Board revision.
- Driver IC type.
- PS11 behavior.
- Focus input type.
- Tracking input type.
- Expected PS11 current range.
- Startup timing.
- Detection timing.
- Supported hardware revision.
- Active cutoff allowed or blocked.
- Known issues.

Unknown profiles should default to logging-only mode.

---

## Configuration Notes

Firmware may eventually store configuration.

Possible stored settings:

- Operating mode.
- Board profile.
- Hardware revision.
- Shunt value.
- Current-sense amplifier gain.
- Current threshold.
- Activity threshold.
- Timing windows.
- Logging format.
- Wi-Fi settings.
- Web interface enabled or disabled.
- Active cutoff enabled or disabled.

Configuration must have safe defaults and a reset method.

---

## Web Interface Notes

A web interface may be added later.

Possible web interface features:

- Live status.
- Focus activity.
- Tracking activity.
- PS11 current.
- Voltage readings.
- Fault state.
- Event log.
- Board profile.
- Firmware version.
- Hardware revision.
- Configuration page.
- Log export.
- Reset fault.
- Safety warning page.

The web interface should not make active cutoff easy to enable by accident.

---

## Web Interface Safety Notes

If a web interface is added:

- Active cutoff must be clearly shown as enabled or disabled.
- Unsupported profiles should lock out active cutoff.
- Dangerous settings should require confirmation.
- Firmware version should be visible.
- Hardware revision should be visible.
- Board profile should be visible.
- Cutoff simulation should be clearly different from real cutoff.
- Invalid threshold values should be rejected.
- A factory reset option should exist.

---

## Cutoff Simulation Notes

Cutoff simulation is a future firmware mode.

In cutoff simulation mode, the firmware should:

- Run detection logic.
- Log suspected faults.
- Log confirmed faults.
- Log when cutoff would have happened.
- Avoid driving cutoff hardware.
- Record focus activity.
- Record tracking activity.
- Record PS11 current.
- Record timing data.
- Record false triggers.

Cutoff simulation should be tested before active cutoff.

---

## Active Cutoff Notes

Active cutoff is high risk.

Firmware should only control active cutoff when:

- Hardware supports it.
- A physical enable jumper is installed.
- Firmware mode allows it.
- Board profile supports it.
- Detection logic has been tested.
- Cutoff simulation has been tested.
- Test hardware is sacrificial or validated.
- Recovery behavior is documented.

Active cutoff should never be enabled by default.

---

## Cutoff Control Safety Notes

Future cutoff control must consider:

- GPIO boot state.
- GPIO reset state.
- Pull-up or pull-down hardware.
- Inverted or non-inverted logic.
- Cutoff enabled state.
- Cutoff disabled state.
- ESP32 crash behavior.
- ESP32 brownout behavior.
- Manual override.
- Fault latch.
- Recovery behavior.
- Backfeeding paths.

The hardware should remain safe even if firmware fails.

---

## Fault Latch Notes

A future firmware may support fault latching.

A latched fault means the fault state remains active until reset.

Possible reset methods:

- Power cycle.
- ESP32 reset.
- Manual reset input.
- Web interface reset.
- Serial command.
- Service mode.
- Timed recovery, only if proven safe.

Fault latching may help prevent repeated cutoff cycling.

---

## Recovery Notes

Recovery behavior must be planned.

Questions to answer:

- Should faults clear automatically?
- Should the console require a power cycle?
- Should the fault remain latched?
- Should logs be saved before recovery?
- Should the user remove the disc?
- What if the fault returns immediately?
- What if the PS2 is frozen after cutoff?
- What if the ESP32 resets during recovery?

Automatic recovery should not be added until tested.

---

## Firmware Testing Order

Recommended firmware testing order:

1. Bench test.
2. Pin state test.
3. Serial logging test.
4. ADC test.
5. PS11 current-sense bench test.
6. PS11 current-sense console test.
7. Focus activity input bench test.
8. Focus activity input console test.
9. Tracking activity input bench test.
10. Tracking activity input console test.
11. Detection test in logging-only mode.
12. Cutoff simulation test.
13. Active cutoff test on sacrificial hardware only.
14. Long-duration logging test.
15. Beta firmware test.

---

## Bench Testing Checklist

Before connecting firmware to a PS2:

- [ ] Firmware builds.
- [ ] Firmware uploads.
- [ ] ESP32 boots.
- [ ] Serial output works.
- [ ] Firmware version prints.
- [ ] Operating mode prints.
- [ ] Active cutoff status prints.
- [ ] GPIO states are checked.
- [ ] ADC reads safe bench input.
- [ ] No unexpected outputs are active.
- [ ] Reset behavior is safe.
- [ ] Brownout behavior is understood as much as possible.

---

## Console Testing Checklist

Before using firmware with a PS2:

- [ ] Console works normally before connection.
- [ ] Board revision documented.
- [ ] Signal conditioning installed.
- [ ] Input voltage range confirmed.
- [ ] ESP32 power source confirmed.
- [ ] Ground reference confirmed.
- [ ] No backfeeding confirmed.
- [ ] Active cutoff disabled.
- [ ] Serial logging working.
- [ ] Firmware version documented.
- [ ] Test condition documented.
- [ ] Stop-testing plan understood.

---

## Stop Testing If

Stop firmware testing immediately if:

- ESP32 becomes hot.
- ESP32 repeatedly resets.
- PS2 resets unexpectedly.
- Optical drive behaves abnormally.
- Current draw becomes abnormal.
- Voltage rails sag.
- ADC readings are out of safe range.
- Fault triggers repeatedly without cause.
- Cutoff output changes unexpectedly.
- PS11 area becomes hot.
- Driver IC becomes unusually hot.
- Smoke or burning smell occurs.

Investigate before continuing.

---

## Firmware Documentation Requirements

Each firmware version should document:

- Firmware name.
- Firmware version.
- Purpose.
- Target ESP32 board.
- Required hardware revision.
- Pin assignments.
- Active cutoff status.
- Operating modes.
- Required signal conditioning.
- Flashing instructions.
- Serial monitor settings.
- Known risks.
- Known issues.
- Test status.

Firmware without documentation should not be treated as stable.

---

## Firmware Release Notes

Each firmware release should include release notes.

Release notes should include:

- Version number.
- Date.
- What was added.
- What changed.
- What was fixed.
- Known issues.
- Hardware revision supported.
- Active cutoff status.
- Upgrade notes.
- Testing status.

Release notes should also be reflected in `CHANGELOG.md`.

---

## Firmware Archive Notes

Old firmware should be archived if it is useful for project history.

Archive firmware when:

- It was used for a specific test.
- It contains an abandoned idea.
- It is unsafe but historically important.
- It was replaced by a better version.
- It explains a design decision.

Archived firmware should include notes explaining why it was archived.

---

## What Not to Store in Firmware

Do not store:

- BIOS files.
- ROM files.
- Game files.
- Disc images.
- Copyrighted Sony files.
- Private customer information.
- Unlicensed service manual scans.
- Unknown firmware from unrelated projects.
- Dangerous firmware without warnings.

The firmware folder should contain only Layzr Savre firmware and development notes.

---

## Open Firmware Questions

Current open questions:

- Which ESP32 module should be used first?
- Should the project use ESP32-WROOM-32, ESP32-WROOM-32E, or ESP32-S3?
- Should PlatformIO be the main build system?
- Which GPIO pins are safest for inputs?
- Which GPIO pins must be avoided?
- Is the ESP32 ADC good enough for PS11 current logging?
- Should an external ADC be used?
- What sample rate is needed for current logging?
- What sample rate is needed for activity logging?
- Should raw waveforms be captured outside the ESP32?
- How should board profiles be stored?
- Should Wi-Fi be enabled in early firmware?
- When should the web interface be added?
- How should active cutoff be locked out?
- How should beta firmware be distributed?
- How should firmware updates be handled?

---

## Current Working Theory

The current working theory is:

- Firmware should begin as simple serial logging.
- Test firmware should be separated from main firmware.
- PS11 current should be logged only after safe signal conditioning.
- Focus and tracking activity should be logged only after safe signal conditioning.
- Detection should begin in logging-only mode.
- Cutoff simulation should come before active cutoff.
- Active cutoff should be disabled by default.
- Unknown board profiles should default to logging-only mode.
- Firmware should print safety status at boot.
- Hardware must remain safe if firmware fails.

This theory will be updated as development continues.

---

## Future Firmware Goals

Future firmware goals may include:

- Basic ESP32 bench test.
- Serial logger.
- PS11 current logger.
- Focus activity logger.
- Tracking activity logger.
- CSV logging.
- JSON logging.
- Web interface.
- Board profiles.
- Configurable thresholds.
- Flatline detection in logging-only mode.
- Cutoff simulation mode.
- Active cutoff test mode.
- Fault latching.
- Fault history.
- Log export.
- Firmware update support.
- Factory reset.
- Beta tester package.
- Public release firmware.

---

## Summary

The firmware side of Layzr Savre should be developed slowly and safely.

The first firmware should only observe and log.

Detection should be tested in logging-only mode before it controls anything.

Cutoff simulation should be tested before real cutoff.

Active cutoff should only be used after careful validation and only on supported hardware.

The firmware should help Layzr Savre become a reliable measurement system first, and only later support protection behavior after the hardware and detection theory are proven.
