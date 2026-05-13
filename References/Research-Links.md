# Research Links

**Project:** PS2 Layzr Savre  
**Owner:** FatBaldDad  
**Status:** Early research / planning / prototype development  
**Folder:** References  

---

## Overview

This file is used to organize reference material for the PS2 Layzr Savre project.

Layzr Savre depends on careful research, measurement, and documentation. This file should collect useful links, notes, datasheet references, board-revision information, pinout references, community discussions, videos, and other research sources related to the PlayStation 2 optical-drive system.

This document should be updated as new information is found.

---

## Purpose of This Folder

The `References/` folder is intended to hold supporting information for the project.

Current planned structure:

    References/
    ├── Datasheets/
    ├── PS2-Board-Notes/
    ├── Pinouts/
    └── Research-Links.md

The goal is to keep project research organized and easy to find.

---

## Important Notice

Do not upload copyrighted or restricted material unless it is allowed to be redistributed.

Do not upload:

- BIOS files.
- ROM files.
- Game files.
- Disc images.
- Copyrighted Sony service manual scans.
- Private Discord logs without permission.
- Private customer information.
- Commercial documents that cannot be redistributed.
- Files copied from another project without permission.

When possible, link to public sources instead of re-uploading files.

---

## Reference Categories

Research links should be organized by category.

Suggested categories:

- Datasheets
- PS2 board notes
- Pinouts
- Optical-drive research
- Driver IC research
- DSP research
- PS11 current monitoring
- Focus and tracking coil research
- Flatline detection research
- Current-sense circuit research
- ESP32 firmware research
- Signal-conditioning research
- Community discussions
- Videos
- GitHub repositories
- Articles and forum posts
- Test-data references

---

## Datasheets

Datasheets should be stored or referenced in:

    References/Datasheets/

Useful datasheets may include:

- Driver IC datasheets.
- Current-sense amplifier datasheets.
- MOSFET datasheets.
- Load switch datasheets.
- Comparator datasheets.
- Op-amp datasheets.
- ESP32 module datasheets.
- Voltage regulator datasheets.
- Fuse datasheets.
- Connector datasheets.
- Shunt resistor datasheets.

Only store datasheets if redistribution is allowed.

If redistribution is not clearly allowed, add a link and notes instead.

---

## Datasheet Reference Template

Use this template when adding a datasheet reference.

## Datasheet Reference

### Part Information

- Part number:
- Manufacturer:
- Description:
- Package:
- Used for:
- Project area:

### Source

- Link:
- Local file stored:
- File location:
- Date accessed:

### Notes

- Important pins:
- Important ratings:
- Voltage range:
- Current range:
- Thermal notes:
- Layout notes:
- Concerns:
- Follow-up needed:

---

## PS2 Board Notes

Board notes should be stored in:

    References/PS2-Board-Notes/

Board notes should document differences between PS2 models and motherboard revisions.

Useful board information may include:

- PS2 model number.
- Motherboard revision.
- Region.
- Driver IC marking.
- DSP marking.
- Mechacon or Syscon marking.
- PS11 fuse location.
- Optical-drive connector information.
- Laser model.
- Optical-drive assembly.
- Fuse map.
- Signal locations.
- Ground reference points.
- Photos of relevant board areas.
- Known differences from other board revisions.

Board notes are important because Layzr Savre should not assume every PS2 revision behaves the same.

---

## PS2 Board Note Template

Use this template when documenting a board revision.

## PS2 Board Note

### Console Information

- PS2 model:
- Region:
- Motherboard revision:
- Date code, if known:
- Optical-drive assembly:
- Laser model:
- Other mods installed:

### IC Information

- Driver IC marking:
- DSP marking:
- Mechacon or Syscon marking:
- Other related ICs:

### Fuse Information

- PS11 location:
- PS11 confirmed as physical fuse:
- PS11 feeds:
- Other nearby fuse labels:
- Fuse notes:

### Signal Notes

- Focus signal locations:
- Tracking signal locations:
- Driver IC output notes:
- Optical-drive connector notes:
- Ground reference points:
- Voltage rail notes:

### Photos

- Board overview:
- PS11 area:
- Driver IC area:
- Optical-drive connector:
- Laser assembly:
- Notes:

### Test Status

- Baseline console test:
- Passive monitoring tested:
- PS11 current tested:
- ESP32 logging tested:
- Detection tested:
- Cutoff tested:
- Known issues:

---

## Pinouts

Pinout notes should be stored in:

    References/Pinouts/

Pinout information may include:

- Optical-drive connector pinouts.
- Laser ribbon pinouts.
- Driver IC pin notes.
- ESP32 interface pin assignments.
- Test pad maps.
- PS11 current-sense wiring.
- Interposer connector mapping.
- Programming header pinouts.
- UART pinouts.
- Ground and voltage reference points.

Pinouts should be marked clearly as verified or unverified.

---

## Pinout Reference Template

Use this template when documenting a pinout.

## Pinout Reference

### Basic Information

- Name:
- Board revision:
- Connector or IC:
- Location:
- Source:
- Verified:
- Verified by:
- Date verified:

### Pinout Table

| Pin | Signal Name | Direction | Voltage | Description | Status | Notes |
|---|---|---|---|---|---|---|
| 1 | TBD | Unknown | Unknown | TBD | Unverified |  |
| 2 | TBD | Unknown | Unknown | TBD | Unverified |  |
| 3 | TBD | Unknown | Unknown | TBD | Unverified |  |

### Notes

- Orientation:
- Pin 1 marker:
- Measurement method:
- Risk level:
- Follow-up needed:

---

## Optical-Drive Research

Optical-drive research should focus on understanding the PS2 laser and drive behavior.

Useful topics:

- Focus behavior.
- Tracking behavior.
- Disc detection.
- Startup behavior.
- Read retries.
- Failed reads.
- Weak laser behavior.
- Dirty disc behavior.
- Scratched disc behavior.
- Optical-drive mechanical issues.
- Laser replacement notes.
- Calibration notes.
- Failure symptoms.

Research should be compared against real measurements when possible.

---

## Driver IC Research

Driver IC research is important because Layzr Savre is monitoring behavior related to the driver IC and coil-drive paths.

Useful topics:

- Driver IC part numbers by board revision.
- Driver IC pin functions.
- Focus output pins.
- Tracking output pins.
- Power input pins.
- Ground pins.
- Enable, mute, or standby pins.
- Thermal behavior.
- Current limits.
- Fault behavior.
- PS11 relationship to driver IC power.

Do not assume one driver IC applies to every PS2 model.

---

## PS11 Research

PS11 is a physical fuse on the PS2 motherboard.

For this project, PS11 is currently being studied as a current-monitoring point because it provides power to the driver IC in the area being studied.

Important PS11 notes:

- PS11 is a fuse.
- One side of PS11 may be lifted for current-monitoring research.
- The goal is to measure current through the PS11 fuse path.
- PS11 should not be assumed to represent the entire optical-drive system.
- PS11 should not be assumed to represent the entire laser-control system.
- PS11 current alone should not be treated as proof of a fault.
- The fuse protection role must be preserved.

Useful PS11 research topics:

- PS11 location by board revision.
- PS11 fuse rating.
- PS11 input and output side.
- Driver IC pin or section powered by PS11.
- Normal current through PS11.
- Failed-read current through PS11.
- Voltage drop concerns.
- Current-sense shunt value.
- Current-sense amplifier options.
- Safe installation method.

---

## PS11 Research Template

Use this template for PS11-specific research.

## PS11 Research Entry

### Console Information

- PS2 model:
- Motherboard revision:
- Region:
- Driver IC marking:
- Laser model:
- Optical-drive assembly:

### PS11 Information

- PS11 physical location:
- PS11 fuse rating:
- PS11 input side:
- PS11 output side:
- Feeds driver IC:
- Confirmation method:
- Photo reference:

### Current Monitoring Notes

- Fuse side lifted:
- Shunt value:
- Shunt power rating:
- Sense amplifier:
- Measurement method:
- Voltage drop:
- Estimated current:
- Operation affected:

### Notes

- Concerns:
- Follow-up needed:
- Verified:
- Date:

---

## Focus and Tracking Coil Research

Focus and tracking coil research should document the signals Layzr Savre may monitor for activity and possible flatline behavior.

Useful research topics:

- Focus coil signal locations.
- Tracking coil signal locations.
- Differential measurement methods.
- Driver IC output pins.
- Optical-drive connector pins.
- Normal activity patterns.
- Failed-read activity patterns.
- Signal voltage range.
- Signal frequency or activity range.
- Safe signal-conditioning methods.
- ESP32-compatible activity detection.

Focus and tracking signals should be treated as sensitive until verified.

---

## Flatline Detection Research

Flatline detection research should focus on identifying abnormal signal behavior.

Useful topics:

- What normal activity looks like.
- What no-disc activity looks like.
- What startup activity looks like.
- What failed-read activity looks like.
- What weak-laser behavior looks like.
- What stuck-high behavior may look like.
- What stuck-low behavior may look like.
- What missing activity may look like.
- How PS11 current changes during suspected faults.
- How long normal quiet periods last.
- How to avoid false triggers.

Flatline detection should be based on real test data, not assumptions.

---

## Current-Sense Circuit Research

Current-sense research may support PS11 current monitoring.

Useful topics:

- Low-value shunt resistor selection.
- Shunt resistor power rating.
- Shunt tolerance.
- Kelvin sensing.
- Current-sense amplifier selection.
- High-side current measurement.
- Common-mode voltage range.
- Output scaling for ESP32 ADC.
- Filtering.
- Noise.
- Calibration.
- Voltage drop.
- Fuse protection preservation.

Current-sense design should avoid affecting normal console operation.

---

## Signal-Conditioning Research

Signal conditioning is needed before PS2 signals reach the ESP32.

Useful topics:

- High-impedance buffers.
- Voltage dividers.
- RC filters.
- Clamp diodes.
- Comparators.
- Differential amplifiers.
- Current-sense amplifiers.
- External ADCs.
- Input protection.
- ESD protection.
- Backfeeding prevention.
- Level shifting.
- Filtering without hiding useful activity.

Signal conditioning should protect both the PS2 and the ESP32.

---

## ESP32 Research

ESP32 research should support firmware and interface development.

Useful topics:

- ESP32 module selection.
- ESP32 ADC accuracy.
- External ADC options.
- GPIO boot states.
- Strapping pins.
- UART programming.
- Wi-Fi logging.
- Web interface hosting.
- OTA updates.
- Power consumption.
- Brownout behavior.
- Safe power-domain design.
- Backfeeding prevention.
- PlatformIO setup.

The ESP32 should begin as a logger before controlling hardware.

---

## Community Discussion References

Community discussions can be useful, but they should be documented carefully.

When referencing community discussions:

- Credit the source if appropriate.
- Do not copy private logs without permission.
- Summarize the useful technical point.
- Include date and context if possible.
- Mark unverified information as unverified.
- Do not treat claims as proven without measurement.

Community references should support research, not replace testing.

---

## Video References

Videos may be useful for installation, repair, and behavior observations.

Useful video topics:

- PS2 optical-drive repair.
- Laser replacement.
- Laser calibration.
- Focus and tracking behavior.
- Driver IC troubleshooting.
- Fuse troubleshooting.
- Oscilloscope probing.
- ESP32 logging.
- Current-sense circuit testing.

When adding videos, include notes about what part of the video is useful.

---

## GitHub Repository References

Other GitHub repositories may be useful for firmware, ESP32 examples, current logging, or PS2 research.

When referencing a repository:

- Include repository name.
- Include link.
- Include what it is useful for.
- Include license if relevant.
- Do not copy code without checking the license.
- Note whether it is used directly or only as inspiration.

---

## Link Entry Template

Use this template when adding a research link.

## Research Link Entry

### Basic Information

- Title:
- Author or source:
- Link:
- Date accessed:
- Category:
- Related project area:

### Why It Matters

- Useful information:
- Related hardware:
- Related firmware:
- Related board revision:
- Related signal:

### Verification Status

- Verified by measurement:
- Verified by datasheet:
- Community claim only:
- Needs follow-up:
- Confidence level:

### Notes

- Important details:
- Concerns:
- Follow-up action:

---

## Research Confidence Levels

Use confidence levels to avoid treating unverified information as proven.

| Confidence Level | Meaning |
|---|---|
| Unverified | Found in a source but not checked |
| Community Report | Reported by someone else, not independently verified |
| Measured Once | Measured on one console or one board |
| Repeated Measurement | Confirmed by repeated testing |
| Board-Specific Verified | Confirmed for a specific board revision |
| Multi-Board Verified | Confirmed across multiple board revisions |
| Datasheet Supported | Supported by datasheet or official part documentation |
| Project Confirmed | Confirmed and used by Layzr Savre design |

Most early research should be marked as unverified or board-specific until tested.

---

## Research Status Labels

Suggested status labels:

| Status | Meaning |
|---|---|
| To Review | Source found but not reviewed |
| Useful | Source contains useful information |
| Needs Verification | Source may be useful but needs testing |
| Verified | Confirmed by measurement or documentation |
| Outdated | May no longer apply or may be incomplete |
| Board-Specific | Applies only to a specific PS2 board |
| Not Useful | Reviewed but not useful |
| Do Not Use | Incorrect, unsafe, or misleading |

---

## Example Research Link Entry

## Research Link Entry

### Basic Information

- Title: Example PS2 optical-drive repair note
- Author or source: Example source
- Link: Add link here
- Date accessed: YYYY-MM-DD
- Category: Optical-drive research
- Related project area: Focus and tracking behavior

### Why It Matters

- Useful information: May show symptoms of failed read behavior.
- Related hardware: Optical pickup and driver IC.
- Related firmware: None.
- Related board revision: Unknown.
- Related signal: Focus and tracking activity.

### Verification Status

- Verified by measurement: No
- Verified by datasheet: No
- Community claim only: Yes
- Needs follow-up: Yes
- Confidence level: Unverified

### Notes

- Important details: Needs comparison against real scope captures.
- Concerns: May not apply to all board revisions.
- Follow-up action: Test on known-good console.

---

## Local File Naming

For local reference files, use clear names.

Suggested format:

    CATEGORY-PART_OR_TOPIC-SOURCE-DATE

Examples:

    Datasheet-CurrentSenseAmp-ExamplePart-2026-05-13.pdf
    BoardNote-SCPH75001-GH040-PS11-2026-05-13.md
    Pinout-GH040-OpticalDriveConnector-2026-05-13.md
    Research-FlatlineDetection-Notes-2026-05-13.md

Avoid vague file names such as:

- scan.pdf
- notes.txt
- new.pdf
- board.jpg
- unknown.doc

---

## Datasheet File Notes

When storing datasheets, include a small note file if useful.

Suggested note file information:

- Part number.
- Manufacturer.
- What the part is used for.
- Important pins.
- Voltage rating.
- Current rating.
- Package.
- Link to original source.
- Date downloaded.
- License or redistribution note, if known.

Do not rename datasheets in a way that makes the part number hard to find.

---

## Board Photo Notes

Board photos should be named and documented clearly.

Useful photo labels:

- PS2 model.
- Board revision.
- Area photographed.
- Date.
- Notes.

Examples:

    SCPH75001-GH040-PS11-area-2026-05-13.jpg
    SCPH75001-GH040-driver-ic-2026-05-13.jpg
    SCPH79001-GH061-optical-connector-2026-05-13.jpg

Board photos should not include private customer information.

---

## Pinout Verification Rules

Pinouts should not be considered verified unless checked.

Verification may include:

- Continuity testing.
- Visual trace following.
- Datasheet comparison.
- Oscilloscope measurement.
- Multimeter measurement.
- Known board revision comparison.
- Repeated testing.

Mark pinouts clearly as verified or unverified.

---

## Reference Review Process

Suggested process when adding a new reference:

1. Add the link or file.
2. Categorize it.
3. Write a short summary.
4. Mark verification status.
5. Note related project area.
6. Note related board revision, if any.
7. Add follow-up action.
8. Update relevant documentation if the source is useful.
9. Do not treat it as proven until tested.

---

## Relationship to Documentation

References should support the project documentation.

Useful references may lead to updates in:

- `Documentation/02-PS2-Laser-System-Basics.md`
- `Documentation/03-Signal-Research.md`
- `Documentation/04-Flatline-Detection-Theory.md`
- `Documentation/05-PS11-Current-Monitoring.md`
- `Documentation/06-Coil-Power-Cutoff-Method.md`
- `Documentation/07-ESP32-Interface.md`
- `Documentation/09-Testing-Plan.md`
- `SAFETY_AND_LIMITATIONS.md`

When documentation is updated from a reference, note the source if appropriate.

---

## Relationship to Hardware

References may guide hardware decisions.

Useful hardware decisions supported by references:

- Driver IC pin identification.
- PS11 current-sense method.
- Shunt resistor selection.
- Current-sense amplifier selection.
- Signal-conditioning method.
- ESP32 input protection.
- Connector selection.
- Fuse protection method.
- Cutoff method, if added later.

Hardware should not be finalized from one unverified source.

---

## Relationship to Firmware

References may guide firmware decisions.

Useful firmware decisions supported by references:

- ESP32 pin selection.
- ADC calibration method.
- Logging format.
- Current conversion.
- Timing windows.
- Detection thresholds.
- Board profiles.
- Web interface design.
- Safety lockout behavior.

Firmware thresholds should come from measured test data, not only references.

---

## Open Research Questions

Current open research questions:

- Which PS2 board revision should be mapped first?
- Which driver IC is used on each target board?
- What exact driver IC input is powered through PS11?
- What is the safe PS11 current-sense method?
- What shunt value is safe at PS11?
- How much voltage drop at PS11 is acceptable?
- What focus signals are useful to monitor?
- What tracking signals are useful to monitor?
- Should coil activity be measured differentially?
- What conditioning circuit is best for ESP32 input?
- Is the ESP32 ADC accurate enough for PS11 current logging?
- What does normal focus activity look like?
- What does normal tracking activity look like?
- What does a suspected flatline event look like?
- What cutoff point is safest, if any?
- What board revisions behave differently?

---

## Current Working Theory

The current working theory is:

- References should guide testing, not replace testing.
- Board-revision differences must be documented.
- PS11 should be treated as a physical fuse and current-monitoring point.
- PS11 current is one data point only.
- Focus and tracking activity need real measurements.
- Driver IC behavior must be documented by board revision.
- ESP32 inputs require safe signal conditioning.
- Active cutoff should not be designed from unverified assumptions.
- Useful references should be linked to test data when possible.

This theory will be updated as research continues.

---

## Summary

The `References/` folder is the research library for Layzr Savre.

It should collect datasheets, board notes, pinouts, links, videos, community references, and research notes that support the project.

Every reference should be treated carefully, categorized, and marked with a verification status.

The goal is to build a useful research base that supports safe hardware design, reliable firmware, accurate testing, and honest documentation.
