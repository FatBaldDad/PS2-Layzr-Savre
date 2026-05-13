# Data Logging

**Project:** PS2 Layzr Savre  
**Owner:** FatBaldDad  
**Status:** Early research / planning / prototype development  
**Document:** 08 - Data Logging  

---

## Overview

Data logging is one of the most important parts of the PS2 Layzr Savre project.

Before Layzr Savre can become a protection system, it first needs to become a good measurement and documentation system.

The goal of data logging is to record PS2 optical-drive behavior during normal and abnormal conditions. This data can then be used to understand focus activity, tracking activity, PS11 current behavior, voltage behavior, failed reads, possible flatline events, and future protection decisions.

At this stage, data logging is for research only.

---

## Purpose of This Document

This document explains how Layzr Savre should collect and organize test data.

It is intended to document:

- What data should be logged.
- Why test context matters.
- How logs should be organized.
- How raw data and processed data should be separated.
- What file names should look like.
- What information should be included with each test.
- How ESP32 logs may be used.
- How oscilloscope and current measurements should be stored.
- How data may support future flatline detection.
- How data may support future kit development.

This document should be updated as the logging process improves.

---

## Why Data Logging Matters

The PS2 optical-drive system is complex.

Without logs, it is easy to make assumptions based on one test, one console, one disc, or one failure.

Data logging helps the project:

- Compare normal and abnormal behavior.
- Compare different PS2 board revisions.
- Compare good and weak lasers.
- Compare good and damaged discs.
- Compare CD and DVD behavior.
- Compare PS1 and PS2 disc behavior.
- Identify possible flatline conditions.
- Identify current behavior through PS11.
- Identify false-trigger risks.
- Build detection thresholds from real measurements.
- Document what was actually tested.
- Support future troubleshooting and kit documentation.

Good logs turn experiments into useful project knowledge.

---

## Data Logging Goals

The main goals of data logging are:

- Record normal optical-drive behavior.
- Record failed-read behavior.
- Record focus activity.
- Record tracking activity.
- Record PS11 current behavior.
- Record voltage behavior where useful.
- Record driver IC behavior where useful.
- Record timing of important events.
- Record suspected fault conditions.
- Record false trigger conditions.
- Record recovery behavior.
- Record board-revision differences.
- Build a usable test history for future design decisions.

---

## What Should Be Logged

Layzr Savre may eventually log several types of data.

Possible data types include:

- Focus coil activity.
- Tracking coil activity.
- PS11 current.
- Driver IC supply voltage.
- Other related voltage rails.
- Startup timing.
- Disc-detection timing.
- Focus-search timing.
- Read-retry timing.
- Fault timing.
- Suspected flatline events.
- ESP32 firmware state.
- Hardware revision.
- Board profile.
- Test condition.
- Console behavior.
- Notes from the tester.

Not every test will include every data type, but every test should include enough context to be useful later.

---

## Test Context Is Required

A log without context may not be useful.

Every log should include information about the console, board, optical drive, disc, hardware revision, firmware revision, and test condition.

At minimum, each test should try to include:

- PS2 model.
- Motherboard revision.
- Driver IC marking, if known.
- Laser model, if known.
- Optical-drive assembly, if known.
- Layzr Savre hardware revision.
- ESP32 firmware revision, if used.
- Measurement method.
- Disc type.
- Disc condition.
- Power supply used.
- Test duration.
- What was being tested.
- What happened.

Without this context, the same waveform or current reading may be hard to understand later.

---

## Recommended Test-Data Folder Structure

Test data should be organized in the `Test-Data/` folder.

Suggested structure:

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

---

## Raw Logs

Raw logs are original data files that have not been edited or cleaned up.

Examples of raw logs:

- ESP32 serial output.
- Raw CSV files.
- Raw JSON logs.
- Oscilloscope waveform exports.
- Logic analyzer captures.
- Current measurement captures.
- Voltage measurement captures.
- Unedited test notes.

Raw logs should be preserved when possible.

Do not overwrite raw logs.

---

## Processed Logs

Processed logs are cleaned, trimmed, converted, or summarized versions of raw logs.

Examples of processed logs:

- Cleaned CSV files.
- Short summaries.
- Annotated fault events.
- Converted waveform data.
- Filtered current logs.
- Comparison tables.
- Notes extracted from raw logs.

Processed logs should reference the original raw log when possible.

---

## Scope Captures

Scope captures should be used for important waveform data.

Useful scope captures may include:

- Focus coil activity.
- Tracking coil activity.
- PS11 current-sense voltage.
- Driver IC voltage.
- Startup behavior.
- Disc-detection behavior.
- Failed-read behavior.
- Suspected flatline behavior.
- Cutoff testing behavior, in the future.

Scope captures should include the time scale, voltage scale, probe point, ground reference, and test condition.

---

## Current Measurements

Current measurements should be used to document PS11 behavior.

Current measurement files may include:

- Shunt voltage readings.
- Estimated current values.
- Current over time.
- Current during startup.
- Current during disc detection.
- Current during normal read.
- Current during failed read.
- Current during suspected flatline behavior.

Current measurements should include the shunt value, shunt power rating, and measurement method.

---

## Voltage Measurements

Voltage measurements may help explain behavior during testing.

Useful voltage measurements may include:

- Driver IC supply voltage.
- ESP32 supply voltage.
- Current-sense amplifier supply voltage.
- Reference voltage.
- Ground offset, if measured.
- Voltage before and after PS11 current-sense path.
- Voltage during startup.
- Voltage during failed reads.

Voltage measurements should be documented with the measurement point and ground reference.

---

## ESP32 Logs

ESP32 logs may eventually become the main data source for Layzr Savre.

Possible ESP32 log contents:

- Timestamp.
- Firmware version.
- Hardware revision.
- Board profile.
- Focus activity state.
- Tracking activity state.
- PS11 current value.
- Driver voltage value.
- Fault state.
- Detection state.
- Cutoff simulation state.
- User configuration.
- Event notes.

Early ESP32 logs can be simple serial text.

Later logs may use CSV or JSON.

---

## Photos

Photos are useful for documenting test setup and board revisions.

Useful photos may include:

- PS2 motherboard revision.
- PS11 fuse location.
- Driver IC marking.
- Laser model.
- Optical-drive assembly.
- Interposer installation.
- Current-sense wiring.
- Scope probe placement.
- Ground reference point.
- ESP32 wiring.
- Mechanical fitment.
- Any damage or repair area.

Photos should be named clearly and linked to the test they belong to.

---

## Test Notes

Test notes should explain what happened during the test.

Useful notes include:

- What the tester expected.
- What actually happened.
- Whether the console booted normally.
- Whether the disc was detected.
- Whether the disc read correctly.
- Whether the drive made abnormal sounds.
- Whether anything became hot.
- Whether the measurement affected behavior.
- Whether the test should be repeated.
- Whether the result seems normal or abnormal.

Simple notes are better than no notes.

---

## Test Reports

A test report is a more complete summary of a test session.

A test report may include:

- Test purpose.
- Console information.
- Hardware setup.
- Firmware setup.
- Measurement setup.
- Disc information.
- Raw data links.
- Processed data links.
- Observed behavior.
- Results.
- Conclusion.
- Follow-up actions.

Test reports can be stored in `Test-Data/Test-Reports/`.

---

## Suggested File Naming

File names should be simple, consistent, and searchable.

Suggested format:

    PS2MODEL-BOARD-SIGNAL-CONDITION-DATE

Examples:

    SCPH75001-GH040-FOCUS-good_dvd-2026-05-13
    SCPH75001-GH040-TRACK-failed_read-2026-05-13
    SCPH75001-GH040-PS11-current-no_disc-2026-05-13
    SCPH79001-GH061-PS11-current-good_dvd-2026-05-13
    SCPH79001-GH061-FOCUS-weak_laser-failed_read-2026-05-13

Use short names, but include enough information to identify the test.

---

## Suggested File Extensions

Possible file extensions:

| File Type | Suggested Extension |
|---|---|
| Plain text log | .txt |
| CSV log | .csv |
| JSON log | .json |
| Scope screenshot | .png |
| Scope waveform export | .csv |
| Logic analyzer capture | Tool-specific format |
| Test report | .md |
| Photo | .jpg or .png |
| Notes | .md or .txt |

Markdown files are preferred for notes and test reports because they display well on GitHub.

---

## Date Format

Use ISO-style dates in file names:

    YYYY-MM-DD

Example:

    2026-05-13

This keeps files sorted properly.

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

Use consistent names so test data can be searched later.

---

## Signal Naming

Suggested signal names:

| Signal | Suggested Name |
|---|---|
| Focus coil activity | FOCUS |
| Focus coil side A | FOCUS_A |
| Focus coil side B | FOCUS_B |
| Tracking coil activity | TRACK |
| Tracking coil side A | TRACK_A |
| Tracking coil side B | TRACK_B |
| PS11 current | PS11_CURRENT |
| PS11 shunt voltage | PS11_SHUNT |
| Driver IC voltage | DRIVER_VCC |
| ESP32 supply voltage | ESP32_VCC |
| Fault state | FAULT_STATE |
| Cutoff simulation | CUTOFF_SIM |
| Cutoff active | CUTOFF_ACTIVE |

Temporary names should be marked as temporary until confirmed.

---

## Logging Formats

Layzr Savre may use more than one logging format.

Useful formats include:

| Format | Use |
|---|---|
| Human-readable text | Early serial debugging |
| CSV | Easy spreadsheet and graphing support |
| JSON | Structured logs for software tools |
| Markdown | Test reports and notes |
| PNG | Scope screenshots and photos |
| Raw waveform export | Detailed signal analysis |

Early development should prioritize readable logs over complex formats.

---

## Human-Readable Log Example

A simple early serial log may look like this:

    time_ms=00001234 state=BOOT firmware=Logger_v0.1
    time_ms=00002000 state=LOGGING_ONLY board_profile=UNKNOWN
    time_ms=00005000 event=FOCUS_ACTIVITY value=ACTIVE
    time_ms=00005100 event=TRACK_ACTIVITY value=ACTIVE
    time_ms=00005200 event=PS11_CURRENT value_mA=320
    time_ms=00008000 event=SUSPECT_FAULT reason=TRACK_NO_ACTIVITY
    time_ms=00009000 event=CUTOFF_SIMULATED reason=FAULT_TIMER_EXPIRED

This is only an example format.

---

## CSV Log Concept

A CSV log may be useful for graphing current and signal activity.

Possible CSV columns:

| Column | Purpose |
|---|---|
| timestamp_ms | Time since boot or test start |
| firmware_version | ESP32 firmware version |
| hardware_revision | Layzr Savre hardware revision |
| board_profile | PS2 board profile |
| focus_activity | Focus activity state |
| tracking_activity | Tracking activity state |
| ps11_current_ma | Estimated PS11 current |
| driver_voltage_v | Driver IC voltage |
| fault_state | Current fault state |
| event | Optional event label |
| notes | Optional notes |

The final format can change as the firmware develops.

---

## JSON Log Concept

A JSON log may be useful later for structured data.

Possible fields:

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

JSON may be useful for future web interface or data viewer tools.

---

## Data Accuracy Notes

Logged data should not be assumed to be perfect.

Possible accuracy concerns:

- ESP32 ADC noise.
- ESP32 ADC calibration.
- Current-sense amplifier offset.
- Shunt tolerance.
- Ground reference error.
- Probe loading.
- Scope probe compensation.
- Sample rate limits.
- Missed fast events.
- File timestamp errors.
- Human note-taking errors.

Every measurement should be treated as evidence, not absolute truth, until verified.

---

## Calibration Notes

Current and voltage measurements may need calibration.

Possible calibration items:

- Shunt resistance.
- ADC reference.
- Current-sense amplifier gain.
- Voltage divider ratio.
- Offset voltage.
- Zero-current reading.
- Known load test.
- Multimeter comparison.
- Oscilloscope comparison.

Calibration values should be stored with the log or test report.

---

## Logging Frequency

Different data types may need different logging rates.

Examples:

| Data Type | Possible Logging Need |
|---|---|
| Fault events | Log immediately |
| PS11 current | Log periodically or on change |
| Focus activity | Log activity state or transitions |
| Tracking activity | Log activity state or transitions |
| Raw waveforms | Use oscilloscope or faster hardware |
| Voltage rails | Log periodically |
| Web status | Update slower than raw logging |
| User settings | Log when changed |

The ESP32 may not be fast enough to log every raw waveform directly.

---

## Raw Waveform Limitation

The ESP32 may not be the right tool for high-speed raw waveform capture.

For raw coil waveforms, better tools may include:

- Oscilloscope.
- Logic analyzer, if signal is digital and safe.
- External ADC.
- Dedicated analog front end.
- Data acquisition hardware.

The ESP32 may be better suited for activity detection, lower-speed current logging, event logging, and user interface features.

---

## Event Logging

Event logging may be more useful than constant raw logging in some cases.

Useful events include:

- ESP32 boot.
- Logging started.
- Disc activity detected.
- Focus activity detected.
- Tracking activity detected.
- PS11 current sampled.
- Current threshold crossed.
- Activity missing.
- Suspected fault.
- Confirmed fault.
- Cutoff simulated.
- Cutoff active, in future hardware.
- Fault reset.
- Firmware error.
- User setting changed.

Event logs should include timestamps.

---

## Fault Logging

Fault logs are important for future protection development.

A fault log should include:

- Fault type.
- Time fault started.
- Fault duration.
- Focus activity state.
- Tracking activity state.
- PS11 current.
- Driver voltage.
- Current threshold.
- Activity threshold.
- Detection mode.
- Whether cutoff was simulated or active.
- Whether the console recovered.
- Notes.

Fault logs should be saved even if the fault turns out to be a false trigger.

---

## False Trigger Logging

False triggers are valuable data.

A false trigger means the system believed a fault happened, but the console was actually behaving normally.

False trigger logs should include:

- What condition caused the trigger.
- What disc was being used.
- What the console was doing.
- What thresholds were active.
- Whether focus activity looked normal.
- Whether tracking activity looked normal.
- What PS11 current looked like.
- How long the trigger lasted.
- Whether the firmware recovered.
- How the logic should be improved.

False triggers should not be hidden.

---

## Test Session Template

Use this template when creating a test session report.

## Test Session Report

### Basic Information

- Date:
- Tester:
- Purpose of test:
- Test location:
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
- Current-sense method:
- Shunt value:
- Signal-conditioning method:
- Cutoff hardware installed:
- Cutoff enabled:

### Firmware

- Firmware name:
- Firmware version:
- Build date:
- Logging mode:
- Detection mode:
- Active cutoff enabled:

### Measurement Setup

- Tools used:
- Probe points:
- Ground reference:
- Scope settings:
- Current measurement method:
- Voltage measurement method:

### Test Condition

- Disc type:
- Disc condition:
- Console state:
- Power supply:
- Test duration:

### Files Collected

- Raw log file:
- Processed log file:
- Scope capture:
- Current measurement:
- Voltage measurement:
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
- Any abnormal heat:
- Any abnormal sound:
- Any instability:

### Results

- Focus behavior summary:
- Tracking behavior summary:
- PS11 current summary:
- Voltage behavior summary:
- Fault behavior summary:
- Recovery behavior summary:

### Conclusion

- Result appears normal:
- Result appears abnormal:
- Data useful for detection:
- More testing needed:
- Follow-up actions:

---

## PS11 Current Log Template

Use this template for PS11 current-specific logs.

## PS11 Current Log Entry

### Console Information

- PS2 model:
- Board revision:
- Driver IC marking:
- Laser model:
- Optical-drive assembly:

### Current-Sense Setup

- PS11 fuse lifted:
- Shunt value:
- Shunt power rating:
- Measurement method:
- Sense amplifier:
- Ground reference:

### Test Condition

- Disc type:
- Disc condition:
- Console state:
- Test duration:

### Measurements

- Startup current:
- No-disc current:
- Disc-detection current:
- Focus-search current:
- Normal-read current:
- Failed-read current:
- Peak current:
- Average current:
- Notes:

### Conclusion

- Current appears normal:
- Current appears abnormal:
- Useful for future detection:
- Follow-up needed:

---

## Scope Capture Template

Use this template for oscilloscope captures.

## Scope Capture Entry

### Console Information

- PS2 model:
- Board revision:
- Driver IC marking:
- Laser model:

### Signal Information

- Signal name:
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
- Read behavior:
- Failed-read behavior:
- Suspected flatline behavior:
- Notes:

### Files

- Scope screenshot:
- Waveform export:
- Related ESP32 log:
- Related current log:

### Conclusion

- Signal useful:
- Signal sensitive:
- Needs buffering:
- Useful for detection:
- Follow-up needed:

---

## Log Review Process

After collecting data, the project should review logs in a consistent way.

Suggested review steps:

1. Confirm the test context is complete.
2. Confirm the file names are clear.
3. Check whether the console behaved normally.
4. Compare focus activity against expected behavior.
5. Compare tracking activity against expected behavior.
6. Compare PS11 current against expected behavior.
7. Look for timing patterns.
8. Look for abnormal current.
9. Look for missing or stuck activity.
10. Identify possible false triggers.
11. Mark whether the data is useful.
12. Add follow-up notes.

---

## Data Quality Levels

Data may be classified by quality.

| Quality Level | Meaning |
|---|---|
| Raw unverified | Data captured but not reviewed |
| Reviewed | Data reviewed for basic correctness |
| Useful | Data has enough context to compare |
| Reference | Data is high-quality and useful for future thresholds |
| Questionable | Data may be affected by setup or measurement problems |
| Invalid | Data should not be used for conclusions |

This helps avoid building detection logic from bad data.

---

## Data Privacy and Copyright

Do not upload copyrighted game data, BIOS files, ROM files, or disc images.

The project should only upload measurement data, photos, logs, notes, and original documentation created for Layzr Savre.

Game titles may be referenced only as test context if needed.

---

## What Not to Log

Do not include:

- BIOS dumps.
- ROM files.
- Game disc images.
- Copyrighted game files.
- Private user information.
- Customer personal information.
- Unlicensed service-manual scans.
- Anything that cannot be redistributed.

Keep the repo focused on project-created test data and documentation.

---

## Data Backup

Important test data should be backed up.

Recommended backup approach:

- Keep raw logs in the repo when practical.
- Keep large files in a separate archive if needed.
- Do not overwrite original raw files.
- Use clear file names.
- Keep notes with each test.
- Store important scope screenshots.
- Keep local backups of large captures.

GitHub may not be ideal for very large raw datasets.

---

## Large File Consideration

Large files may need special handling.

Possible options:

- Compress large logs.
- Store only processed data in the repo.
- Store large raw data outside the repo.
- Use GitHub Releases for larger release packages.
- Use Git LFS only if the project decides to support it.
- Keep summaries in Markdown.

Avoid filling the repo with huge files unless they are important.

---

## Relationship to Flatline Detection

Data logging supports flatline detection.

The project needs data to answer:

- What does normal activity look like?
- What does abnormal activity look like?
- How long can normal quiet periods last?
- What does PS11 current look like during normal operation?
- What does PS11 current look like during failed reads?
- What signal combinations suggest a real fault?
- What conditions create false triggers?
- What thresholds are realistic?

Flatline detection should be based on logged data, not guesses.

---

## Relationship to Cutoff Testing

Data logging must come before cutoff testing.

Before active cutoff is enabled, logs should show:

- Normal behavior.
- Abnormal behavior.
- Suspected fault behavior.
- False trigger behavior.
- Current behavior.
- Timing behavior.
- Detection behavior in logging-only mode.

Cutoff should not be enabled until the logs support the detection logic.

---

## Relationship to Kit Development

Good logs will help future kit development.

Data can support:

- Compatibility lists.
- Board-revision notes.
- Installation guides.
- Troubleshooting guides.
- Firmware thresholds.
- Safety warnings.
- Customer-facing limitations.
- Beta tester instructions.
- Quality-control procedures.

A kit should be supported by test data, not just theory.

---

## Open Questions

Current open data logging questions:

- What is the best early log format?
- Should ESP32 logs start as text, CSV, or JSON?
- What sampling rate is needed for PS11 current?
- What sampling rate is needed for focus and tracking activity?
- Should raw coil waveforms be captured only with a scope?
- Should the ESP32 log activity state instead of raw waveform data?
- How should false triggers be marked?
- How should board profiles be stored in logs?
- How much data should be included in the repo?
- What files should stay local until summarized?
- Should beta testers submit logs through GitHub Issues?
- Should a standard test report template be required?

---

## Current Working Theory

The current working theory is:

- Data logging should begin before active protection.
- Raw data should be preserved when possible.
- Processed data should reference raw data.
- Test context is required for useful logs.
- PS11 current is one useful data point, not the whole system.
- Focus and tracking activity should be compared with PS11 current.
- ESP32 logging should begin with simple serial output.
- Oscilloscope captures are still needed for raw waveform research.
- False triggers should be documented.
- Detection thresholds should come from reviewed test data.

This theory will be updated as the project develops.

---

## Future Logging Goals

Future logging features may include:

- Live ESP32 serial logging.
- CSV export.
- JSON export.
- Web interface log viewer.
- Fault-event history.
- Current graphing.
- Voltage graphing.
- Activity timeline.
- Board profile tagging.
- Automatic test session metadata.
- Log export button.
- Beta tester log package.
- Data viewer software.

These features should be added after basic logging is reliable.

---

## Summary

Data logging is the foundation of Layzr Savre.

The project needs real measurements before it can make reliable decisions about flatline detection, current monitoring, cutoff behavior, compatibility, or kit release.

Good logs should include signal data, PS11 current data, voltage data where useful, timing, test context, and honest notes about what happened.

The goal is to build a useful record of PS2 optical-drive behavior so Layzr Savre can move from theory to tested hardware.
