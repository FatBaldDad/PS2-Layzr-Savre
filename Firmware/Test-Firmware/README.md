# Test Firmware

**Project:** PS2 Layzr Savre  
**Owner:** FatBaldDad  
**Status:** Early research / planning / prototype development  
**Folder:** Firmware/Test-Firmware  

---

## Overview

This folder will contain experimental, temporary, and proof-of-concept firmware used during PS2 Layzr Savre development.

Test firmware is separate from the main ESP32 firmware because it may be incomplete, unsafe for normal use, board-specific, or created only for a single experiment.

At this stage, all test firmware should be treated as experimental.

Do not use test firmware on valuable consoles, customer consoles, or finished builds unless the behavior is fully understood and documented.

---

## Purpose of This Folder

The purpose of this folder is to keep development and experiment firmware organized.

Test firmware may be used for:

- ESP32 bench testing.
- Pin behavior testing.
- ADC testing.
- PS11 current-monitoring experiments.
- Focus activity input testing.
- Tracking activity input testing.
- Signal-conditioning tests.
- Serial logging tests.
- Web interface experiments.
- Flatline detection experiments.
- Cutoff simulation experiments.
- Active cutoff experiments on sacrificial hardware only.

Test firmware should help prove ideas before they are moved into the main firmware folder.

---

## Important Safety Notice

Test firmware may behave unpredictably.

Test firmware may:

- Use temporary pin assignments.
- Output unexpected GPIO states.
- Lack safety checks.
- Lack board-profile protection.
- Lack cutoff lockout logic.
- Use untested thresholds.
- Log incomplete data.
- Miss fault conditions.
- False-trigger during normal behavior.
- Reset unexpectedly.
- Be written for only one test setup.

Do not assume test firmware is safe just because it compiles.

---

## Test Firmware Rules

All test firmware should follow these rules:

1. Clearly state what the firmware is for.
2. Clearly state which hardware it was tested with.
3. Clearly state whether active cutoff is disabled or enabled.
4. Default to logging-only behavior whenever possible.
5. Avoid driving PS2 signals unless the test specifically requires it.
6. Avoid active cutoff unless testing on sacrificial hardware.
7. Print firmware name and version at boot.
8. Document pin assignments.
9. Document known risks.
10. Do not move test code into main firmware until reviewed.

---

## Recommended Folder Structure

Suggested folder structure:

    Firmware/Test-Firmware/
    ├── README.md
    ├── Bench-Test/
    ├── ADC-Test/
    ├── PS11-Current-Test/
    ├── Focus-Activity-Test/
    ├── Tracking-Activity-Test/
    ├── Signal-Conditioning-Test/
    ├── Flatline-Detection-Test/
    ├── Cutoff-Simulation-Test/
    ├── Active-Cutoff-Test/
    └── Archived-Tests/

This structure can change as the project develops.

---

## Possible Test Firmware Types

| Test Firmware | Purpose | Active Cutoff |
|---|---|---|
| Bench Test | Confirm ESP32 boots and serial output works | Disabled |
| Pin State Test | Check GPIO startup and reset behavior | Disabled |
| ADC Test | Test analog readings and noise | Disabled |
| PS11 Current Test | Test current-sense input behavior | Disabled |
| Focus Activity Test | Test conditioned focus activity input | Disabled |
| Tracking Activity Test | Test conditioned tracking activity input | Disabled |
| Signal Conditioning Test | Test buffers, filters, comparators, or amplifiers | Disabled |
| Logger Test | Test serial, CSV, or JSON logging | Disabled |
| Flatline Detection Test | Test suspected fault detection in logging-only mode | Disabled |
| Cutoff Simulation Test | Log when cutoff would have happened | Disabled |
| Active Cutoff Test | Test real cutoff on sacrificial hardware only | Optional with hardware enable |

---

## Bench Test Firmware

Bench test firmware should be the first test firmware created.

Purpose:

- Confirm the ESP32 boots.
- Confirm serial output works.
- Confirm firmware version prints.
- Confirm basic timing works.
- Confirm no unsafe GPIO outputs are active.
- Confirm the board can be flashed and reset.

Bench test firmware should not connect to PS2 optical-drive signals.

---

## Pin State Test Firmware

Pin state test firmware may be used to confirm ESP32 GPIO behavior.

Purpose:

- Check GPIO boot states.
- Check reset behavior.
- Check whether pins pulse during boot.
- Check internal pull-ups and pull-downs.
- Check which pins are safe for inputs.
- Check which pins should not be used for cutoff control.
- Check whether any pin affects boot mode.

This test is important before assigning any future cutoff or fault-control pin.

---

## ADC Test Firmware

ADC test firmware may be used to study ESP32 analog input behavior.

Purpose:

- Read ADC values.
- Measure noise.
- Test voltage dividers.
- Test current-sense amplifier output.
- Test calibration values.
- Compare ESP32 readings to a multimeter or oscilloscope.
- Determine whether an external ADC is needed.

ADC testing should be done on safe bench signals before connecting to the PS2.

---

## PS11 Current Test Firmware

PS11 current test firmware may be used to log current-sense data from the PS11 fuse path.

Important note:

PS11 is a physical fuse on the PS2 motherboard that provides power to the driver IC in the area being studied.

The current plan is to lift one side of PS11 and use that fuse location as a current-monitoring point.

PS11 current test firmware should only read a properly conditioned current-sense signal.

It should not connect directly to the PS11 fuse path.

Purpose:

- Log shunt voltage.
- Estimate PS11 current.
- Compare current during different drive states.
- Test current-sense amplifier behavior.
- Test ADC filtering.
- Test current logging format.
- Compare good-read and failed-read behavior.

Active cutoff should remain disabled.

---

## Focus Activity Test Firmware

Focus activity test firmware may be used to test a conditioned focus activity input.

Purpose:

- Read focus activity state.
- Detect signal changes.
- Log activity present or missing.
- Test activity threshold.
- Test filtering.
- Compare startup, no-disc, and read behavior.
- Check for false activity readings.

The ESP32 should only receive a safe conditioned signal.

Do not connect raw focus coil outputs directly to the ESP32.

---

## Tracking Activity Test Firmware

Tracking activity test firmware may be used to test a conditioned tracking activity input.

Purpose:

- Read tracking activity state.
- Detect signal changes.
- Log activity present or missing.
- Test activity threshold.
- Test filtering.
- Compare normal read and failed-read behavior.
- Check for false activity readings.

The ESP32 should only receive a safe conditioned signal.

Do not connect raw tracking coil outputs directly to the ESP32.

---

## Signal Conditioning Test Firmware

Signal conditioning test firmware may be used to validate the analog front end.

Possible circuits to test:

- High-impedance buffers.
- Voltage dividers.
- RC filters.
- Comparators.
- Differential amplifiers.
- Current-sense amplifiers.
- Clamp circuits.
- External ADCs.
- Activity detectors.
- Envelope detectors.

Purpose:

- Confirm output voltage is safe for ESP32.
- Confirm signal is readable.
- Confirm noise is acceptable.
- Confirm filtering does not hide useful events.
- Confirm circuit does not load the PS2 signal.
- Confirm readings match oscilloscope behavior.

---

## Logger Test Firmware

Logger test firmware may be used to test output formats.

Possible formats:

- Human-readable serial text.
- CSV.
- JSON.
- Event log format.
- Fault log format.
- Web interface output.

Purpose:

- Confirm logs are readable.
- Confirm timestamps work.
- Confirm file or serial output is consistent.
- Confirm important context is included.
- Confirm logs can be reviewed later.

Early logging should prioritize clarity over complexity.

---

## Flatline Detection Test Firmware

Flatline detection test firmware is used to test detection logic without active cutoff.

Purpose:

- Watch focus activity.
- Watch tracking activity.
- Watch PS11 current.
- Apply startup ignore timing.
- Apply disc-detection ignore timing.
- Apply fault confirmation timing.
- Log suspected faults.
- Log false triggers.
- Log missed suspicious behavior.
- Compare detection behavior to real test data.

Active cutoff must remain disabled in early flatline detection firmware.

---

## Cutoff Simulation Test Firmware

Cutoff simulation firmware logs when cutoff would have happened, but does not actually cut power.

Purpose:

- Test detection thresholds.
- Test timing windows.
- Test false-trigger behavior.
- Test suspected fault logging.
- Test board-profile assumptions.
- Test current and activity combinations.
- Prepare for future cutoff testing.

Cutoff simulation is an important step before active cutoff.

---

## Active Cutoff Test Firmware

Active cutoff test firmware is high risk.

It should only be used when:

- Testing on sacrificial hardware.
- The cutoff circuit is installed correctly.
- A physical cutoff enable jumper is installed.
- The cutoff point has been verified.
- Detection logic has already been tested in logging-only mode.
- Cutoff simulation has already been tested.
- Recovery behavior is documented.
- The tester understands the risk.

Active cutoff test firmware should never be confused with normal logging firmware.

---

## Firmware Naming Convention

Test firmware should use clear names.

Suggested names:

- LayzrSavre_BenchTest
- LayzrSavre_PinStateTest
- LayzrSavre_ADCTest
- LayzrSavre_PS11CurrentTest
- LayzrSavre_FocusActivityTest
- LayzrSavre_TrackingActivityTest
- LayzrSavre_SignalConditioningTest
- LayzrSavre_LoggerTest
- LayzrSavre_FlatlineDetectionTest
- LayzrSavre_CutoffSimulationTest
- LayzrSavre_ActiveCutoffTest

Do not use vague names such as `test`, `new`, `final`, or `working`.

---

## Firmware Versioning

Suggested test firmware version format:

| Version | Meaning |
|---|---|
| 0.0.x | Quick bench experiments |
| 0.1.x | Basic test firmware |
| 0.2.x | Improved logging |
| 0.3.x | Input-specific testing |
| 0.4.x | Detection testing |
| 0.5.x | Cutoff simulation testing |
| 0.6.x | Active cutoff testing on sacrificial hardware |

Every test firmware should print its name and version at boot.

---

## Required Header Comment

Each test firmware file should include a header comment with this information:

    Firmware Name:
    Firmware Version:
    Project:
    Purpose:
    Target ESP32 Board:
    Layzr Savre Hardware Revision:
    Active Cutoff Enabled:
    Tested On:
    Known Risks:
    Notes:

This helps avoid confusion later.

---

## Required README for Each Test

Each test firmware folder should include its own README file.

That README should include:

- Firmware name.
- Purpose.
- Target hardware.
- Required wiring.
- Pin assignments.
- Active cutoff status.
- Required test equipment.
- Flashing instructions.
- Expected serial output.
- Safety notes.
- Test procedure.
- Known issues.
- Results, if tested.

---

## Pin Assignment Requirement

Every test firmware must document pin assignments.

Pin table template:

| ESP32 Pin | Signal Name | Direction | Purpose | Boot Concern | Notes |
|---|---|---|---|---|---|
| TBD | TEST_INPUT | Input | Test input signal | Unknown | Example |
| TBD | SERIAL_TX | Output | Serial debug | Low risk | Example |
| TBD | FAULT_LED | Output | Test LED | Unknown | Example |
| TBD | CUTOFF_CONTROL | Output | Active cutoff test only | High risk | Disabled unless required |

Do not use a pin for cutoff testing until its boot behavior is understood.

---

## Active Cutoff Status Requirement

Every test firmware README should clearly state one of the following:

| Status | Meaning |
|---|---|
| Active cutoff not present | Firmware has no cutoff code |
| Active cutoff disabled | Firmware contains cutoff code but it is disabled |
| Cutoff simulation only | Firmware logs cutoff events but does not cut power |
| Active cutoff enabled | Firmware can control cutoff hardware |
| Active cutoff dangerous | Firmware is experimental and high risk |

This should be shown near the top of each test firmware README.

---

## Safe Default Requirement

Test firmware should default to safe behavior.

Safe default examples:

- Active cutoff disabled.
- GPIO outputs low or high only when safe.
- Unknown board profile locked out.
- No automatic hardware control.
- Serial output confirms mode.
- Firmware waits before monitoring.
- Firmware prints warnings at boot.
- Manual enable required for risky functions.

Do not assume a tester will remember which firmware is dangerous.

---

## Example Boot Message

Test firmware should print a clear boot message.

Example:

    boot firmware=LayzrSavre_PS11CurrentTest version=0.1.0
    mode=LOGGING_ONLY active_cutoff=DISABLED
    hardware=PROTO board_profile=UNKNOWN
    warning=TEST_FIRMWARE_NOT_FOR_PUBLIC_RELEASE

For active cutoff test firmware, the warning should be much stronger.

---

## Example Active Cutoff Warning

Active cutoff test firmware should print a warning like this:

    WARNING: ACTIVE CUTOFF TEST FIRMWARE
    USE ONLY ON SACRIFICIAL HARDWARE
    CONFIRM CUTOFF ENABLE JUMPER BEFORE TESTING
    DO NOT USE ON CUSTOMER OR VALUABLE CONSOLES

The firmware should make the risk obvious.

---

## Bench Testing Requirement

Before connecting any test firmware to a PS2:

- [ ] Firmware builds successfully.
- [ ] Firmware uploads successfully.
- [ ] ESP32 boots.
- [ ] Serial output works.
- [ ] Firmware name prints.
- [ ] Firmware version prints.
- [ ] Active cutoff status prints.
- [ ] GPIO default states are checked.
- [ ] No unexpected outputs are active.
- [ ] Inputs read safe bench signals correctly.
- [ ] Firmware can reset without unsafe behavior.

---

## Console Testing Requirement

Before using test firmware with a PS2:

- [ ] Console works normally before connection.
- [ ] Board revision is documented.
- [ ] ESP32 power is stable.
- [ ] Ground reference is confirmed.
- [ ] Inputs are conditioned.
- [ ] Input voltage range is safe.
- [ ] No backfeeding is present.
- [ ] Active cutoff is disabled unless intentionally testing it.
- [ ] Serial logging is working.
- [ ] Wires are secured.
- [ ] No mechanical interference exists.
- [ ] Stop-testing plan is understood.

---

## PS11 Current Test Requirement

Before using PS11 current test firmware:

- [ ] PS11 location is confirmed.
- [ ] PS11 is confirmed as a physical fuse.
- [ ] One side of PS11 is lifted only if required for the test.
- [ ] Current-sense path is installed correctly.
- [ ] Shunt value is documented.
- [ ] Shunt power rating is documented.
- [ ] Sense amplifier or ADC input is protected.
- [ ] Fuse protection role is considered.
- [ ] Voltage drop is checked.
- [ ] Current-sense signal is safe for ESP32 input.
- [ ] Active cutoff is disabled.

---

## Focus and Tracking Test Requirement

Before using focus or tracking activity test firmware:

- [ ] Signal point is identified.
- [ ] Signal is not connected directly to ESP32.
- [ ] Signal-conditioning circuit is installed.
- [ ] Output voltage is safe for ESP32 input.
- [ ] Ground reference is confirmed.
- [ ] Oscilloscope behavior is reviewed.
- [ ] Input threshold is documented.
- [ ] Test condition is documented.
- [ ] Active cutoff is disabled.

---

## Cutoff Simulation Test Requirement

Before using cutoff simulation firmware:

- [ ] Passive monitoring data has been collected.
- [ ] PS11 current data has been collected.
- [ ] Focus and tracking inputs are conditioned.
- [ ] Detection thresholds are documented.
- [ ] Startup ignore time is documented.
- [ ] Fault confirmation time is documented.
- [ ] Active cutoff is disabled.
- [ ] Firmware clearly prints cutoff simulation mode.
- [ ] False triggers will be logged.

---

## Active Cutoff Test Requirement

Before using active cutoff test firmware:

- [ ] Sacrificial console is used.
- [ ] Active cutoff hardware is installed.
- [ ] Cutoff point is verified.
- [ ] Cutoff enable jumper is installed intentionally.
- [ ] Manual override is available.
- [ ] Fault indicator is working.
- [ ] Detection logic has already been tested.
- [ ] Cutoff simulation has already been tested.
- [ ] Recovery behavior is planned.
- [ ] Emergency power-off method is ready.
- [ ] Tester understands risk.

Active cutoff test firmware should not be used casually.

---

## Stop Testing If

Stop testing immediately if:

- ESP32 becomes hot.
- ESP32 repeatedly resets.
- PS2 resets unexpectedly.
- Optical drive behaves abnormally.
- PS11 area becomes hot.
- Shunt becomes hot.
- Driver IC becomes unusually hot.
- Voltage rails sag.
- Current draw becomes abnormal.
- Firmware prints repeated errors.
- Fault triggers repeatedly without cause.
- Cutoff output changes unexpectedly.
- A wire disconnects.
- A short is suspected.
- Smoke or burning smell occurs.

Investigate before continuing.

---

## Test Firmware Log Template

Use this template when documenting a test firmware run.

## Test Firmware Run

### Firmware Information

- Firmware name:
- Firmware version:
- Build date:
- Target ESP32 board:
- Active cutoff status:
- Test firmware folder:

### Hardware Information

- Layzr Savre hardware revision:
- ESP32 board:
- PS2 model:
- Board revision:
- Driver IC marking:
- Laser model:
- Other mods installed:

### Wiring and Inputs

- Focus input:
- Tracking input:
- PS11 current input:
- Driver voltage input:
- Cutoff output:
- Fault LED:
- Ground reference:
- Power source:

### Test Condition

- Bench test or console test:
- Disc type:
- Disc condition:
- Console state:
- Test duration:

### Observed Behavior

- Firmware booted:
- Serial output worked:
- Inputs read correctly:
- Logs were useful:
- False triggers:
- Resets:
- Heat:
- Console behavior affected:
- Active cutoff occurred:

### Files Collected

- Serial log:
- Scope capture:
- Current measurement:
- Photos:
- Notes:

### Conclusion

- Test passed:
- Test failed:
- Firmware safe for next test:
- Firmware should be archived:
- Firmware should be revised:
- Follow-up needed:

---

## Moving Test Firmware to Main Firmware

Test firmware should only be moved into the main ESP32 firmware after review.

Before moving code:

- [ ] Purpose is clear.
- [ ] Code is stable.
- [ ] Pin assignments are safe.
- [ ] Active cutoff behavior is understood.
- [ ] Logging format is useful.
- [ ] Safety checks are added.
- [ ] Known issues are documented.
- [ ] Test results are recorded.
- [ ] Code is cleaned up.
- [ ] Version number is updated.
- [ ] Main firmware README is updated.

Do not move messy test code into the main firmware without cleanup.

---

## Archiving Test Firmware

Old test firmware should not be deleted immediately if it documents a useful experiment.

Archive old firmware when:

- It has been replaced by better test firmware.
- It was used for a specific test that is complete.
- It is unsafe but historically useful.
- It contains a failed approach worth remembering.
- It helps explain a design decision.

Archived firmware should include notes explaining why it was archived.

---

## What Not to Store Here

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

This folder is only for Layzr Savre development firmware.

---

## Suggested First Test Firmware

The first test firmware should probably be:

    LayzrSavre_BenchTest

Purpose:

- Confirm ESP32 boot.
- Confirm serial output.
- Confirm safe default pin states.
- Print firmware name and version.
- Print active cutoff disabled.
- Provide a foundation for later tests.

This should be done before any PS2 signals are connected.

---

## Suggested Early Test Order

Recommended early test order:

1. Bench test firmware.
2. Pin state test firmware.
3. ADC test firmware.
4. Logger test firmware.
5. PS11 current test firmware, after safe current-sense hardware exists.
6. Focus activity test firmware, after signal conditioning exists.
7. Tracking activity test firmware, after signal conditioning exists.
8. Flatline detection test firmware in logging-only mode.
9. Cutoff simulation test firmware.
10. Active cutoff test firmware only on sacrificial hardware.

---

## Open Questions

Current open questions:

- Which ESP32 board should be used for the first bench test?
- Which pins are safest for test inputs?
- Which pins should be avoided completely?
- Should test firmware use PlatformIO from the beginning?
- Should each test firmware be a separate PlatformIO project or shared project?
- Should test firmware share code with main firmware?
- How should active cutoff test firmware be locked out?
- How should test logs be named?
- Should test firmware output CSV, JSON, or plain text first?
- Should web interface tests be separate from logging tests?
- How should archived test firmware be documented?

---

## Current Working Theory

The current working theory is:

- Test firmware should be separated from main firmware.
- Bench testing should happen before console testing.
- Active cutoff should be disabled by default.
- GPIO boot behavior must be checked before hardware control.
- PS11 current test firmware should only read conditioned signals.
- Focus and tracking test firmware should only read conditioned signals.
- Flatline detection should begin in logging-only mode.
- Cutoff simulation should come before active cutoff.
- Active cutoff test firmware should only be used on sacrificial hardware.
- Unsafe or old test firmware should be archived with notes.

This theory will be updated as development continues.

---

## Summary

The Test Firmware folder is for experiments, proof-of-concept code, and hardware validation during Layzr Savre development.

Test firmware should be clearly named, clearly documented, and clearly marked as safe or unsafe.

The first test firmware should focus on ESP32 boot, serial output, and safe pin behavior.

More advanced test firmware can be added later for PS11 current monitoring, focus and tracking activity, flatline detection, cutoff simulation, and active cutoff testing.

Active cutoff firmware should only be used after careful validation and only on sacrificial hardware.
