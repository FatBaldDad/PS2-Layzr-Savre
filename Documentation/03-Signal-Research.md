# Signal Research

**Project:** PS2 Layzr Savre  
**Owner:** FatBaldDad  
**Status:** Early research / planning / prototype development  
**Document:** 03 - Signal Research  

---

## Overview

This document is used to track signal research for the PS2 Layzr Savre project.

The goal is to identify which PS2 optical-drive, DSP, driver IC, tracking, focusing, fuse, current, and voltage signals may be useful for monitoring, logging, flatline detection, and future protection behavior.

This document should be treated as a living research file.

At this stage, signals should be considered unverified unless they have been measured, documented, and confirmed on a specific PS2 board revision.

---

## Purpose of Signal Research

Layzr Savre depends on understanding which signals can be safely monitored and which signals should not be touched.

The purpose of this research is to:

- Identify useful optical-drive signals.
- Identify safe monitoring points.
- Identify signals that may show focus activity.
- Identify signals that may show tracking activity.
- Identify signals that may show abnormal or flatline behavior.
- Identify the PS11 fuse path for current monitoring.
- Identify driver IC power behavior.
- Identify board-revision differences.
- Confirm which signals are safe to observe.
- Confirm which signals should not be loaded or interrupted.
- Build a signal map for future hardware revisions.

---

## Important Warning

Signals in the PS2 optical-drive system may be sensitive.

A monitoring circuit can still affect normal console behavior if it adds too much load, capacitance, leakage, noise, or ground error.

Until tested, every signal should be treated as sensitive.

Do not assume a signal is safe to connect to an ESP32, logic analyzer, oscilloscope, current monitor, or cutoff circuit without understanding the signal level and circuit behavior.

---

## Research Priority

The current signal research priority is:

1. Identify the tracking coil drive signals.
2. Identify the focusing coil drive signals.
3. Identify the driver IC outputs related to tracking and focusing.
4. Identify the PS11 fuse path that provides power to the driver IC.
5. Determine how to monitor current through the PS11 fuse location.
6. Identify safe ground references.
7. Identify useful voltage rails.
8. Identify which signals may indicate normal activity.
9. Identify which signals may indicate abnormal or flatline behavior.
10. Identify signals that should remain monitor-only.

---

## Signal Categories

Layzr Savre signal research is divided into several categories.

| Category | Purpose |
|---|---|
| Focus coil signals | Observe lens up/down focusing behavior |
| Tracking coil signals | Observe lens side-to-side tracking behavior |
| Driver IC outputs | Observe the outputs driving optical-drive loads |
| Driver IC power | Observe the power feeding the driver IC |
| PS11 fuse path | Monitor current through the fuse path feeding the driver IC |
| DSP-related signals | Observe control behavior from the optical-drive logic |
| Voltage rails | Confirm stable power during drive operation |
| Ground references | Provide safe measurement reference points |
| ESP32 interface signals | Provide conditioned signals for logging and diagnostics |
| Fault/cutoff signals | Future control signals for active protection |

---

## Current Known PS11 Information

PS11 is a physical fuse on the PS2 motherboard.

For this project, PS11 is currently being treated as a fuse that provides power to the driver IC in the optical-drive area being studied.

The current plan is to lift one side of the PS11 fuse and use that fuse location as a current-monitoring point.

The goal is to measure current through the PS11 fuse path during different optical-drive conditions.

Important notes:

- PS11 is a fuse.
- PS11 provides power to the driver IC in the area being studied.
- PS11 should not be assumed to represent the entire optical-drive power system.
- PS11 should not be assumed to represent the entire laser-control system.
- PS11 current alone should not be treated as proof of a fault.
- PS11 current may become one useful data point in a larger detection system.
- The original protective purpose of the fuse must be preserved.
- The current-monitoring method must not defeat the fuse protection.

---

## PS11 Current Research Goals

The PS11 current-monitoring research should answer these questions:

- What exact driver IC power input is fed through PS11?
- Does the PS11 path differ by board revision?
- What is the normal current through PS11 with no disc?
- What is the normal current through PS11 during disc detection?
- What is the normal current through PS11 during focus search?
- What is the normal current through PS11 during a successful read?
- What is the normal current through PS11 during a failed read?
- What is the normal current through PS11 with a weak laser?
- What is the normal current through PS11 with a dirty or scratched disc?
- What current behavior is abnormal?
- How much voltage drop can be safely added at the PS11 fuse location?
- What current-sense value is safe?
- What current-sense amplifier or measurement method is best?
- How noisy is the measurement?
- Can PS11 current help confirm a future flatline or fault condition?

---

## Focus Coil Signal Research

The focus coils move the optical pickup lens up and down to maintain focus on the disc surface.

Focus coil signals are important because they may show whether the system is actively trying to focus or whether the drive output has become stuck or inactive.

Research goals:

- Identify focus coil positive and negative signal paths.
- Identify where the focus coil signals leave the driver IC.
- Identify where the focus coil signals appear at the ribbon cable or optical pickup connector.
- Measure normal focus-search behavior.
- Measure focus behavior during successful disc detection.
- Measure focus behavior during failed disc detection.
- Measure focus behavior during normal reading.
- Measure focus behavior during read retries.
- Identify whether focus activity changes with weak lasers or bad discs.
- Identify whether a focus flatline condition can be detected reliably.

Possible focus-related signal states:

- Normal dynamic activity.
- Focus search pulses.
- Reduced activity.
- Stuck-high behavior.
- Stuck-low behavior.
- No activity.
- Abnormal sustained drive.
- Noisy or unstable behavior.

---

## Tracking Coil Signal Research

The tracking coils move the optical pickup lens side to side so the laser can follow the disc track.

Tracking coil signals are important because they may show normal seeking behavior, read correction behavior, and possible stuck or flatline conditions.

Research goals:

- Identify tracking coil positive and negative signal paths.
- Identify where the tracking coil signals leave the driver IC.
- Identify where the tracking coil signals appear at the ribbon cable or optical pickup connector.
- Measure normal tracking behavior during disc read.
- Measure tracking behavior during seeking.
- Measure tracking behavior during read retries.
- Measure tracking behavior during failed reads.
- Identify whether tracking behavior changes with dirty or scratched discs.
- Identify whether tracking behavior changes with weak lasers.
- Identify whether a tracking flatline condition can be detected reliably.

Possible tracking-related signal states:

- Normal dynamic activity.
- Seeking activity.
- Read correction activity.
- Reduced activity.
- Stuck-high behavior.
- Stuck-low behavior.
- No activity.
- Abnormal sustained drive.
- Noisy or unstable behavior.

---

## Driver IC Signal Research

The driver IC is a key part of the optical-drive system because it drives loads such as the focus coils, tracking coils, motors, or other drive-related circuits depending on board revision.

Research goals:

- Identify the driver IC used on each target board revision.
- Identify which pins relate to focus coil output.
- Identify which pins relate to tracking coil output.
- Identify which pins relate to sled or spindle control if useful.
- Identify which power inputs feed the driver IC.
- Confirm which power input is supplied through PS11.
- Measure driver IC output behavior during normal operation.
- Measure driver IC output behavior during failed reads.
- Check driver IC temperature during testing.
- Identify any output behavior that may indicate a dangerous condition.

Important note:

The term "driver IC" should be used carefully because different PS2 board revisions may use different parts or different signal routing.

Each board revision should be documented separately.

---

## DSP Signal Research

The DSP is involved in optical-drive signal processing and control behavior.

Layzr Savre may eventually monitor DSP-related behavior, but DSP signals should be treated with extra care.

Research goals:

- Identify DSP-related signals that may be useful for observation.
- Determine which signals are safe to monitor.
- Avoid loading sensitive DSP signals.
- Avoid interrupting DSP signals during early development.
- Compare DSP-controlled behavior during normal and failed reads.
- Determine whether any DSP-related signal can help identify expected drive activity.

At this stage, DSP signals should be considered monitor-only unless proven otherwise.

---

## Voltage Rail Research

Voltage monitoring may help explain abnormal behavior.

Research goals:

- Identify voltage rails related to the optical-drive and driver IC area.
- Identify which rails remain active during standby.
- Identify which rails become active during drive use.
- Measure voltage stability during startup.
- Measure voltage stability during disc reads.
- Measure voltage stability during failed reads.
- Check for voltage dips during high current events.
- Check whether added monitoring hardware causes voltage drop.

Possible voltage rails to document:

- Driver IC supply rail through PS11.
- Logic supply rails near the optical-drive area.
- ESP32 supply rail.
- Any reference voltages used by monitoring circuits.
- Ground reference points.

---

## Ground Reference Research

Good ground reference points are required for accurate measurements.

Research goals:

- Identify safe ground points near the optical-drive circuit.
- Identify ground points near PS11.
- Identify ground points near the driver IC.
- Identify ground points near the ESP32 interface board.
- Avoid ground loops during measurement.
- Avoid using poor or noisy ground references.
- Document which ground point was used for each measurement.

Ground reference should be included in every test log.

---

## Signal Safety Levels

Each signal should be classified before being connected to Layzr Savre hardware.

Suggested signal classifications:

| Classification | Meaning |
|---|---|
| Unknown | Signal has not been measured yet |
| Monitor-only | Signal may be observed but not controlled |
| Buffered monitor | Signal may be monitored only through a buffer or high-impedance input |
| Conditioned input | Signal can be safely level-shifted or filtered for ESP32 input |
| Current-sense only | Signal or path is only used for current measurement |
| Do not connect | Signal should not be connected to Layzr Savre hardware |
| Future control candidate | Signal may be considered for future control after testing |
| Active control | Signal is intentionally controlled by Layzr Savre hardware |

Early research should classify most signals as `Unknown` or `Monitor-only` until proven safe.

---

## Signal Map Template

Use this template when documenting a signal.

| Field | Entry |
|---|---|
| Signal name |  |
| Temporary name |  |
| Board revision |  |
| PS2 model |  |
| IC or connector |  |
| Pin or pad |  |
| Signal type |  |
| Expected voltage range |  |
| Measured voltage range |  |
| AC or DC behavior |  |
| Normal behavior |  |
| Failed-read behavior |  |
| No-disc behavior |  |
| Startup behavior |  |
| Safe to monitor | Unknown |
| Safe for ESP32 input | Unknown |
| Requires buffer | Unknown |
| Requires level shifting | Unknown |
| Risk level | Unknown |
| Notes |  |

---

## Candidate Signals to Research

The following table is a working list of signal areas to research.

| Candidate Signal Area | Purpose | Current Status |
|---|---|---|
| Focus coil positive | Observe focus coil drive | Research needed |
| Focus coil negative | Observe focus coil drive | Research needed |
| Tracking coil positive | Observe tracking coil drive | Research needed |
| Tracking coil negative | Observe tracking coil drive | Research needed |
| Driver IC power through PS11 | Monitor current through fuse path | Research needed |
| Driver IC ground reference | Measurement reference | Research needed |
| Driver IC output pins | Observe output behavior | Research needed |
| DSP-related control signals | Observe expected activity | Research needed |
| Optical-drive connector pins | Interposer mapping | Research needed |
| ESP32 analog inputs | Data logging | Planned |
| ESP32 digital inputs | Activity detection | Planned |
| Fault output signal | Future active protection | Future research |
| Cutoff control signal | Future power cutoff | Future research |

---

## Measurement Methods

Different signals may require different measurement methods.

Possible measurement tools:

- Multimeter.
- Oscilloscope.
- Differential oscilloscope probe.
- Logic analyzer.
- Current-sense amplifier.
- Low-value current shunt.
- ESP32 ADC input.
- External ADC.
- Serial data logger.
- Thermal camera or temperature probe.
- Bench power supply, where appropriate.

High-speed or sensitive signals should be measured with proper probing methods.

---

## Oscilloscope Measurement Notes

When using an oscilloscope:

- Use a proper ground reference.
- Avoid long ground leads when possible.
- Use high-impedance probes.
- Start with passive observation.
- Confirm voltage range before connecting.
- Avoid shorting adjacent pins.
- Avoid probing moving parts while the disc is spinning.
- Document probe location.
- Document time scale.
- Document voltage scale.
- Save screenshots or waveform files.
- Record the disc type and test condition.

For differential coil signals, a differential measurement may be more useful than measuring only one side to ground.

---

## Logic Analyzer Measurement Notes

A logic analyzer may be useful for digital signals, but it should not be connected to unknown analog or high-voltage signals.

Before using a logic analyzer:

- Confirm the signal voltage range.
- Confirm the signal is digital or logic-level.
- Confirm the logic analyzer input is protected.
- Confirm the ground reference is safe.
- Avoid connecting directly to unknown driver outputs.
- Use buffering or level shifting if needed.

Do not assume a coil-drive output is safe for a logic analyzer.

---

## ESP32 Measurement Notes

The ESP32 may be useful for logging slower analog or digital data, but it has limitations.

ESP32 concerns:

- ADC accuracy is limited.
- ADC readings may be noisy.
- Inputs must not exceed safe voltage levels.
- GPIO boot states must be considered.
- Inputs should not backfeed the PS2 when unpowered.
- Fast coil activity may need conditioning before logging.
- External ADC or analog front end may be needed.
- Protection resistors, filters, clamps, or buffers may be required.

The ESP32 should not be directly connected to unknown PS2 signals.

---

## Current Shunt Research Notes

For PS11 current monitoring, the planned idea is to lift one side of PS11 and insert or route a known current-sense path so current can be measured.

Research concerns:

- The shunt value must be low enough to avoid affecting normal operation.
- The shunt must be rated for the expected current.
- The shunt should not bypass the original fuse protection.
- The fuse protection role must be preserved.
- The voltage drop must be measured accurately.
- The measurement circuit must not inject noise into the driver IC supply.
- The wiring must be short and secure.
- The hardware must not mechanically stress the fuse pads.
- The method must be documented clearly for each board revision.

At this stage, PS11 current monitoring is for observation only.

---

## Flatline Detection Research

Flatline detection should be based on real measured behavior.

Signals that may help with flatline detection:

- Focus coil activity.
- Tracking coil activity.
- Driver IC output behavior.
- PS11 current behavior.
- Timing during expected drive activity.
- Voltage behavior during fault conditions.

Possible detection ideas:

- Detect missing dynamic activity.
- Detect stuck-high behavior.
- Detect stuck-low behavior.
- Detect abnormal current during failed read.
- Detect sustained no-change behavior during expected activity.
- Require multiple signals before fault trigger.
- Ignore startup and disc-detection windows.
- Ignore short glitches.
- Add a time delay before declaring a fault.

Flatline detection must avoid false triggers during normal drive behavior.

---

## Signals That Should Be Treated Carefully

The following signal types should be treated carefully until fully understood:

- Direct laser diode control signals.
- Optical feedback signals.
- DSP analog inputs.
- Driver IC outputs.
- Coil-drive outputs.
- Reference voltages.
- High-speed communication signals.
- Motor-drive outputs.
- Power rails feeding sensitive ICs.
- Any signal that changes behavior when probed.

Early Layzr Savre versions should avoid controlling these signals.

---

## Monitor-Only Rule

Until a signal is proven safe, it should be monitor-only.

Monitor-only means:

- Do not pull it high.
- Do not pull it low.
- Do not interrupt it.
- Do not drive it from ESP32 GPIO.
- Do not connect it directly to a low-impedance input.
- Do not attach long wires without understanding the effect.
- Do not use it as a protection trigger by itself.

Observation comes before control.

---

## Naming Convention

Use clear names when documenting signals.

Suggested naming style:

| Type | Example Name |
|---|---|
| Focus coil signal | FOCUS_COIL_A |
| Focus coil signal | FOCUS_COIL_B |
| Tracking coil signal | TRACK_COIL_A |
| Tracking coil signal | TRACK_COIL_B |
| PS11 current sense positive | PS11_SENSE_P |
| PS11 current sense negative | PS11_SENSE_N |
| Driver IC supply | DRIVER_VCC |
| Driver IC ground | DRIVER_GND |
| Fault output | FAULT_OUT |
| ESP32 logging input | ESP32_LOG_IN_1 |

Temporary names should be clearly marked until confirmed.

---

## Board Revision Documentation

Every signal should be tied to a specific board revision.

Required board information:

- PS2 model number.
- Motherboard revision.
- Region, if useful.
- Optical-drive assembly.
- Laser model, if known.
- Driver IC marking.
- DSP marking, if known.
- Fuse designator.
- Connector reference.
- Photos of the area, if available.

Do not assume that a signal map from one board applies to all boards.

---

## Test Condition Documentation

Every signal capture should include test conditions.

Useful test conditions:

- No disc.
- Known-good PS2 DVD game.
- Known-good PS2 CD game.
- Known-good PS1 disc.
- Audio CD.
- DVD video.
- Dirty disc.
- Scratched disc.
- Weak laser.
- Failed read.
- Browser idle.
- Game loading.
- Long-duration read.
- Startup only.
- Lid open or tray open, where applicable.

---

## Data File Naming

Suggested file naming format:

- model-board-signal-condition-date
- example: SCPH75001-GH040-FOCUS_COIL_A-good_dvd-2026-05-13
- example: SCPH75001-GH040-PS11_CURRENT-failed_read-2026-05-13
- example: SCPH79001-GH061-TRACK_COIL_B-startup-2026-05-13

Keep names simple and searchable.

---

## Research Log Template

Use this template for signal research notes.

## Signal Research Entry

### Console Information

- PS2 model:
- Board revision:
- Region:
- Optical-drive assembly:
- Laser model:
- Driver IC marking:
- DSP marking:
- Other mods installed:

### Signal Information

- Signal name:
- Temporary name:
- Measurement point:
- IC or connector:
- Pin or pad:
- Ground reference:
- Tool used:
- Probe type:

### Test Condition

- Disc type:
- Disc condition:
- Console state:
- Power supply:
- Test duration:

### Observed Behavior

- Voltage range:
- Frequency or activity:
- Startup behavior:
- No-disc behavior:
- Read behavior:
- Failed-read behavior:
- Notes:

### Safety Notes

- Did probing affect operation:
- Did the signal appear sensitive:
- Any abnormal heat:
- Any abnormal current:
- Risk level:

### Conclusion

- Safe to monitor:
- Needs buffering:
- Needs level shifting:
- Useful for flatline detection:
- Useful for logging:
- Follow-up needed:

---

## Current Open Questions

Current open signal research questions:

- Which focus coil signals are the best to monitor?
- Which tracking coil signals are the best to monitor?
- Should coil signals be measured differentially?
- What is the safest way to condition coil activity for ESP32 logging?
- What is the safest current-sense method at PS11?
- What current range should be expected through PS11?
- What voltage drop at PS11 is acceptable?
- What signals best indicate expected drive activity?
- What signals should be ignored during startup?
- What signals change during failed reads?
- What signals are different between PS2 board revisions?
- What signals should never be connected to Layzr Savre hardware?
- What signals can eventually support active protection?

---

## Early Conclusions

Early conclusions should be conservative.

Current working assumptions:

- PS11 is a physical fuse that provides power to the driver IC in the area being studied.
- PS11 current monitoring is only a measurement idea at this stage.
- Focus and tracking coil activity may be useful for detecting abnormal behavior.
- Coil activity alone may not be enough to prove a dangerous condition.
- Current alone may not be enough to prove a dangerous condition.
- Board revisions may behave differently.
- Passive monitoring should come before active protection.
- ESP32 logging should come before ESP32-controlled cutoff.
- The project needs real test data before protection claims can be made.

---

## Summary

Signal research is one of the most important parts of the Layzr Savre project.

Before Layzr Savre can become a protection system, it must first become a good measurement and documentation system.

The project should identify useful signals, monitor them safely, collect real data, compare normal and abnormal behavior, and document board-revision differences.

Only after that should the project move toward flatline detection and active cutoff behavior.
