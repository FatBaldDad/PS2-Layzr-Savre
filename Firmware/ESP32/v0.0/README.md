# ESP32 Firmware

**Project:** PS2 Layzr Savre  
**Owner:** FatBaldDad  
**Status:** Early research / planning / prototype development  
**Folder:** Firmware/ESP32  

---

## Overview

This folder will contain the ESP32 firmware for the PS2 Layzr Savre project.

The ESP32 firmware is planned to handle logging, communication, diagnostics, configuration, and future fault-detection support for the Layzr Savre hardware.

At this stage, the ESP32 firmware should be treated as experimental research firmware.

The first firmware goal is logging only.

Active protection, cutoff control, or any hardware action that affects the PS2 optical-drive system should not be enabled until the hardware and detection logic have been tested and validated.

---

## Purpose of the ESP32 Firmware

The ESP32 firmware is intended to provide the interface between the Layzr Savre monitoring hardware and the user.

Planned firmware responsibilities may include:

- Reading conditioned focus activity signals.
- Reading conditioned tracking activity signals.
- Reading PS11 current-monitoring data.
- Reading voltage-monitoring data where useful.
- Logging optical-drive behavior.
- Sending serial debug output.
- Supporting future web interface features.
- Supporting future board profiles.
- Supporting future flatline detection logic.
- Supporting future cutoff simulation mode.
- Supporting future active cutoff only after validation.

The first firmware builds should focus on safe observation and logging.

---

## Current Firmware Status

Current status:

- Firmware is not started or is in early planning.
- No stable firmware release is available.
- No production firmware is available.
- No active protection firmware is available.
- No cutoff behavior should be considered safe or final.
- Pin assignments are not finalized.
- Signal-conditioning hardware is not finalized.
- Board profiles are not finalized.
- Detection thresholds are not finalized.

This folder is being prepared so firmware can be developed in an organized way.

---

## Development Rule

The ESP32 firmware should follow this development rule:

Observe first.  
Log second.  
Detect third.  
Simulate cutoff fourth.  
Cut power last.

The first firmware should not cut power or control PS2 hardware.

---

## Planned Firmware Stages

| Stage | Firmware Name | Purpose | Status |
|---|---|---|---|
| Stage 0 | Bench Test | Confirm ESP32 boots and serial output works | Planned |
| Stage 1 | Logger v0.1 | Basic serial logging from safe test inputs | Planned |
| Stage 2 | Logger v0.2 | Add PS11 current logging after signal conditioning | Planned |
| Stage 3 | Logger v0.3 | Add focus and tracking activity logging | Planned |
| Stage 4 | Detection Test v0.1 | Detect suspected faults in logging-only mode | Planned |
| Stage 5 | Cutoff Simulation v0.1 | Log when cutoff would have happened without cutting power | Future |
| Stage 6 | Cutoff Test v0.1 | Enable active cutoff only with hardware enable and sacrificial testing | Future |
| Stage 7 | Beta Firmware | Firmware for trusted beta testers | Future |
| Stage 8 | Release Firmware | Stable firmware for public kit release | Future Goal |

---

## Folder Structure

Suggested firmware folder structure:

    Firmware/ESP32/
    ├── README.md
    ├── platformio.ini
    ├── src/
    │   └── main.cpp
    ├── include/
    │   └── config.h
    ├── lib/
    ├── data/
    └── notes/

This structure may change as development progresses.

---

## Planned Files

Possible future files:

| File | Purpose |
|---|---|
| platformio.ini | PlatformIO project configuration |
| src/main.cpp | Main firmware entry point |
| include/config.h | Pin definitions and firmware settings |
| include/pins.h | ESP32 pin assignments |
| include/version.h | Firmware version information |
| include/board_profiles.h | Future PS2 board profile definitions |
| src/logger.cpp | Logging functions |
| src/sensors.cpp | Sensor reading functions |
| src/current_monitor.cpp | PS11 current reading functions |
| src/activity_monitor.cpp | Focus and tracking activity functions |
| src/detection.cpp | Future flatline detection logic |
| src/web_interface.cpp | Future web interface functions |
| src/fault_manager.cpp | Future fault state and latch handling |
| src/cutoff_control.cpp | Future cutoff simulation or active cutoff control |
| data/ | Future web interface files |
| notes/ | Firmware development notes |

These files do not all need to exist at the beginning.

---

## Recommended Development Platform

The planned firmware platform is currently expected to be PlatformIO.

PlatformIO is useful because it provides:

- Organized project structure.
- Library management.
- Easy build configuration.
- Repeatable firmware builds.
- VS Code integration.
- Support for multiple ESP32 boards.

The firmware may also be adapted later for Arduino IDE or ESP-IDF if needed.

---

## Possible ESP32 Targets

The exact ESP32 module is not finalized.

Possible targets may include:

| Target | Notes |
|---|---|
| ESP32-WROOM-32 | Common, inexpensive, widely supported |
| ESP32-WROOM-32E | Common module option |
| ESP32-S3 | More modern option with additional features |
| ESP32 DevKit | Useful for early bench testing |
| Custom ESP32 board | Possible future kit hardware |

The first firmware should clearly document which board it is built for.

---

## Firmware Safety Notice

This firmware may eventually interact with hardware connected to sensitive PS2 optical-drive circuits.

Incorrect firmware behavior could damage hardware if active control features are enabled.

Firmware must be designed so that:

- Active cutoff is disabled by default.
- Unknown boards default to logging-only mode.
- GPIO pins are safe during boot.
- Cutoff control pins do not float.
- Dangerous features require intentional enable.
- Fault thresholds cannot be set carelessly.
- Serial output clearly reports safety mode.
- Web interface, if used, clearly reports whether cutoff is active.
- Unsupported board profiles cannot accidentally enable active protection.

During early development, the firmware should only log data.

---

## ESP32 GPIO Safety

ESP32 GPIO pins can behave differently during boot.

Some pins may be strapping pins, pulled high, pulled low, or used internally by flash or boot mode.

Before assigning pins, check:

- Whether the pin is safe during boot.
- Whether the pin is an input-only pin.
- Whether the pin supports ADC.
- Whether the pin is used for flash.
- Whether the pin affects boot mode.
- Whether the pin may output a pulse at startup.
- Whether the pin has an internal pull-up or pull-down.
- Whether the pin can backfeed the PS2 circuit.

Cutoff control must never be assigned to an unsafe boot pin without protection.

---

## Planned Pin Assignments

Pin assignments are not finalized.

Use this table once pins are selected.

| ESP32 Pin | Signal Name | Direction | Purpose | Boot Concern | Status |
|---|---|---|---|---|---|
| TBD | FOCUS_ACTIVITY | Input | Focus activity monitor | Unknown | Planned |
| TBD | TRACK_ACTIVITY | Input | Tracking activity monitor | Unknown | Planned |
| TBD | PS11_CURRENT | Input ADC | PS11 current monitor | Unknown | Planned |
| TBD | DRIVER_VOLTAGE | Input ADC | Driver IC voltage monitor | Unknown | Future |
| TBD | FAULT_LED | Output | Fault indicator | Unknown | Future |
| TBD | MODE_SELECT | Input | Logging or test mode select | Unknown | Future |
| TBD | MANUAL_RESET | Input | Clear latched fault | Unknown | Future |
| TBD | CUTOFF_ENABLE | Output | Future cutoff control | High risk | Future |
| TBD | UART_TX | Output | Serial debug | Low risk | Planned |
| TBD | UART_RX | Input | Serial debug | Low risk | Planned |

Do not finalize hardware until the pin behavior is reviewed.

---

## Planned Firmware Modes

Future firmware may support different operating modes.

| Mode | Purpose | Active Cutoff |
|---|---|---|
| Bench Test | Test ESP32 without PS2 connected | Disabled |
| Logging Only | Read and log data only | Disabled |
| Detection Test | Detect suspected faults but only log them | Disabled |
| Cutoff Simulation | Log when cutoff would have happened | Disabled |
| Protection Test | Active cutoff testing on sacrificial hardware | Optional with hardware enable |
| Beta Protection | Controlled beta testing | Optional with restrictions |
| Release Protection | Final validated protection behavior | Only after validation |

The default mode should be logging-only or safer.

---

## Logging-Only Mode

Logging-only mode is the first important firmware mode.

In logging-only mode, the firmware may:

- Read conditioned inputs.
- Log focus activity.
- Log tracking activity.
- Log PS11 current.
- Log voltage readings.
- Log firmware state.
- Log suspected faults.
- Log false triggers.
- Output serial debug data.
- Avoid controlling PS2 hardware.
- Avoid cutoff behavior.

Logging-only mode should be safe for early testing.

---

## Cutoff Simulation Mode

Cutoff simulation mode is a future firmware mode.

In cutoff simulation mode, the firmware may detect a suspected fault and record that cutoff would have happened, but it does not actually cut power.

This mode is important because it allows detection logic to be tested before active cutoff is enabled.

Cutoff simulation may log:

- Suspected fault type.
- Fault start time.
- Fault duration.
- Focus activity state.
- Tracking activity state.
- PS11 current.
- Detection thresholds.
- Whether cutoff would have triggered.
- Whether the condition cleared.

This mode should be used before any real cutoff testing.

---

## Active Cutoff Mode

Active cutoff mode is a future feature.

It should not be enabled in early firmware.

Active cutoff should only be allowed when:

- Hardware supports cutoff.
- Hardware cutoff enable is installed.
- Firmware is configured for active cutoff.
- Board profile is supported.
- Detection logic has been tested.
- False trigger behavior has been reviewed.
- Testing is being done on sacrificial or validated hardware.
- User intentionally enables the feature.

Active cutoff must never be enabled by accident.

---

## Planned Data Inputs

Possible data inputs:

- Focus activity signal.
- Tracking activity signal.
- PS11 current sense.
- Driver IC voltage.
- ESP32 supply voltage.
- Mode select input.
- Manual reset input.
- Cutoff enable jumper state.
- Fault latch status.
- Board profile setting.

All inputs should be validated before use.

---

## Planned Data Outputs

Possible outputs:

- Serial debug log.
- CSV log.
- JSON log.
- Web interface status.
- Fault LED.
- Fault buzzer, if added.
- Cutoff simulation event.
- Future cutoff control output.
- Future fault latch reset output.

Early firmware should only output serial logs and safe indicators.

---

## Serial Output

Serial output should be the first firmware interface.

Serial output should show:

- Firmware name.
- Firmware version.
- Build date.
- Hardware revision.
- Board profile.
- Operating mode.
- Safety mode.
- Active cutoff status.
- Input readings.
- Event messages.
- Fault messages.
- Error messages.

Serial output should make it obvious whether the firmware is in logging-only mode or active cutoff mode.

---

## Example Serial Output Concept

Example output format:

    boot firmware=LayzrSavre_Logger version=0.1.0 mode=LOGGING_ONLY
    safety active_cutoff=DISABLED board_profile=UNKNOWN
    time_ms=1000 event=LOGGING_STARTED
    time_ms=1200 focus_activity=ACTIVE track_activity=ACTIVE ps11_current_ma=0
    time_ms=5000 event=SUSPECT_FAULT reason=TRACK_NO_ACTIVITY
    time_ms=6000 event=CUTOFF_SIMULATED active_cutoff=DISABLED

This is only a concept and may change later.

---

## CSV Logging Concept

CSV logs may be useful for graphing and review.

Possible CSV columns:

| Column | Purpose |
|---|---|
| timestamp_ms | Time since ESP32 boot or test start |
| firmware_version | Firmware version |
| hardware_revision | Layzr Savre hardware revision |
| board_profile | PS2 board profile |
| focus_activity | Focus activity state |
| tracking_activity | Tracking activity state |
| ps11_current_ma | Estimated current through PS11 |
| driver_voltage_v | Driver IC voltage, if measured |
| fault_state | Current detection or fault state |
| event | Optional event label |
| notes | Optional note field |

CSV support can be added after basic serial output works.

---

## JSON Logging Concept

JSON logs may be useful for web interface or external tools.

Possible JSON fields:

- timestamp_ms
- firmware_version
- hardware_revision
- board_profile
- ps2_model
- board_revision
- focus_activity
- tracking_activity
- ps11_current_ma
- driver_voltage_v
- fault_state
- event_type
- notes

JSON support is optional and can come later.

---

## Web Interface Concept

A future web interface may provide a simple diagnostic page.

Possible web interface pages:

- Status page.
- Live data page.
- PS11 current page.
- Focus and tracking activity page.
- Event log page.
- Fault history page.
- Configuration page.
- Firmware information page.
- Safety warning page.

The web interface should not expose dangerous controls without safeguards.

---

## Web Interface Safety Rules

Future web interface safety rules:

- Active cutoff disabled by default.
- Unsupported board profiles locked to logging-only mode.
- Dangerous settings require confirmation.
- Active cutoff status shown clearly.
- Hardware cutoff enable state shown clearly.
- Firmware version shown clearly.
- Hardware revision shown clearly.
- Configuration reset option available.
- Invalid threshold values rejected.
- Safety warnings shown near active control settings.

The web interface should prevent mistakes.

---

## Board Profiles

Different PS2 boards may require different firmware settings.

Future board profiles may include:

- PS2 model.
- Board revision.
- Driver IC type.
- PS11 behavior.
- Focus input type.
- Tracking input type.
- Expected PS11 current range.
- Startup ignore time.
- Disc-detection ignore time.
- Fault confirmation time.
- Active cutoff allowed or disabled.
- Notes.

Unknown board profile should default to logging-only mode.

---

## Detection Logic

Detection logic is a future firmware feature.

Possible detection inputs:

- Focus activity.
- Tracking activity.
- PS11 current.
- Driver voltage.
- Timing windows.
- Board profile.
- Current threshold.
- Activity threshold.

Detection logic should begin in logging-only mode.

A suspected fault should be logged before any hardware action is allowed.

---

## Possible Detection States

Future detection states may include:

| State | Description |
|---|---|
| BOOT | ESP32 is starting |
| SAFE_IDLE | Firmware running with no active detection |
| LOGGING_ONLY | Logging data only |
| MONITORING | Watching conditioned inputs |
| ACTIVITY_PRESENT | Focus or tracking activity appears present |
| ACTIVITY_MISSING | Expected activity appears missing |
| CURRENT_NORMAL | PS11 current appears within expected range |
| CURRENT_ABNORMAL | PS11 current appears outside expected range |
| SUSPECT_FAULT | Possible fault detected |
| FAULT_CONFIRMED | Fault confirmed by timing and conditions |
| CUTOFF_SIMULATED | Firmware logs that cutoff would occur |
| CUTOFF_ACTIVE | Future hardware cutoff is active |
| FAULT_LATCHED | Fault remains active until reset |
| RECOVERY | System is recovering or waiting for reset |

Early firmware should only log these states.

---

## Fault Types

Future firmware may classify faults.

Possible fault types:

| Fault Type | Description |
|---|---|
| FOCUS_NO_ACTIVITY | Focus activity missing when expected |
| FOCUS_STUCK_HIGH | Focus signal appears stuck high |
| FOCUS_STUCK_LOW | Focus signal appears stuck low |
| TRACK_NO_ACTIVITY | Tracking activity missing when expected |
| TRACK_STUCK_HIGH | Tracking signal appears stuck high |
| TRACK_STUCK_LOW | Tracking signal appears stuck low |
| PS11_OVERCURRENT | PS11 current above expected range |
| PS11_UNDERRANGE | PS11 current below expected range during expected activity |
| DRIVER_VOLTAGE_FAULT | Driver IC voltage outside expected range |
| MULTI_SIGNAL_FAULT | Multiple monitored conditions suggest a fault |
| UNKNOWN_FAULT | Fault detected but not classified |

These names are placeholders.

---

## Timing Windows

Timing windows are needed to avoid false triggers.

Possible timing settings:

| Timing Setting | Purpose |
|---|---|
| STARTUP_IGNORE_MS | Ignore normal startup behavior |
| DISC_DETECT_IGNORE_MS | Ignore normal disc-detection behavior |
| RETRY_IGNORE_MS | Ignore normal retry pauses |
| FAULT_CONFIRM_MS | Require fault to remain long enough |
| FAULT_LATCH_MS | Keep fault state active |
| RECOVERY_DELAY_MS | Delay before allowing recovery |

Timing values must come from real test data.

---

## Configuration Storage

The ESP32 may eventually store settings.

Possible stored settings:

- Firmware mode.
- Board profile.
- Hardware revision.
- Current threshold.
- Activity threshold.
- Startup ignore time.
- Fault confirmation time.
- Logging format.
- Wi-Fi settings.
- Web interface setting.
- Active cutoff setting.
- User notes.

Settings must have safe defaults.

---

## Firmware Versioning

Firmware versions should be clear and consistent.

Suggested version format:

| Version | Meaning |
|---|---|
| 0.1.x | Bench test and basic serial logging |
| 0.2.x | PS11 current logging |
| 0.3.x | Focus and tracking activity logging |
| 0.4.x | Detection logic in logging-only mode |
| 0.5.x | Cutoff simulation mode |
| 0.6.x | Active cutoff test firmware |
| 0.9.x | Beta firmware |
| 1.0.x | Public release firmware |

Firmware should print its version at boot.

---

## Firmware Naming

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

Do not use the same name for logging-only firmware and active cutoff firmware.

---

## Build Information

Each firmware build should include:

- Firmware name.
- Firmware version.
- Build date.
- Target ESP32 board.
- Hardware revision.
- Active cutoff enabled or disabled.
- Git commit, if available.
- Notes.

This information should print at startup.

---

## PlatformIO Setup

This folder may use PlatformIO.

Possible basic setup steps:

1. Open the repository in VS Code.
2. Install the PlatformIO extension.
3. Open the `Firmware/ESP32/` folder.
4. Select the correct ESP32 environment.
5. Build the firmware.
6. Connect the ESP32.
7. Upload the firmware.
8. Open the serial monitor.

Exact instructions will be added after the target ESP32 board is selected.

---

## Example PlatformIO Environment

A future `platformio.ini` may include an ESP32 board target.

Example concept:

    [env:esp32dev]
    platform = espressif32
    board = esp32dev
    framework = arduino
    monitor_speed = 115200

This is only an example and may not be the final configuration.

---

## Serial Monitor Settings

Suggested early serial settings:

| Setting | Value |
|---|---|
| Baud rate | 115200 |
| Data bits | 8 |
| Parity | None |
| Stop bits | 1 |
| Line ending | Newline or both NL and CR |
| Flow control | None |

These settings may change later.

---

## Flashing Safety

Before flashing firmware while connected to Layzr Savre hardware:

- Confirm active cutoff is disabled.
- Confirm the PS2 is not relying on the ESP32.
- Confirm no GPIO boot state can affect the PS2.
- Confirm power domains are safe.
- Confirm firmware target matches the hardware.
- Confirm serial adapter voltage is correct.
- Confirm ground reference is safe.
- Confirm the ESP32 can enter bootloader mode.

When in doubt, flash the ESP32 disconnected from the PS2.

---

## Bench Testing

Before connecting to the PS2, firmware should be tested on the bench.

Bench test checklist:

- [ ] Firmware builds.
- [ ] Firmware uploads.
- [ ] ESP32 boots.
- [ ] Serial output works.
- [ ] Firmware version prints.
- [ ] Mode prints as logging-only or bench test.
- [ ] Inputs read expected dummy values.
- [ ] Outputs remain safe.
- [ ] Cutoff output remains disabled.
- [ ] Reset behavior is stable.
- [ ] No unexpected GPIO toggles are seen.

---

## Console Testing

After bench testing, firmware may be tested with the PS2 only when the hardware inputs are safe.

Console test checklist:

- [ ] PS2 works normally before connection.
- [ ] ESP32 firmware tested on bench.
- [ ] Input conditioning verified.
- [ ] Input voltage range verified.
- [ ] ESP32 ground reference verified.
- [ ] No backfeeding verified.
- [ ] Active cutoff disabled.
- [ ] Serial logging active.
- [ ] PS2 powers on normally.
- [ ] Optical drive behaves normally.
- [ ] Logs are collected.
- [ ] No abnormal heat or reset behavior.

---

## Data Logging Checklist

Before collecting logs:

- [ ] Firmware version documented.
- [ ] Hardware revision documented.
- [ ] PS2 model documented.
- [ ] Board revision documented.
- [ ] Disc type documented.
- [ ] Disc condition documented.
- [ ] Test duration documented.
- [ ] Logging mode documented.
- [ ] Active cutoff state documented.
- [ ] File name selected.
- [ ] Notes file prepared.

---

## Stop Testing If

Stop firmware testing immediately if:

- ESP32 becomes hot.
- ESP32 repeatedly resets.
- PS2 resets unexpectedly.
- Optical drive behaves abnormally.
- Serial output shows repeated errors.
- ADC readings are out of safe range.
- Fault triggers repeatedly without cause.
- Cutoff output changes unexpectedly.
- Voltage rails sag.
- Current draw becomes abnormal.
- Any sign of backfeeding is found.

Investigate before continuing.

---

## Current Source Files

Current source files:

| File | Status |
|---|---|
| platformio.ini | Planned |
| src/main.cpp | Planned |
| include/config.h | Planned |
| include/pins.h | Planned |
| include/version.h | Planned |

This table should be updated as files are added.

---

## Development Checklist

Firmware development checklist:

- [ ] Choose ESP32 target board.
- [ ] Create `platformio.ini`.
- [ ] Create basic `main.cpp`.
- [ ] Print firmware version at boot.
- [ ] Define safe pin states.
- [ ] Create pin assignment file.
- [ ] Add serial logging.
- [ ] Add bench test input readings.
- [ ] Add PS11 current input placeholder.
- [ ] Add focus activity input placeholder.
- [ ] Add tracking activity input placeholder.
- [ ] Add logging-only mode.
- [ ] Add cutoff disabled confirmation.
- [ ] Add configuration defaults.
- [ ] Add detection state placeholders.
- [ ] Add documentation for flashing.
- [ ] Add test log examples.

---

## Open Questions

Current firmware open questions:

- Which ESP32 module will be used first?
- Will the firmware use Arduino framework, ESP-IDF, or both?
- Which pins are safest for focus and tracking inputs?
- Which pin is safest for PS11 current ADC input?
- Is the ESP32 ADC good enough for current monitoring?
- Should an external ADC be used?
- What sample rate is needed?
- Should Wi-Fi be enabled in early firmware?
- Should the web interface come before or after detection?
- How should board profiles be stored?
- How should logs be exported?
- How should firmware updates be handled?
- How should active cutoff be locked out during development?
- What hardware jumper should be required for active cutoff?

---

## Current Working Theory

The current working theory is:

- ESP32 firmware should begin as a logger.
- Serial output should come before web interface.
- PS11 current should be logged only after proper conditioning.
- Focus and tracking activity should be logged only after safe signal conditioning.
- Detection should begin in logging-only mode.
- Cutoff simulation should come before real cutoff.
- Active cutoff should be disabled by default.
- Unknown board profiles should default to logging-only mode.
- Hardware must remain safe if firmware crashes or the ESP32 is unpowered.

This theory will be updated as firmware is developed.

---

## Future Firmware Goals

Future firmware may include:

- Serial logger.
- CSV logger.
- JSON logger.
- Web interface.
- Live status display.
- PS11 current display.
- Focus activity display.
- Tracking activity display.
- Voltage display.
- Fault event logging.
- Cutoff simulation.
- Active cutoff support after validation.
- Board profiles.
- Configurable thresholds.
- Firmware update support.
- Recovery mode.
- Factory reset option.
- Beta tester log export.

---

## Summary

The ESP32 firmware is planned to be the logging and interface side of Layzr Savre.

The first firmware should be safe, simple, and focused on data collection.

Active protection should not be enabled until the hardware, signals, current monitoring, detection logic, false-trigger behavior, and recovery behavior have been tested.

The firmware should help Layzr Savre become a reliable measurement system before it becomes a protection system.
