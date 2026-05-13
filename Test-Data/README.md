# Test Data

**Project:** PS2 Layzr Savre  
**Owner:** FatBaldDad  
**Status:** Early research / planning / prototype development  
**Folder:** Test-Data  

---

## Overview

This folder is for storing test data collected during PS2 Layzr Savre development.

The purpose of this folder is to organize raw logs, processed logs, oscilloscope captures, current measurements, voltage measurements, ESP32 logs, photos, notes, and test reports related to the PS2 optical-drive system.

Layzr Savre depends on real test data.

Before the project can make reliable decisions about flatline detection, PS11 current monitoring, ESP32 logging, or future cutoff behavior, the project needs repeatable measurements from real PS2 consoles.

---

## Purpose of This Folder

This folder is intended to store and organize data from:

- Passive signal monitoring.
- Focus activity testing.
- Tracking activity testing.
- PS11 current monitoring.
- Driver IC voltage testing.
- ESP32 logging.
- Flatline detection research.
- Cutoff simulation testing.
- Future active cutoff testing.
- Board-revision comparisons.
- Optical-drive failure research.
- Compatibility testing.

This folder should help turn bench tests into useful project documentation.

---

## Important Notice

Test data should be treated carefully.

A single test does not prove universal behavior.

A single console does not represent every PS2 model.

A single failed read does not prove a dangerous condition.

A single current spike does not prove a fault.

Data should be reviewed, compared, repeated, and documented before conclusions are made.

---

## Recommended Folder Structure

Current planned folder structure:

    Test-Data/
    ├── README.md
    ├── Raw-Logs/
    ├── Processed-Logs/
    ├── Scope-Captures/
    ├── Current-Measurements/
    ├── Voltage-Measurements/
    ├── ESP32-Logs/
    ├── Photos/
    ├── Notes/
    └── Test-Reports/

The initial repo may only include some of these folders. More folders can be added as testing expands.

---

## Raw Logs

The `Raw-Logs/` folder is for original unmodified data.

Examples of raw logs:

- Raw ESP32 serial logs.
- Raw CSV output.
- Raw JSON output.
- Raw oscilloscope waveform exports.
- Raw logic analyzer captures.
- Raw current measurement data.
- Raw voltage measurement data.
- Unedited test notes.

Raw logs should be preserved when practical.

Do not overwrite raw logs.

---

## Processed Logs

The `Processed-Logs/` folder is for cleaned, converted, summarized, or reviewed data.

Examples of processed logs:

- Cleaned CSV files.
- Trimmed logs.
- Annotated logs.
- Converted waveform data.
- Summary tables.
- Graph-ready data.
- Fault event summaries.
- Comparison notes.

Processed logs should reference the raw log they came from whenever possible.

---

## Scope Captures

The `Scope-Captures/` folder is for oscilloscope screenshots and waveform captures.

Useful scope captures may include:

- Focus coil activity.
- Tracking coil activity.
- PS11 current-sense voltage.
- Driver IC supply voltage.
- Startup behavior.
- No-disc behavior.
- Disc-detection behavior.
- Normal read behavior.
- Failed-read behavior.
- Suspected flatline behavior.
- Cutoff simulation behavior.
- Future active cutoff behavior.

Scope captures should include enough notes to understand what was measured.

---

## Current Measurements

The `Current-Measurements/` folder is for current-related test data.

For Layzr Savre, the main planned current measurement is through the PS11 fuse path.

Important PS11 notes:

- PS11 is a physical fuse on the PS2 motherboard.
- PS11 provides power to the driver IC in the area being studied.
- The current plan is to lift one side of PS11 and use that fuse location as a current-monitoring point.
- PS11 current is one data point only.
- PS11 current alone should not be treated as proof of a fault.

Current measurement files may include:

- Shunt voltage readings.
- Estimated current values.
- Current over time.
- Current during startup.
- Current during no-disc state.
- Current during disc detection.
- Current during focus search.
- Current during normal read.
- Current during failed read.
- Current during suspected flatline behavior.

---

## Voltage Measurements

The `Voltage-Measurements/` folder may be added for voltage-related test data.

Useful voltage measurements may include:

- Driver IC supply voltage.
- Voltage before and after PS11 current-sense path.
- ESP32 supply voltage.
- Current-sense amplifier supply voltage.
- Reference voltages.
- Related optical-drive voltage rails.
- Voltage behavior during startup.
- Voltage behavior during failed reads.
- Voltage sag during high current events.

Voltage measurements should include the measurement point and ground reference.

---

## ESP32 Logs

The `ESP32-Logs/` folder may be added for logs created by Layzr Savre firmware.

Possible ESP32 logs:

- Serial debug logs.
- CSV logs.
- JSON logs.
- Event logs.
- Fault logs.
- Cutoff simulation logs.
- Current logs.
- Activity logs.
- Board profile logs.
- Firmware boot logs.

ESP32 logs should include firmware version and hardware revision when possible.

---

## Photos

The `Photos/` folder may be added for photos related to testing.

Useful photos include:

- PS2 motherboard revision.
- PS11 fuse location.
- Driver IC marking.
- DSP marking.
- Laser model.
- Optical-drive assembly.
- Interposer installation.
- Current-sense wiring.
- Scope probe location.
- Ground reference location.
- ESP32 wiring.
- Mechanical fitment.
- Damage or repair areas.
- Test setup.

Photos should be named clearly and linked to the test they belong to.

---

## Notes

The `Notes/` folder may be added for quick test notes, observations, and rough findings.

Useful notes include:

- Test observations.
- Problems found.
- Measurement concerns.
- Possible false triggers.
- Board-revision differences.
- Ideas for follow-up tests.
- Setup reminders.
- Signal naming notes.
- Known issues.

Rough notes are acceptable, but important findings should eventually be cleaned up into a test report.

---

## Test Reports

The `Test-Reports/` folder may be added for full Markdown test reports.

A test report should summarize:

- Test purpose.
- Console information.
- Hardware setup.
- Firmware setup.
- Measurement setup.
- Disc condition.
- Test result.
- Files collected.
- Observed behavior.
- Conclusion.
- Follow-up actions.

Test reports are useful because they connect raw data to real testing context.

---

## Why Context Matters

A file without context may not be useful later.

Every useful test should try to include:

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

The more context included, the more useful the data becomes.

---

## Suggested File Naming Format

Use simple, searchable file names.

Suggested format:

    YYYY-MM-DD-PS2MODEL-BOARD-SIGNAL-CONDITION

Examples:

    2026-05-13-SCPH75001-GH040-FOCUS-good_ps2_dvd
    2026-05-13-SCPH75001-GH040-TRACK-failed_read
    2026-05-13-SCPH75001-GH040-PS11-current-no_disc
    2026-05-13-SCPH79001-GH061-PS11-current-good_ps2_dvd
    2026-05-13-SCPH79001-GH061-FOCUS-weak_laser-failed_read

Add the correct file extension based on the file type.

---

## Suggested File Extensions

| Data Type | Suggested Extension |
|---|---|
| Plain text log | .txt |
| Markdown notes or report | .md |
| CSV data | .csv |
| JSON data | .json |
| Scope screenshot | .png |
| Photo | .jpg or .png |
| Waveform export | .csv or tool-specific format |
| Logic analyzer capture | Tool-specific format |

Markdown is preferred for reports because it displays clearly on GitHub.

---

## Date Format

Use this date format:

    YYYY-MM-DD

Example:

    2026-05-13

This keeps files sorted correctly.

---

## Signal Naming

Suggested signal names:

| Signal | Suggested Name |
|---|---|
| Focus activity | FOCUS |
| Focus coil side A | FOCUS_A |
| Focus coil side B | FOCUS_B |
| Tracking activity | TRACK |
| Tracking coil side A | TRACK_A |
| Tracking coil side B | TRACK_B |
| PS11 current | PS11_CURRENT |
| PS11 shunt voltage | PS11_SHUNT |
| Driver IC voltage | DRIVER_VCC |
| ESP32 supply voltage | ESP32_VCC |
| Fault state | FAULT_STATE |
| Cutoff simulation | CUTOFF_SIM |
| Active cutoff | CUTOFF_ACTIVE |

Temporary names should be marked as temporary until confirmed.

---

## Test Condition Naming

Suggested condition names:

| Condition | Suggested Name |
|---|---|
| No disc | no_disc |
| Startup only | startup |
| Browser idle | browser_idle |
| Known-good PS2 DVD | good_ps2_dvd |
| Known-good PS2 CD | good_ps2_cd |
| Known-good PS1 disc | good_ps1_cd |
| Audio CD | audio_cd |
| DVD video | dvd_video |
| Dirty disc | dirty_disc |
| Scratched disc | scratched_disc |
| Weak laser | weak_laser |
| Failed read | failed_read |
| Read retry | read_retry |
| Suspected flatline | suspected_flatline |
| Cutoff simulation | cutoff_simulation |
| Active cutoff test | active_cutoff_test |

Use consistent names so data can be searched later.

---

## Data Quality Levels

Test data can be classified by quality.

| Quality Level | Meaning |
|---|---|
| Raw Unreviewed | Data saved but not reviewed |
| Reviewed | Data checked for basic correctness |
| Useful | Data has enough context to compare |
| Reference | High-quality data suitable for future thresholds |
| Questionable | Data may be affected by test setup |
| Invalid | Data should not be used for conclusions |

Do not build detection thresholds from questionable or invalid data.

---

## Test Result Categories

Test results should be marked clearly.

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

Failed tests should still be documented.

---

## Recommended Test Order

Recommended test data collection order:

1. Baseline console test.
2. Board documentation.
3. Passive focus signal capture.
4. Passive tracking signal capture.
5. PS11 current measurement.
6. ESP32 bench logging.
7. ESP32 console logging.
8. Logging-only flatline detection.
9. Cutoff simulation.
10. Active cutoff testing only on sacrificial hardware.

Do not start with active cutoff testing.

---

## Baseline Console Data

Before installing Layzr Savre hardware, collect baseline data.

Baseline data should include:

- Console powers on.
- Browser appears.
- Known-good PS2 DVD reads.
- Known-good PS2 CD reads, if available.
- Known-good PS1 disc reads, if available.
- Drive sounds normal.
- No abnormal heat.
- Power supply used.
- Existing problems noted.

Baseline data helps prove whether Layzr Savre changed the behavior.

---

## Board Documentation Data

Board documentation should include:

- PS2 model.
- Motherboard revision.
- Region, if useful.
- Driver IC marking.
- DSP marking, if visible.
- PS11 fuse location.
- Laser model, if known.
- Optical-drive assembly.
- Existing mods.
- Photos of relevant areas.

Board documentation is required because PS2 revisions may behave differently.

---

## Focus Data

Focus data should document focusing coil or focus activity behavior.

Useful focus test states:

- Startup.
- No disc.
- Disc detection.
- Focus search.
- Known-good disc read.
- Failed read.
- Weak laser.
- Dirty disc.
- Scratched disc.
- Suspected flatline.

Focus data may help identify normal and abnormal behavior.

---

## Tracking Data

Tracking data should document tracking coil or tracking activity behavior.

Useful tracking test states:

- Startup.
- No disc.
- Disc detection.
- Seeking.
- Normal read.
- Read retry.
- Failed read.
- Weak laser.
- Dirty disc.
- Scratched disc.
- Suspected flatline.

Tracking data may help identify normal and abnormal behavior.

---

## PS11 Current Data

PS11 current data should document current through the PS11 fuse path.

Useful PS11 current test states:

- Startup.
- No disc.
- Browser idle.
- Disc detection.
- Focus search.
- Normal PS2 DVD read.
- Normal PS2 CD read.
- Normal PS1 disc read.
- Audio CD read.
- DVD video read.
- Read retry.
- Failed read.
- Weak laser.
- Dirty disc.
- Scratched disc.
- Suspected flatline.

PS11 current should be compared against focus and tracking activity.

---

## ESP32 Log Data

ESP32 logs may include:

- Firmware name.
- Firmware version.
- Hardware revision.
- Board profile.
- Operating mode.
- Active cutoff status.
- Focus activity.
- Tracking activity.
- PS11 current.
- Voltage readings.
- Fault state.
- Event type.
- Timestamp.
- Notes.

ESP32 logs should clearly show whether firmware is in logging-only mode, cutoff simulation mode, or active cutoff mode.

---

## Flatline Detection Data

Flatline detection data should be collected in logging-only mode first.

Useful data includes:

- Suspected fault time.
- Suspected fault duration.
- Focus activity state.
- Tracking activity state.
- PS11 current.
- Voltage behavior, if measured.
- Detection threshold.
- Startup ignore time.
- Fault confirmation time.
- Whether the event was a false trigger.
- Whether the console behaved normally.

Flatline detection should not control hardware until validated.

---

## Cutoff Simulation Data

Cutoff simulation data records when firmware would have cut power, without actually cutting power.

Useful data includes:

- Time cutoff would have happened.
- Reason for simulated cutoff.
- Focus activity at the time.
- Tracking activity at the time.
- PS11 current at the time.
- Detection state.
- Firmware mode.
- Whether the event was valid or false.
- Console behavior.

Cutoff simulation should happen before active cutoff testing.

---

## Active Cutoff Data

Active cutoff data should only be collected on sacrificial hardware after earlier testing is complete.

Useful data includes:

- Cutoff point.
- Cutoff method.
- Hardware revision.
- Firmware revision.
- Detection settings.
- PS11 current before cutoff.
- PS11 current after cutoff.
- Driver IC voltage before cutoff.
- Driver IC voltage after cutoff.
- Console behavior.
- Recovery behavior.
- Heat.
- Any damage or instability.

Active cutoff data must be documented carefully.

---

## Test Report Template

Use this template for a full test report.

## Test Report

### Basic Information

- Date:
- Tester:
- Test purpose:
- Test stage:
- Result category:
- Data quality:
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

## PS11 Current Test Template

Use this template for PS11 current-specific data.

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

## Scope Capture Template

Use this template for scope capture notes.

## Scope Capture

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
- Scope channel:
- Voltage scale:
- Time scale:

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
- Suspected flatline behavior:
- Signal appeared sensitive:
- Probing affected operation:

### Files

- Scope screenshot:
- Waveform export:
- Related ESP32 log:
- Related current log:
- Photos:

### Conclusion

- Signal useful:
- Safe to monitor:
- Needs buffering:
- Useful for detection:
- Follow-up needed:

---

## ESP32 Log Template

Use this template for ESP32 log notes.

## ESP32 Log Entry

### Console Information

- PS2 model:
- Board revision:
- Driver IC marking:
- Laser model:

### ESP32 Setup

- ESP32 module:
- Firmware name:
- Firmware version:
- Hardware revision:
- Power source:
- Ground reference:
- Logging mode:
- Active cutoff status:

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

### Files

- Serial log:
- CSV log:
- JSON log:
- Photos:
- Notes:

### Conclusion

- Logging stable:
- Input readings useful:
- More filtering needed:
- Follow-up needed:

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
- Unknown unrelated firmware.
- Personal information from beta testers.
- Customer information.
- Anything that cannot be redistributed.

This folder should contain Layzr Savre test data only.

---

## Large File Notes

Some test data may be too large for normal GitHub use.

Large files may include:

- Long waveform captures.
- Large logic analyzer sessions.
- Long-duration raw logs.
- High-resolution photo sets.
- Video captures.

Possible handling options:

- Store summaries in the repo.
- Store important screenshots instead of huge raw files.
- Compress large files.
- Use GitHub Releases for release-related test packages.
- Use Git LFS only if the project chooses to support it.
- Keep local backups of large raw captures.

Avoid filling the repo with huge files unless they are important.

---

## Data Review Process

Suggested data review process:

1. Confirm the file name is clear.
2. Confirm the test context is included.
3. Confirm the console information is included.
4. Confirm the hardware revision is included.
5. Confirm the firmware version is included, if used.
6. Confirm the measurement method is documented.
7. Confirm the raw data was saved, if possible.
8. Review whether the console behaved normally.
9. Review focus activity.
10. Review tracking activity.
11. Review PS11 current.
12. Review voltage data, if available.
13. Mark data quality.
14. Mark result category.
15. Add follow-up notes.

---

## Relationship to Documentation

Important findings from test data should be added to the documentation.

Possible documents to update:

- `Documentation/03-Signal-Research.md`
- `Documentation/04-Flatline-Detection-Theory.md`
- `Documentation/05-PS11-Current-Monitoring.md`
- `Documentation/06-Coil-Power-Cutoff-Method.md`
- `Documentation/08-Data-Logging.md`
- `Documentation/09-Testing-Plan.md`
- `PROJECT_STATUS.md`
- `CHANGELOG.md`

Test data should support documentation updates.

---

## Relationship to Firmware

Test data should guide firmware development.

Useful firmware decisions based on test data:

- ADC scaling.
- Sampling rate.
- Current thresholds.
- Activity thresholds.
- Startup ignore time.
- Disc-detection ignore time.
- Fault confirmation time.
- False trigger filtering.
- Board profiles.
- Logging format.
- Cutoff simulation behavior.

Firmware thresholds should not be guessed.

---

## Relationship to Hardware

Test data should guide hardware development.

Useful hardware decisions based on test data:

- Signal-conditioning method.
- Current-sense value.
- Current-sense amplifier choice.
- ESP32 input protection.
- Test pad placement.
- Interposer routing.
- Cutoff circuit location, if used later.
- Fuse protection method.
- Mechanical mounting.
- Board-revision-specific design changes.

Hardware decisions should be based on measured behavior.

---

## Current Working Theory

The current working theory is:

- Test data is the foundation of the project.
- Raw logs should be preserved when practical.
- Processed logs should reference raw logs.
- PS11 current is one useful measurement point, not the whole system.
- Focus and tracking activity should be compared with PS11 current.
- Board revision matters.
- False triggers are important and should be documented.
- Active cutoff should not be tested until enough data exists.
- Detection thresholds should come from reviewed data.
- Good test reports are as important as good hardware.

This theory will be updated as data is collected.

---

## Summary

The `Test-Data/` folder is where Layzr Savre development becomes measurable.

This folder should collect the raw evidence needed to understand PS2 optical-drive behavior, PS11 current, focus activity, tracking activity, ESP32 logging, flatline detection, and future cutoff behavior.

Good data will help the project move from theory to tested hardware.

Poorly documented data should not be used for major design decisions.

The goal is to build a useful, honest, and repeatable test record for the PS2 community.
