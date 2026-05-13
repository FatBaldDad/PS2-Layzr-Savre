# Testing Plan

**Project:** PS2 Layzr Savre  
**Owner:** FatBaldDad  
**Status:** Early research / planning / prototype development  
**Document:** 09 - Testing Plan  

---

## Overview

Testing is one of the most important parts of the PS2 Layzr Savre project.

Layzr Savre should not become an active protection product until the optical-drive signals, PS11 current behavior, ESP32 logging, flatline detection logic, and future cutoff method have been tested carefully.

The goal of this testing plan is to create a repeatable process for collecting useful data and reducing the risk of damaging PS2 hardware during development.

At this stage, testing should focus on observation, logging, and validation.

Active cutoff testing should come later.

---

## Purpose of This Document

This document explains the planned testing process for Layzr Savre.

It is intended to document:

- What should be tested first.
- What should not be tested yet.
- What tools are recommended.
- What safety checks should happen before power-on.
- What optical-drive states should be measured.
- What PS11 current data should be collected.
- What focus and tracking data should be collected.
- How ESP32 logging should be tested.
- How flatline detection should be validated.
- How future cutoff testing should be approached.
- How test results should be recorded.

This document should be updated as the project develops.

---

## Testing Philosophy

Layzr Savre should be tested in stages.

The safest testing order is:

1. Confirm the console works before modification.
2. Inspect and document the board revision.
3. Test passive monitoring only.
4. Confirm the console still works normally.
5. Collect focus and tracking signal data.
6. Add PS11 current monitoring.
7. Confirm current monitoring does not affect normal operation.
8. Add ESP32 logging only after signals are conditioned.
9. Test detection logic in logging-only mode.
10. Simulate cutoff events before enabling real cutoff.
11. Test active cutoff only on sacrificial hardware.
12. Validate recovery behavior.
13. Repeat across multiple PS2 models and board revisions.

The project should observe first, log second, detect third, and cut power last.

---

## Testing Stages

| Stage | Name | Purpose | Status |
|---|---|---|---|
| Stage 0 | Baseline Console Test | Confirm the console works before Layzr Savre is installed | Planned |
| Stage 1 | Board Documentation | Record PS2 model, board revision, driver IC, and laser details | Planned |
| Stage 2 | Passive Signal Test | Observe focus and tracking behavior without control | Planned |
| Stage 3 | PS11 Current Test | Monitor current through the PS11 fuse path | Planned |
| Stage 4 | ESP32 Logging Test | Log conditioned signals and current data | Planned |
| Stage 5 | Flatline Detection Test | Test detection logic in logging-only mode | Planned |
| Stage 6 | Cutoff Simulation Test | Log when cutoff would have happened without cutting power | Future |
| Stage 7 | Active Cutoff Test | Test real cutoff on sacrificial hardware only | Future |
| Stage 8 | Multi-Console Validation | Compare results across models and board revisions | Future |
| Stage 9 | Beta Tester Validation | Controlled testing by trusted testers | Future |

---

## Important Safety Warning

Layzr Savre interacts with sensitive parts of the PS2 optical-drive system.

Incorrect wiring, incorrect probing, incorrect current monitoring, incorrect firmware, or incorrect cutoff behavior may damage the console.

Possible damage may include:

- Optical-drive failure
- Laser failure
- Driver IC damage
- Blown fuses
- Damaged PS11 pads
- Damaged traces
- Console lockups
- Failed reads
- Partial power states
- ESP32 damage
- Motherboard damage

Early testing should be performed on sacrificial or non-critical consoles.

---

## What Should Be Tested First

The first tests should be low-risk observation tests.

Early test priorities:

- Confirm normal console operation.
- Identify the board revision.
- Identify PS11.
- Identify the driver IC.
- Identify focus and tracking signal locations.
- Confirm safe ground reference points.
- Measure signals with an oscilloscope.
- Confirm passive monitoring does not affect operation.
- Record normal optical-drive behavior.
- Record failed-read behavior.

Do not begin with active cutoff.

---

## What Should Not Be Tested Yet

The following should not be tested until earlier stages are complete:

- Active coil or driver power cutoff.
- ESP32-controlled cutoff.
- Automatic protection triggering.
- Direct ESP32 connection to unknown PS2 signals.
- Pulling DSP signals high or low.
- Pulling Mechacon or Syscon signals high or low.
- Driving unknown optical-drive control lines.
- Bypassing PS11 fuse protection.
- Testing on valuable or customer consoles.
- Claiming protection behavior before validation.

---

## Required Test Documentation

Every test should document:

- Test date.
- Tester name.
- Test purpose.
- PS2 model.
- Motherboard revision.
- Region, if useful.
- Driver IC marking.
- DSP marking, if known.
- Laser model, if known.
- Optical-drive assembly, if known.
- Other mods installed.
- Layzr Savre hardware revision.
- Firmware revision, if used.
- Measurement method.
- Probe points.
- Ground reference.
- Disc type.
- Disc condition.
- Power supply used.
- Test duration.
- Observed behavior.
- Result.
- Follow-up actions.

A test without context may not be useful later.

---

## Recommended Test Equipment

Recommended equipment for development testing:

- Multimeter
- Oscilloscope
- Logic analyzer, only for confirmed logic-level signals
- Differential probe, if available
- Current shunt
- Current-sense amplifier test board, if used
- USB-to-serial adapter
- ESP32 programming adapter
- Fine soldering iron
- Flux
- Magnification
- Kapton tape or insulation
- Fine wire
- Known-good PS2 discs
- Known-bad or scratched test discs
- Sacrificial PS2 console
- Thermal camera or temperature probe, if available

Not every future installer will need all of this equipment, but development testing does.

---

## Test Console Selection

Early testing should use consoles that are not valuable.

Recommended first test console:

- Known working enough to read discs.
- Not a rare or valuable model.
- Easy to open and rework.
- Board revision is visible.
- Optical drive can be tested repeatedly.
- Failure would not be a major loss.

Avoid early testing on:

- Customer consoles.
- Rare consoles.
- Finished custom builds.
- Consoles with sentimental value.
- Consoles that already have unknown faults.
- Consoles with unstable power behavior.

---

## Baseline Console Test

Before installing any Layzr Savre hardware, confirm that the console works normally.

Baseline checklist:

- [ ] Console powers on.
- [ ] Browser appears.
- [ ] Controller input works.
- [ ] Optical drive moves normally.
- [ ] Known-good PS2 DVD reads.
- [ ] Known-good PS2 CD reads, if available.
- [ ] Known-good PS1 disc reads, if available.
- [ ] Audio CD reads, if useful.
- [ ] Drive does not make abnormal sounds.
- [ ] Driver IC does not become unusually hot.
- [ ] No fuses are open.
- [ ] Power supply is stable.

If the console does not work normally before modification, the test results may be difficult to trust.

---

## Board Documentation Test

Before electrical testing, document the board.

Board documentation checklist:

- [ ] PS2 model recorded.
- [ ] Motherboard revision recorded.
- [ ] Region recorded, if useful.
- [ ] Driver IC marking recorded.
- [ ] DSP marking recorded, if visible.
- [ ] PS11 location photographed.
- [ ] Optical-drive connector photographed.
- [ ] Laser model recorded, if known.
- [ ] Optical-drive assembly photographed.
- [ ] Existing mods documented.
- [ ] Fuse condition checked.
- [ ] Ground reference points identified.
- [ ] Photos saved in the project folder.

Photos are important because board-revision differences matter.

---

## Passive Signal Testing

Passive signal testing should be the first electrical testing stage.

The goal is to observe focus and tracking behavior without changing console operation.

Passive signal testing should measure:

- Focus coil activity.
- Tracking coil activity.
- Driver IC output behavior, if safe.
- Startup behavior.
- No-disc behavior.
- Disc-detection behavior.
- Normal read behavior.
- Failed-read behavior.

The monitoring circuit should be high impedance and should not load the PS2 signals.

---

## Passive Signal Test Checklist

Before passive signal testing:

- [ ] Console baseline test completed.
- [ ] Board revision documented.
- [ ] Signal point identified.
- [ ] Ground reference identified.
- [ ] Probe type selected.
- [ ] Oscilloscope settings prepared.
- [ ] Test disc selected.
- [ ] Wires secured.
- [ ] No short circuits found.
- [ ] Monitoring hardware does not interfere mechanically.
- [ ] Console powers on normally with monitoring hardware installed.

During testing:

- [ ] Capture startup behavior.
- [ ] Capture no-disc behavior.
- [ ] Capture disc-detection behavior.
- [ ] Capture known-good disc behavior.
- [ ] Capture failed-read behavior, if safe.
- [ ] Save scope screenshots.
- [ ] Save waveform files, if available.
- [ ] Record notes.

---

## PS11 Current Testing

PS11 current testing is used to measure current through the PS11 fuse path.

PS11 is a physical fuse that provides power to the driver IC in the area being studied.

The current plan is to lift one side of PS11 and use that fuse location as a current-monitoring point.

This test should be done carefully because PS11 is part of the power path.

---

## PS11 Current Test Checklist

Before PS11 current testing:

- [ ] Console baseline test completed.
- [ ] PS11 location confirmed.
- [ ] PS11 is confirmed as a physical fuse.
- [ ] PS11 fuse condition checked.
- [ ] Driver IC power path confirmed as much as possible.
- [ ] One side of PS11 selected for lifting.
- [ ] Shunt value selected.
- [ ] Shunt power rating confirmed.
- [ ] Current-sense wiring prepared.
- [ ] Fuse protection role considered.
- [ ] No bypass of fuse protection created.
- [ ] Voltage drop risk considered.
- [ ] Ground reference confirmed.
- [ ] Continuity checked before power.
- [ ] Shorts checked before power.

During testing:

- [ ] Power on with no disc.
- [ ] Confirm normal boot.
- [ ] Measure baseline PS11 current.
- [ ] Test known-good disc.
- [ ] Measure current during disc detection.
- [ ] Measure current during focus search.
- [ ] Measure current during normal read.
- [ ] Measure current during failed read, if safe.
- [ ] Watch for heat.
- [ ] Stop if abnormal behavior occurs.

---

## PS11 Current Data to Record

Each PS11 current test should record:

- PS2 model.
- Board revision.
- Driver IC marking.
- PS11 fuse location.
- Which side of PS11 was lifted.
- Shunt value.
- Shunt power rating.
- Measurement method.
- Voltage across shunt.
- Estimated current.
- Disc type.
- Disc condition.
- Console state.
- Driver IC temperature, if checked.
- Whether the console behaved normally.
- Whether voltage drop affected operation.

PS11 current should be treated as one data point, not as proof of a fault by itself.

---

## ESP32 Logging Testing

ESP32 testing should begin only after the monitored signals are properly conditioned.

The ESP32 should first be used for logging and diagnostics.

Early ESP32 testing should not control the PS2 hardware.

---

## ESP32 Logging Test Checklist

Before ESP32 testing:

- [ ] Firmware builds successfully.
- [ ] Serial output works.
- [ ] ESP32 power source is stable.
- [ ] GPIO pin assignments are documented.
- [ ] ADC inputs are protected.
- [ ] Input voltage range is confirmed.
- [ ] No direct connection to unknown PS2 signals.
- [ ] No GPIO can accidentally drive PS2 signals.
- [ ] Cutoff output is disabled.
- [ ] Active protection is disabled.
- [ ] ESP32 does not backfeed the PS2.
- [ ] ESP32 does not reset unexpectedly.
- [ ] Logging works on the bench before console testing.

During testing:

- [ ] Confirm ESP32 boots.
- [ ] Confirm firmware version prints.
- [ ] Confirm serial log starts.
- [ ] Confirm focus data logs, if connected.
- [ ] Confirm tracking data logs, if connected.
- [ ] Confirm PS11 current data logs, if connected.
- [ ] Confirm no false fault action occurs.
- [ ] Confirm console behavior is not affected.

---

## Flatline Detection Testing

Flatline detection should begin in logging-only mode.

The firmware may detect suspected faults, but it should not cut power during early testing.

The goal is to learn whether the detection logic can identify suspicious behavior without false triggering during normal operation.

---

## Flatline Detection Test Checklist

Before flatline detection testing:

- [ ] Passive monitoring data collected.
- [ ] PS11 current data collected.
- [ ] ESP32 logging is stable.
- [ ] Detection thresholds are documented.
- [ ] Startup ignore window is enabled.
- [ ] Disc-detection ignore window is enabled.
- [ ] Fault confirmation timer is enabled.
- [ ] Active cutoff is disabled.
- [ ] Cutoff simulation mode is used instead of real cutoff.
- [ ] Test conditions are documented.

During testing:

- [ ] Run no-disc test.
- [ ] Run known-good disc test.
- [ ] Run startup-only test.
- [ ] Run normal read test.
- [ ] Run read-retry test, if possible.
- [ ] Run failed-read test, if safe.
- [ ] Log suspected faults.
- [ ] Record false triggers.
- [ ] Record missed suspicious behavior.
- [ ] Adjust thresholds only after reviewing data.

---

## Cutoff Simulation Testing

Cutoff simulation testing means the firmware logs when it would have cut power, but the hardware does not actually cut power.

This is a critical step before real cutoff testing.

Cutoff simulation can help identify:

- False triggers.
- Bad thresholds.
- Timing problems.
- Startup detection problems.
- Read-retry detection problems.
- Board-revision differences.
- Bad assumptions about PS11 current.
- Bad assumptions about focus or tracking activity.

Simulation should be repeated many times before active cutoff is enabled.

---

## Active Cutoff Testing

Active cutoff testing should only happen after passive monitoring, PS11 current monitoring, ESP32 logging, flatline detection, and cutoff simulation have been tested.

Active cutoff should only be tested on sacrificial hardware.

Active cutoff testing must not be enabled by default.

---

## Active Cutoff Test Checklist

Before active cutoff testing:

- [ ] Sacrificial console selected.
- [ ] Console works before modification.
- [ ] Board revision documented.
- [ ] Cutoff point verified.
- [ ] Cutoff circuit installed.
- [ ] Cutoff disabled by default.
- [ ] Physical cutoff enable jumper confirmed.
- [ ] Manual override confirmed.
- [ ] Fault indicator confirmed.
- [ ] ESP32 firmware version documented.
- [ ] Detection thresholds documented.
- [ ] Cutoff simulation already tested.
- [ ] No false triggers during normal operation.
- [ ] Recovery plan documented.
- [ ] Emergency stop plan ready.

During active cutoff testing:

- [ ] Start with no disc.
- [ ] Confirm normal boot.
- [ ] Confirm cutoff does not trigger.
- [ ] Test known-good disc.
- [ ] Confirm cutoff does not false trigger.
- [ ] Trigger controlled fault condition only if safe.
- [ ] Confirm cutoff activates when expected.
- [ ] Measure current before cutoff.
- [ ] Measure current after cutoff.
- [ ] Measure voltage before cutoff.
- [ ] Measure voltage after cutoff.
- [ ] Check driver IC temperature.
- [ ] Check recovery behavior.
- [ ] Save logs and notes.

---

## Test Conditions

Layzr Savre should be tested under many optical-drive conditions.

| Test Condition | Purpose |
|---|---|
| No disc | Establish baseline idle behavior |
| Startup only | Capture power-on and boot behavior |
| Browser idle | Observe low-activity normal state |
| Known-good PS2 DVD | Capture normal PS2 DVD behavior |
| Known-good PS2 CD | Capture normal PS2 CD behavior |
| Known-good PS1 disc | Capture PS1 optical-drive behavior |
| Audio CD | Capture audio CD behavior |
| DVD video | Capture DVD video behavior |
| Dirty disc | Observe difficult-read behavior |
| Scratched disc | Observe read retries and failure behavior |
| Weak laser | Compare weak optical pickup behavior |
| Failed read | Capture abnormal optical-drive behavior |
| Repeated retries | Watch for sustained abnormal activity |
| Suspected flatline | Study possible stuck or missing activity |
| Cutoff simulation | Test detection without hardware cutoff |
| Active cutoff | Test real protection behavior only after validation |

---

## Disc Test Set

A useful test set may include:

- Known-good PS2 DVD game.
- Known-good PS2 CD game.
- Known-good PS1 game.
- Audio CD.
- DVD video.
- Lightly scratched disc.
- Dirty disc.
- Disc known to fail on weak lasers.
- Disc that causes read retries.
- No disc.

Do not use valuable or rare discs during risky testing.

---

## Signal Data to Capture

Signal data should include:

- Focus activity.
- Tracking activity.
- PS11 current.
- Driver IC voltage, if useful.
- Startup timing.
- Disc-detection timing.
- Read-retry timing.
- Fault timing.
- Suspected flatline timing.
- ESP32 detection state.
- Cutoff simulation state.
- Cutoff active state, in future testing.

---

## Test Result Categories

Each test result should be marked with a simple category.

| Result | Meaning |
|---|---|
| Pass | Test behaved as expected |
| Fail | Test did not behave as expected |
| Inconclusive | Data was not clear enough |
| Needs Repeat | Test should be repeated |
| Unsafe | Test showed a safety concern |
| Useful Data | Data is useful for future comparison |
| False Trigger | Detection triggered during normal behavior |
| Missed Fault | Suspicious behavior occurred but detection did not catch it |

These categories make it easier to review progress later.

---

## Test Data Quality Levels

Test data should be classified by quality.

| Quality Level | Meaning |
|---|---|
| Raw Unreviewed | Data saved but not reviewed |
| Reviewed | Data checked for basic accuracy |
| Useful | Data has enough context to compare |
| Reference | High-quality data suitable for future thresholds |
| Questionable | Data may be affected by test setup |
| Invalid | Data should not be used for conclusions |

Do not build protection thresholds from questionable data.

---

## Test Report Folder

Test reports should be stored in:

    Test-Data/Test-Reports/

Suggested folder structure:

    Test-Data/
    ├── Raw-Logs/
    ├── Processed-Logs/
    ├── Scope-Captures/
    ├── Current-Measurements/
    ├── Voltage-Measurements/
    ├── ESP32-Logs/
    ├── Photos/
    ├── Notes/
    └── Test-Reports/

---

## Test Report Naming

Suggested test report file name format:

    YYYY-MM-DD-PS2MODEL-BOARD-CONDITION.md

Examples:

    2026-05-13-SCPH75001-GH040-good_ps2_dvd.md
    2026-05-13-SCPH75001-GH040-ps11_current.md
    2026-05-13-SCPH79001-GH061-failed_read.md
    2026-05-13-SCPH79001-GH061-cutoff_simulation.md

---

## Test Session Report Template

Use this template for a full test session.

## Test Session Report

### Basic Information

- Date:
- Tester:
- Test purpose:
- Test stage:
- Result category:
- Notes:

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
- PS11 current monitoring installed:
- Current-sense value:
- Signal-conditioning method:
- Cutoff hardware installed:
- Cutoff enabled:

### Firmware

- Firmware name:
- Firmware version:
- Build date:
- Logging mode:
- Detection mode:
- Cutoff simulation enabled:
- Active cutoff enabled:

### Measurement Setup

- Tools used:
- Probe points:
- Ground reference:
- Scope settings:
- Current measurement method:
- Voltage measurement method:
- ESP32 log method:

### Test Condition

- Disc type:
- Disc condition:
- Console state:
- Power supply:
- Test duration:

### Files Collected

- Raw log:
- Processed log:
- Scope captures:
- Current measurements:
- Voltage measurements:
- ESP32 logs:
- Photos:
- Notes:

### Observed Behavior

- Console booted normally:
- Disc detected:
- Disc read normally:
- Read retries observed:
- Failed read observed:
- Suspected flatline observed:
- False trigger observed:
- Cutoff simulated:
- Cutoff activated:
- Any abnormal heat:
- Any abnormal sound:
- Any instability:

### Measurements

- Focus behavior:
- Tracking behavior:
- PS11 current:
- Driver IC voltage:
- Driver IC temperature:
- ESP32 voltage:
- Fault timing:
- Recovery behavior:

### Conclusion

- Test passed:
- Test failed:
- Data useful:
- Safety concern:
- Follow-up needed:
- Recommended next step:

---

## Baseline Test Template

Use this for testing a console before modification.

## Baseline Console Test

### Console Information

- PS2 model:
- Board revision:
- Region:
- Driver IC marking:
- Laser model:
- Optical-drive assembly:
- Other mods installed:

### Power-On Test

- Console powers on:
- Browser appears:
- No unusual sounds:
- No unusual heat:
- Power supply used:

### Disc Tests

- Known-good PS2 DVD reads:
- Known-good PS2 CD reads:
- Known-good PS1 disc reads:
- Audio CD reads:
- DVD video reads:
- Notes:

### Result

- Console suitable for testing:
- Issues found:
- Follow-up needed:

---

## Passive Signal Test Template

Use this for focus and tracking signal tests.

## Passive Signal Test

### Console Information

- PS2 model:
- Board revision:
- Driver IC marking:
- Laser model:

### Signal Information

- Signal measured:
- Temporary signal name:
- Measurement point:
- Probe type:
- Ground reference:
- Scope settings:

### Test Condition

- Disc type:
- Disc condition:
- Console state:
- Test duration:

### Observed Behavior

- Startup behavior:
- No-disc behavior:
- Disc-detection behavior:
- Normal-read behavior:
- Failed-read behavior:
- Signal appeared sensitive:
- Probing affected operation:

### Files

- Scope screenshot:
- Waveform export:
- Photos:
- Notes:

### Conclusion

- Signal useful:
- Safe to monitor:
- Needs buffering:
- Needs follow-up:

---

## PS11 Current Test Template

Use this for PS11 current tests.

## PS11 Current Test

### Console Information

- PS2 model:
- Board revision:
- Driver IC marking:
- Laser model:
- Optical-drive assembly:

### PS11 Setup

- PS11 location confirmed:
- PS11 side lifted:
- Shunt value:
- Shunt power rating:
- Measurement method:
- Sense amplifier used:
- Ground reference:

### Test Condition

- Disc type:
- Disc condition:
- Console state:
- Power supply:
- Test duration:

### Measurements

- Shunt voltage at startup:
- Estimated current at startup:
- Shunt voltage during no-disc state:
- Estimated current during no-disc state:
- Shunt voltage during disc detection:
- Estimated current during disc detection:
- Shunt voltage during normal read:
- Estimated current during normal read:
- Shunt voltage during failed read:
- Estimated current during failed read:
- Peak current:
- Driver IC temperature:

### Observed Behavior

- Console booted normally:
- Disc detected:
- Disc read normally:
- Measurement affected operation:
- Abnormal heat:
- Abnormal sound:
- Instability:

### Conclusion

- Shunt value acceptable:
- Current data useful:
- Voltage drop acceptable:
- Follow-up needed:

---

## ESP32 Logging Test Template

Use this for ESP32 logging tests.

## ESP32 Logging Test

### Console Information

- PS2 model:
- Board revision:
- Driver IC marking:
- Laser model:

### ESP32 Setup

- ESP32 module:
- Firmware version:
- Power source:
- Ground reference:
- Serial output working:
- Web interface enabled:
- Cutoff disabled:

### Inputs Connected

- Focus input:
- Tracking input:
- PS11 current input:
- Driver voltage input:
- Other inputs:

### Test Condition

- Disc type:
- Disc condition:
- Console state:
- Test duration:

### Observed Behavior

- ESP32 booted normally:
- Logs started:
- Focus data logged:
- Tracking data logged:
- PS11 current logged:
- Fault events logged:
- False triggers:
- Console behavior affected:

### Conclusion

- Logging stable:
- Input readings useful:
- More filtering needed:
- Follow-up needed:

---

## Flatline Detection Test Template

Use this for logging-only detection testing.

## Flatline Detection Test

### Console Information

- PS2 model:
- Board revision:
- Driver IC marking:
- Laser model:

### Detection Setup

- Firmware version:
- Detection mode:
- Active cutoff enabled:
- Cutoff simulation enabled:
- Startup ignore time:
- Disc-detection ignore time:
- Fault confirmation time:
- Current threshold:
- Activity threshold:

### Test Condition

- Disc type:
- Disc condition:
- Console state:
- Test duration:

### Observed Behavior

- Focus activity:
- Tracking activity:
- PS11 current:
- Suspected fault detected:
- Confirmed fault detected:
- Cutoff simulated:
- False trigger:
- Missed suspicious behavior:
- Console recovered:

### Conclusion

- Detection useful:
- Detection too sensitive:
- Detection too slow:
- Threshold change needed:
- Follow-up needed:

---

## Active Cutoff Test Template

Use this only after active cutoff testing is approved for sacrificial hardware.

## Active Cutoff Test

### Console Information

- PS2 model:
- Board revision:
- Driver IC marking:
- Laser model:

### Cutoff Setup

- Hardware revision:
- Firmware revision:
- Cutoff point:
- Cutoff method:
- Cutoff enable jumper installed:
- Manual override available:
- Fault indicator working:

### Detection Settings

- Startup ignore time:
- Disc-detection ignore time:
- Fault confirmation time:
- Current threshold:
- Activity threshold:
- Fault latch enabled:

### Test Condition

- Disc type:
- Disc condition:
- Fault condition:
- Test duration:

### Measurements

- PS11 current before cutoff:
- PS11 current after cutoff:
- Driver voltage before cutoff:
- Driver voltage after cutoff:
- Driver IC temperature:
- Cutoff switch temperature:

### Observed Behavior

- Fault detected:
- Cutoff activated:
- Console froze:
- Console recovered:
- False trigger:
- Abnormal heat:
- Abnormal sound:
- Damage observed:

### Conclusion

- Cutoff method safe:
- Cutoff method unsafe:
- Recovery acceptable:
- More testing needed:
- Do not repeat until revised:

---

## Stop Testing Conditions

Stop testing immediately if any of the following occur:

- Burning smell.
- Smoke.
- PS11 area becomes hot.
- Shunt becomes hot.
- Driver IC becomes unusually hot.
- ESP32 becomes unusually hot.
- Console will not power on.
- Console resets repeatedly.
- Console locks up.
- Optical drive makes abnormal sounds.
- Disc does not spin normally.
- Laser behavior appears abnormal.
- Current is much higher than expected.
- Voltage drop is excessive.
- Cutoff triggers repeatedly without cause.
- Cutoff chatters or cycles.
- Signal wire disconnects.
- A short is suspected.

Do not continue until the issue is understood.

---

## False Trigger Testing

False trigger testing is required before active cutoff.

A false trigger happens when detection says a fault occurred during normal behavior.

False trigger tests should include:

- Startup.
- No disc.
- Browser idle.
- Known-good PS2 DVD.
- Known-good PS2 CD.
- Known-good PS1 disc.
- Audio CD.
- DVD video.
- Normal game loading.
- Read retries from a scratched disc.
- Multiple power cycles.

Any false trigger should be logged and investigated.

---

## Repeatability Testing

A single successful test is not enough.

Important tests should be repeated.

Repeatability should check:

- Same console, same disc, same result.
- Same console, different disc, similar result.
- Same board revision, different console.
- Different board revision, same test condition.
- Same firmware, repeated sessions.
- Same hardware, long-duration run.

Repeatable behavior is more useful than one-time behavior.

---

## Long-Duration Testing

Long-duration testing should be done before beta release.

Possible long-duration tests:

- 30-minute known-good disc read.
- 1-hour game session.
- Multiple boot cycles.
- Multiple disc changes.
- Repeated failed-read attempts, if safe.
- ESP32 logging for extended time.
- Web interface left running.
- Current monitoring over time.
- Temperature monitoring over time.

Long-duration tests help find heat, stability, and false trigger issues.

---

## Multi-Console Testing

Layzr Savre should eventually be tested across multiple PS2 models and board revisions.

Useful comparison points:

- PS2 model.
- Motherboard revision.
- Driver IC type.
- DSP type.
- Laser model.
- Optical-drive assembly.
- PS11 location and behavior.
- Focus activity.
- Tracking activity.
- PS11 current range.
- Detection threshold differences.
- False trigger differences.
- Cutoff behavior, if tested.

Do not assume one console represents all PS2 consoles.

---

## Compatibility Tracking

Compatibility should be documented only after testing.

Compatibility categories:

| Category | Meaning |
|---|---|
| Untested | No test data yet |
| Research Only | Signal or current data collected only |
| Passive Monitor Compatible | Passive monitoring works without affecting operation |
| Logging Compatible | ESP32 logging works |
| Detection Testing | Detection logic is being tested |
| Cutoff Testing | Active cutoff tested on sacrificial hardware |
| Beta Supported | Approved for trusted tester use |
| Unsupported | Known issue or unsafe behavior found |

A board should not be marked supported without test data.

---

## Release Testing Requirements

Before any public kit release, the project should have:

- Stable hardware revision.
- Stable firmware revision.
- Confirmed passive monitoring behavior.
- Confirmed PS11 current monitoring behavior.
- Confirmed ESP32 logging behavior.
- Detection tested in logging-only mode.
- False trigger testing completed.
- Cutoff tested only if included in the kit.
- Recovery behavior documented.
- Supported model list.
- Unsupported model list.
- Installation guide.
- First-power-on checklist.
- Troubleshooting guide.
- Safety warnings.
- Known limitations.

---

## Open Questions

Current open testing questions:

- Which PS2 board revision should be tested first?
- What is the safest first signal to monitor?
- What is the safest shunt value for PS11 current testing?
- What voltage drop at PS11 is acceptable?
- What sampling rate is needed for PS11 current?
- What signal conditioning is needed for focus activity?
- What signal conditioning is needed for tracking activity?
- Can the ESP32 log useful activity data reliably?
- What does normal flatline-like behavior look like?
- How long should detection ignore startup behavior?
- How long should detection ignore disc-detection behavior?
- What false trigger conditions are most likely?
- What cutoff point is safest, if any?
- What recovery method is safest after cutoff?

---

## Current Working Theory

The current testing theory is:

- Passive monitoring should happen before active control.
- PS11 current should be measured carefully as one data point.
- Focus and tracking activity should be compared with PS11 current.
- ESP32 logging should begin with serial output.
- Flatline detection should begin in logging-only mode.
- Cutoff simulation should happen before real cutoff.
- Active cutoff should only be tested on sacrificial hardware.
- Board-revision differences must be documented.
- A kit should only be released after repeatable test results exist.

This theory will be updated as testing produces real data.

---

## Development Rule

For Layzr Savre testing, the rule is:

Baseline first.  
Monitor second.  
Measure third.  
Log fourth.  
Detect fifth.  
Simulate cutoff sixth.  
Cut power last.

---

## Summary

Testing is the foundation of the Layzr Savre project.

The project should not make protection claims until the PS2 optical-drive signals, PS11 current behavior, ESP32 logging, flatline detection, false trigger behavior, and future cutoff method have been tested carefully.

The first tests should focus on passive monitoring and data collection.

Active cutoff should only be tested later, only on sacrificial hardware, and only after detection behavior has been validated in logging-only mode.

The long-term goal is to create a tested, documented, and honest preservation kit for the PS2 community.
