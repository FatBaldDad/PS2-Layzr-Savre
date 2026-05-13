# ESP32 Interface

**Project:** PS2 Layzr Savre  
**Owner:** FatBaldDad  
**Status:** Early research / planning / prototype development  
**Document:** 07 - ESP32 Interface  

---

## Overview

The ESP32 interface is planned to be the logging, communication, configuration, and user-interface side of the PS2 Layzr Savre project.

The interposer board and monitoring hardware will collect information from the PS2 optical-drive system. The ESP32 will be used to read, process, log, display, and eventually react to that information.

At this stage, the ESP32 should be treated as a research and telemetry controller first.

Active protection control should only be added after the monitored signals, detection logic, timing behavior, and cutoff hardware have been validated.

---

## Purpose of This Document

This document explains the planned role of the ESP32 in the Layzr Savre system.

It is intended to document:

- Why the ESP32 is being used.
- What information the ESP32 may monitor.
- What information the ESP32 may log.
- How the ESP32 may communicate with the console or user.
- How the ESP32 may support a future web interface.
- What safety concerns exist with ESP32 GPIO and ADC inputs.
- Why the ESP32 should not control protection hardware until the system is tested.
- What future firmware features may be developed.

This document should be updated as the hardware and firmware are developed.

---

## Main Role of the ESP32

The ESP32 is planned to act as the main interface controller for Layzr Savre.

Planned ESP32 roles include:

- Data logging.
- Signal monitoring.
- Current monitoring.
- Voltage monitoring.
- Fault-event recording.
- Serial debug output.
- Web interface hosting.
- Configuration storage.
- Future UART communication.
- Future protection control, only after validation.

The first ESP32 firmware should focus on observing and logging.

---

## What the ESP32 Should Do First

The first ESP32 development goal should be simple and safe.

Early firmware should:

- Boot reliably.
- Print serial debug information.
- Read safe, conditioned input signals.
- Log signal activity.
- Log PS11 current data after proper conditioning.
- Log voltage data where useful.
- Timestamp events.
- Store or stream test data.
- Avoid controlling PS2 hardware.
- Avoid cutting power.
- Avoid driving unknown PS2 signals.

The first firmware should be a logger, not a protection controller.

---

## What the ESP32 Should Not Do Yet

Early ESP32 firmware should not:

- Cut coil power.
- Cut driver IC power.
- Pull unknown PS2 signals high or low.
- Drive DSP signals.
- Drive Mechacon or Syscon signals.
- Directly connect to coil-drive outputs.
- Directly connect to the PS11 fuse path.
- Trigger protection from one signal alone.
- Assume current alone proves a fault.
- Assume coil activity alone proves a fault.
- Enable active protection by default.

Protection behavior should come after testing and validation.

---

## Planned ESP32 Inputs

The ESP32 may eventually receive several types of inputs.

| Input Area | Purpose | Status |
|---|---|---|
| Focus activity | Observe focusing coil behavior | Planned |
| Tracking activity | Observe tracking coil behavior | Planned |
| PS11 current sense | Monitor current through the PS11 fuse path | Planned |
| Driver IC voltage | Monitor driver IC supply behavior | Future research |
| General voltage rails | Monitor power stability | Future research |
| Fault detect input | Receive conditioned fault signal from analog hardware | Future research |
| Cutoff status input | Confirm whether cutoff circuit is active | Future research |
| Manual reset input | Allow clearing a latched fault | Future research |
| Mode select input | Choose logging, test, or protection mode | Future research |

All ESP32 inputs must be protected and conditioned before connection.

---

## Planned ESP32 Outputs

The ESP32 may eventually provide several outputs.

| Output Area | Purpose | Status |
|---|---|---|
| Serial debug output | Development logging | Planned |
| Web interface | User display and configuration | Planned |
| Fault LED output | Show warning or fault state | Future research |
| Buzzer or chime output | Optional fault or status alert | Future research |
| Cutoff control output | Future active protection control | Future research |
| Fault latch reset | Reset external latch if safe | Future research |
| UART communication | Communicate with console or external tools | Future research |

Any output that controls PS2 hardware must have a safe default state.

---

## Signal Conditioning Requirement

The ESP32 should not be connected directly to unknown PS2 optical-drive signals.

Many PS2 signals may be:

- Higher than ESP32-safe voltage.
- Analog.
- Differential.
- Noisy.
- Fast changing.
- Sensitive to loading.
- Connected to driver outputs.
- Connected to coils or motors.
- Unsafe for direct GPIO or ADC input.

Before a signal reaches the ESP32, it may need:

- High-impedance buffering.
- Voltage division.
- Level shifting.
- Filtering.
- Clamping.
- Differential measurement.
- Current-sense amplification.
- Isolation.
- External ADC conversion.
- Input protection resistors.
- ESD protection.

Signal conditioning should be designed and tested before firmware depends on the readings.

---

## ESP32 ADC Limitations

The ESP32 ADC can be useful for logging, but it has limitations.

Important concerns:

- ADC readings can be noisy.
- ADC accuracy is limited.
- ADC calibration may be required.
- Wi-Fi activity may affect readings.
- Input voltage must stay within safe limits.
- Fast signals may not be captured accurately.
- External analog front end may be needed.
- External ADC may be needed for better accuracy.

For PS11 current monitoring, the ESP32 should read a conditioned signal from a current-sense circuit, not the fuse path directly.

---

## ESP32 GPIO Safety

ESP32 GPIO pins can have special behavior during boot.

This matters because some pins may be high, low, floating, or used as strapping pins during startup.

Risks include:

- GPIO pin drives a signal before firmware starts.
- GPIO pin floats during boot.
- GPIO pin backfeeds an unpowered PS2 circuit.
- GPIO pin enables cutoff before intended.
- GPIO pin changes state during reset.
- GPIO pin causes the ESP32 to boot incorrectly.
- GPIO pin conflicts with flash, UART, or boot mode.

All GPIO assignments should be reviewed before hardware is finalized.

---

## Boot State Safety

The ESP32 does not start instantly.

During boot, the PS2 may already be powering up or attempting to use the optical drive.

The hardware must be safe while the ESP32 is:

- Off.
- Booting.
- Resetting.
- In bootloader mode.
- Browned out.
- Crashed.
- Reflashing firmware.
- Not connected.

The PS2 should not depend on the ESP32 being fully booted unless the design has been proven safe.

---

## Backfeeding Risk

Backfeeding happens when one circuit powers another circuit through a signal line.

This can happen if the ESP32 is powered while the PS2 is off, or if the PS2 is powered while the ESP32 is off.

Backfeeding risks include:

- Powering part of the PS2 through an ESP32 input.
- Powering part of the ESP32 through a PS2 signal.
- Causing undefined IC states.
- Creating partial power conditions.
- Damaging GPIO pins.
- Damaging PS2 circuitry.
- Causing strange startup behavior.

Input protection and proper power-domain design are required.

---

## Power Supply Considerations

The ESP32 needs a stable power source.

Power supply questions:

- Will the ESP32 be powered from the PS2?
- Will the ESP32 be powered from an external USB source?
- Will the ESP32 remain powered when the PS2 is off?
- Will the ESP32 share ground with the PS2?
- Will the ESP32 power supply create noise?
- Can the ESP32 brown out during Wi-Fi activity?
- Can the ESP32 regulator handle peak current?
- Can the ESP32 power system backfeed the console?

The power system should be documented for each hardware revision.

---

## Grounding Considerations

The ESP32 and PS2 measurement circuits need a proper ground reference.

Ground concerns include:

- Noisy ground reference.
- Long ground wires.
- Ground loops.
- Incorrect ground point.
- Shared high-current paths.
- Measurement error from ground offset.
- Noise injected into optical-drive circuits.

Every test log should document the ground reference used.

---

## Planned Data to Log

The ESP32 may eventually log several data types.

Possible logged data:

- Focus activity.
- Tracking activity.
- PS11 current.
- Driver IC voltage.
- Power rail voltage.
- Fault state.
- Fault duration.
- Startup timing.
- Disc-detection timing.
- Read-retry timing.
- Cutoff status.
- Firmware version.
- Hardware revision.
- Board profile.
- User configuration.
- Timestamped events.

Early logging should be simple and reliable.

---

## Logging Modes

Future firmware may include multiple logging modes.

| Mode | Purpose |
|---|---|
| Raw logging | Capture raw or lightly processed readings |
| Activity logging | Record whether focus or tracking activity is present |
| Current logging | Record PS11 current behavior |
| Voltage logging | Record voltage rail behavior |
| Event logging | Record startup, read, fault, and recovery events |
| Fault logging | Record suspected or confirmed fault conditions |
| Simulation logging | Record when cutoff would have happened without actually cutting power |

Logging-only modes should come before active protection modes.

---

## Serial Debug Interface

The first ESP32 interface should likely be serial output.

Serial output is useful because it is simple, reliable, and easy to test.

Possible serial output data:

- Firmware version.
- Hardware revision.
- Boot status.
- Signal readings.
- Current readings.
- Voltage readings.
- Fault state.
- Timing information.
- Configuration values.
- Debug messages.
- Error messages.

Serial output should be human-readable during early development.

---

## Web Interface Concept

A future ESP32 web interface may make Layzr Savre easier to use.

Possible web interface features:

- Live status page.
- Focus activity display.
- Tracking activity display.
- PS11 current display.
- Voltage display.
- Fault status display.
- Event log page.
- Configuration page.
- Threshold settings.
- Board profile selection.
- Export logs.
- Clear fault state.
- Firmware information.
- Safety warnings.

The web interface should not make unsafe options easy to enable by accident.

---

## Web Interface Safety

If a web interface is added, safety must be considered.

Important rules:

- Active cutoff should not be enabled by default.
- Dangerous settings should require confirmation.
- Experimental features should be clearly marked.
- Unsupported board profiles should be locked out or warned.
- Configuration should not allow impossible values.
- Fault thresholds should have safe limits.
- Logs should show hardware and firmware revision.
- The interface should clearly state whether the system is in logging-only mode or active protection mode.

The interface should help prevent mistakes, not create new ones.

---

## UART Communication Concept

Layzr Savre may eventually use UART communication where useful.

Possible UART uses:

- Development logging.
- Communication with external tools.
- Communication with another controller.
- Possible console-side communication if a safe and useful method is identified.
- Debugging during installation.
- Data export.

UART communication should be treated as optional until the exact use is defined.

The project should avoid assuming that UART access is available or needed on every console.

---

## Console Communication Caution

If Layzr Savre communicates with the console, the communication method must be researched carefully.

Concerns include:

- Voltage compatibility.
- Signal direction.
- Ground reference.
- Boot timing.
- Whether the console expects anything on that line.
- Whether the line is shared with service tools.
- Whether communication could interfere with normal operation.
- Whether the signal is safe across board revisions.

Console communication should not be required for the first versions.

---

## Firmware State Machine Concept

A future firmware state machine may help organize detection and logging.

Possible states:

| State | Description |
|---|---|
| BOOT | ESP32 is starting up |
| SAFE_IDLE | System is running but not actively detecting faults |
| LOGGING_ONLY | System is logging data only |
| MONITORING | System is watching conditioned inputs |
| ACTIVITY_PRESENT | Focus or tracking activity appears normal |
| ACTIVITY_MISSING | Expected activity appears missing |
| CURRENT_NORMAL | PS11 current appears within expected range |
| CURRENT_ABNORMAL | PS11 current appears outside expected range |
| SUSPECT_FAULT | A possible fault has been detected |
| FAULT_CONFIRMED | Detection timing and conditions confirm the fault |
| CUTOFF_SIMULATED | Firmware records that cutoff would have happened |
| CUTOFF_ACTIVE | Future hardware cutoff is active |
| FAULT_LATCHED | Fault remains active until reset |
| RECOVERY | System is recovering or waiting for user action |

Early firmware should log these states before controlling hardware.

---

## Detection Logic Role

The ESP32 may eventually run detection logic.

Possible detection logic may compare:

- Focus activity.
- Tracking activity.
- PS11 current.
- Timing.
- Voltage behavior.
- Startup ignore window.
- Disc-detection ignore window.
- Fault confirmation window.
- Board profile.
- User configuration.

The ESP32 should not declare a confirmed fault based on one short event.

---

## Logging-Only Detection

Before active protection is enabled, firmware should support logging-only detection.

In logging-only mode, the ESP32 may:

- Detect a suspected fault.
- Log the suspected fault.
- Record readings at the time of the event.
- Record how long the condition lasted.
- Record whether the condition cleared.
- Record whether cutoff would have been triggered.
- Avoid controlling the cutoff circuit.

This mode is important for reducing false triggers before active protection is tested.

---

## Cutoff Control Caution

A future ESP32 output may control a cutoff circuit.

This should only happen after:

- Passive monitoring is validated.
- PS11 current monitoring is validated.
- Detection logic is tested.
- False triggers are studied.
- Cutoff hardware is tested.
- Recovery behavior is understood.
- Board-revision compatibility is documented.

Cutoff control should require a deliberate hardware or firmware enable during development.

---

## Cutoff Enable Safety

A development board may include a physical cutoff enable jumper.

Possible behavior:

- Jumper not installed: logging and detection only.
- Jumper installed: active cutoff testing allowed.
- Firmware still requires active cutoff mode to be enabled.
- Web interface shows whether cutoff is physically enabled.
- Serial output reports whether cutoff is physically enabled.

This helps prevent accidental active protection during early testing.

---

## Fault Latching

The ESP32 may eventually support fault latching.

A latched fault means the system remains in a fault state until reset.

Possible reset methods:

- Console power cycle.
- ESP32 reset.
- Manual reset button.
- Web interface reset.
- Service-mode reset.
- Firmware command.
- Timed reset, only if proven safe.

Fault latching can help prevent rapid cycling during an unsafe condition.

---

## Configuration Storage

The ESP32 may eventually store configuration settings.

Possible settings:

- Board profile.
- Hardware revision.
- Current threshold.
- Activity threshold.
- Startup ignore time.
- Fault confirmation time.
- Logging mode.
- Web interface settings.
- Wi-Fi settings.
- Active cutoff enable setting.
- User notes.

Configuration must be handled carefully so bad settings do not create unsafe behavior.

---

## Board Profiles

Different PS2 board revisions may need different settings.

A future ESP32 firmware may support board profiles.

Possible board profile data:

- PS2 model.
- Board revision.
- Driver IC type.
- PS11 behavior.
- Focus signal input type.
- Tracking signal input type.
- Expected current range.
- Expected timing windows.
- Supported hardware revision.
- Known limitations.
- Active cutoff allowed or not allowed.

Unsupported board profiles should default to logging-only mode.

---

## Firmware Update Method

The ESP32 firmware will need a reliable update method.

Possible update methods:

- USB serial flashing.
- UART flashing.
- Web-based OTA update.
- Local file upload.
- Factory firmware image.
- Recovery firmware mode.

Early development should use the simplest reliable method.

Firmware flashing instructions should be documented before beta testing.

---

## Firmware File Organization

Suggested firmware folder structure:

- Firmware/ESP32/README.md
- Firmware/ESP32/src/
- Firmware/ESP32/include/
- Firmware/ESP32/lib/
- Firmware/ESP32/data/
- Firmware/ESP32/platformio.ini
- Firmware/Test-Firmware/README.md

This structure may change depending on whether PlatformIO, Arduino IDE, ESP-IDF, or another toolchain is used.

---

## Platform Choice

Possible firmware development platforms include:

| Platform | Notes |
|---|---|
| PlatformIO | Good project structure and library management |
| Arduino IDE | Simple and beginner-friendly |
| ESP-IDF | Most powerful and direct ESP32 development environment |
| ESPHome-style approach | Not currently planned |
| Custom build system | Not needed early on |

PlatformIO may be a good starting point because it keeps the firmware organized in the repo.

---

## Pin Assignment Documentation

Every ESP32 pin used by Layzr Savre should be documented.

Pin documentation should include:

- ESP32 pin number.
- Signal name.
- Input or output.
- Voltage range.
- Boot behavior.
- Pull-up or pull-down state.
- Whether it is a strapping pin.
- Whether it is ADC capable.
- Whether it needs protection.
- Whether it is safe during reset.
- Connected circuit.
- Notes.

Do not assign cutoff control to a pin without understanding its boot behavior.

---

## Suggested Pin Table Template

Use this table when assigning pins.

| ESP32 Pin | Signal Name | Direction | Function | Boot Concern | Notes |
|---|---|---|---|---|---|
| TBD | FOCUS_ACTIVITY | Input | Focus activity monitor | Unknown | Requires conditioning |
| TBD | TRACK_ACTIVITY | Input | Tracking activity monitor | Unknown | Requires conditioning |
| TBD | PS11_CURRENT | Input | Current sense ADC | Unknown | Requires amplifier or conditioning |
| TBD | DRIVER_VOLTAGE | Input | Voltage sense ADC | Unknown | Optional |
| TBD | FAULT_LED | Output | Fault indicator | Unknown | Must default safe |
| TBD | CUTOFF_ENABLE | Output | Future cutoff control | High risk | Must default safe |
| TBD | MANUAL_RESET | Input | Clear latched fault | Unknown | Optional |
| TBD | UART_TX | Output | Serial debug | Low risk | Development use |
| TBD | UART_RX | Input | Serial debug | Low risk | Development use |

This table should be updated when actual pins are selected.

---

## Data Format Concept

The ESP32 should eventually output logs in a consistent format.

Possible log formats:

- Human-readable serial text.
- CSV.
- JSON.
- Simple event list.
- Binary log file, only if needed later.

Early logs should be easy to read.

Example fields to include:

- Timestamp.
- Firmware version.
- Hardware revision.
- PS2 model.
- Board profile.
- Focus activity.
- Tracking activity.
- PS11 current.
- Driver voltage.
- Fault state.
- Event type.
- Notes.

---

## Event Types

Possible event types:

| Event Type | Description |
|---|---|
| BOOT | ESP32 started |
| CONFIG_LOADED | Settings loaded |
| LOGGING_STARTED | Logging began |
| DISC_ACTIVITY | Drive activity detected |
| FOCUS_ACTIVITY | Focus activity detected |
| TRACK_ACTIVITY | Tracking activity detected |
| CURRENT_SAMPLE | PS11 current sample recorded |
| SUSPECT_FAULT | Possible fault detected |
| FAULT_CONFIRMED | Fault confirmed by detection rules |
| CUTOFF_SIMULATED | Cutoff would have triggered |
| CUTOFF_ACTIVE | Future cutoff activated |
| FAULT_CLEARED | Fault cleared or reset |
| ERROR | Firmware or hardware error |

These names are placeholders.

---

## Test Data Context

Every ESP32 log should include enough context to be useful.

Useful context:

- PS2 model.
- Board revision.
- Driver IC marking.
- Laser model.
- Optical-drive assembly.
- Layzr Savre hardware revision.
- ESP32 firmware revision.
- Current-sense method.
- Signal-conditioning method.
- Disc type.
- Disc condition.
- Power supply.
- Test duration.
- Notes.

Without context, logs may be difficult to compare.

---

## ESP32 Test Template

Use this template when documenting ESP32 interface tests.

## ESP32 Interface Test Entry

### Console Information

- PS2 model:
- Board revision:
- Region:
- Driver IC marking:
- DSP marking:
- Optical-drive assembly:
- Laser model:
- Other mods installed:

### Layzr Savre Hardware

- Interposer revision:
- ESP32 board revision:
- Current-sense method:
- Signal-conditioning method:
- Cutoff hardware installed:
- Cutoff enabled:

### ESP32 Firmware

- Firmware name:
- Firmware version:
- Build date:
- Logging mode:
- Detection mode:
- Web interface enabled:
- Active cutoff enabled:

### Pin Assignments

- Focus input:
- Tracking input:
- PS11 current input:
- Voltage input:
- Fault LED:
- Cutoff control:
- Reset input:
- UART TX:
- UART RX:

### Test Condition

- Disc type:
- Disc condition:
- Console state:
- Power supply:
- Test duration:

### Observed Behavior

- ESP32 booted normally:
- Serial output working:
- Web interface working:
- Focus data logged:
- Tracking data logged:
- PS11 current logged:
- Voltage logged:
- Suspected faults logged:
- False triggers observed:
- Console behavior affected:

### Conclusion

- Firmware stable:
- Input readings useful:
- Noise level acceptable:
- More filtering needed:
- More calibration needed:
- Safe for further testing:
- Follow-up needed:

---

## Early Firmware Development Checklist

Before using ESP32 firmware on a console:

- [ ] Confirm firmware builds successfully.
- [ ] Confirm serial output works.
- [ ] Confirm GPIO assignments are documented.
- [ ] Confirm no cutoff output is enabled by default.
- [ ] Confirm unused outputs are safe.
- [ ] Confirm ADC inputs are protected.
- [ ] Confirm input voltage levels are safe.
- [ ] Confirm ESP32 power is stable.
- [ ] Confirm no backfeeding occurs.
- [ ] Confirm logging works without the PS2 connected.
- [ ] Confirm firmware can recover after reset.
- [ ] Confirm firmware version is printed at boot.

---

## Early Hardware Safety Checklist

Before connecting the ESP32 to the PS2:

- [ ] Confirm PS2 board revision.
- [ ] Confirm ground reference.
- [ ] Confirm ESP32 power source.
- [ ] Confirm no shared power issue.
- [ ] Confirm signal conditioning is installed.
- [ ] Confirm input voltage range.
- [ ] Confirm input protection.
- [ ] Confirm no GPIO can drive the PS2 signal.
- [ ] Confirm current-sense output is safe for ESP32 input.
- [ ] Confirm cutoff hardware is disabled.
- [ ] Confirm wires are secured.
- [ ] Confirm no mechanical interference.

---

## Stop Testing If

Stop ESP32 testing immediately if:

- ESP32 becomes unusually hot.
- ESP32 repeatedly resets.
- PS2 resets unexpectedly.
- Optical drive behaves abnormally.
- ADC readings are clearly out of range.
- Input protection parts become hot.
- Voltage rails sag.
- Current draw becomes abnormal.
- Web interface changes settings unexpectedly.
- Cutoff output changes state unexpectedly.
- Serial output shows repeated errors.
- Any signal appears to be backfeeding.

Investigate before continuing.

---

## Open Questions

Current open questions for the ESP32 interface:

- Which ESP32 module should be used for the first prototype?
- Should the project use ESP32, ESP32-S3, or another variant?
- Which GPIO pins are safest for inputs?
- Which GPIO pins are safest for future cutoff control?
- Should PS11 current use ESP32 ADC or an external ADC?
- What sample rate is needed?
- What signal conditioning is required for focus activity?
- What signal conditioning is required for tracking activity?
- Is Wi-Fi needed during early logging?
- Should logs be saved locally or streamed over serial?
- Should a web interface be included in early firmware?
- Should board profiles be stored in flash?
- How should firmware updates be handled?
- How should active cutoff be locked out during development?

---

## Current Working Theory

The current working theory is:

- The ESP32 should first be used as a logger and diagnostic tool.
- PS2 signals should be conditioned before reaching the ESP32.
- PS11 current should be measured through a safe current-sense circuit, not directly.
- Firmware should begin with serial logging.
- Web interface features can come later.
- Detection should begin in logging-only mode.
- Active cutoff should be disabled by default.
- Hardware should remain safe if the ESP32 is off, booting, or crashed.
- Board profiles may be needed for different PS2 revisions.

This theory must be tested.

---

## Future Firmware Goals

Future ESP32 firmware may include:

- Serial logging.
- Web interface.
- Live signal display.
- PS11 current display.
- Voltage display.
- Fault detection.
- Logging-only detection mode.
- Cutoff simulation mode.
- Active cutoff mode with hardware enable.
- Fault latch.
- Manual reset.
- Board profiles.
- Configurable thresholds.
- Log export.
- Firmware update support.
- Safety lockout for unsupported boards.

---

## Future Hardware Goals

Future ESP32 interface hardware may include:

- Dedicated ESP32 module footprint.
- Protected input circuits.
- Current-sense amplifier input.
- External ADC.
- Voltage monitoring dividers.
- Focus activity input.
- Tracking activity input.
- Fault LED.
- Manual reset button.
- Cutoff enable jumper.
- Cutoff control output.
- UART header.
- USB programming header.
- Test pads.
- Clear silkscreen labels.
- Strain relief points.
- Power-domain protection.

---

## Documentation Requirements Before Beta

Before any beta tester uses the ESP32 interface, documentation should include:

- Firmware flashing guide.
- Pin assignment table.
- Hardware revision notes.
- Input voltage limits.
- Current-sense setup.
- Logging instructions.
- Serial monitor instructions.
- Web interface instructions, if used.
- Safe startup procedure.
- Known issues.
- Recovery procedure.
- Cutoff enable warning.
- Supported board profiles.
- Unsupported board profiles.

---

## Summary

The ESP32 interface is planned to be the logging, communication, configuration, and future control center for Layzr Savre.

Early development should use the ESP32 for safe observation only.

The ESP32 should log focus activity, tracking activity, PS11 current, voltage behavior, timing, and suspected fault events after the signals are properly conditioned.

Active cutoff control should only be added after the hardware, firmware, detection logic, and recovery behavior are tested and documented.

The ESP32 should make Layzr Savre easier to understand, not more dangerous to install or use.
