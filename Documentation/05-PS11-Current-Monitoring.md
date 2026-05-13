# PS11 Current Monitoring

**Project:** PS2 Layzr Savre  
**Owner:** FatBaldDad  
**Status:** Early research / planning / prototype development  
**Document:** 05 - PS11 Current Monitoring  

---

## Overview

PS11 current monitoring is one of the planned measurement areas for the PS2 Layzr Savre project.

PS11 is a physical fuse on the PS2 motherboard. In the area being studied, PS11 provides power to the driver IC.

The current plan is to lift one side of the PS11 fuse and use that fuse location as a current-monitoring point. By measuring the voltage drop across a known low-value current-sense path, Layzr Savre may be able to estimate the current flowing through the PS11 fuse path during different optical-drive conditions.

At this stage, PS11 current monitoring is only a measurement and research feature.

It should not yet be treated as a proven protection trigger.

---

## Purpose of This Document

This document explains the current plan for monitoring current through PS11.

It is intended to document:

- What PS11 is currently understood to be.
- What Layzr Savre plans to measure at PS11.
- What the project is not assuming about PS11.
- Why the fuse location may be useful for current monitoring.
- How current may be estimated using a shunt.
- What safety concerns must be considered.
- What questions still need to be answered.
- What test data should be collected.

This document should be updated as real measurements are taken.

---

## Current Known Information

Current working understanding:

- PS11 is a physical fuse on the PS2 motherboard.
- PS11 provides power to the driver IC in the optical-drive area being studied.
- The project plans to lift one side of PS11 for current-monitoring research.
- The current-monitoring point will be the PS11 fuse path.
- The measurement goal is to observe current through that fuse path during different drive conditions.
- PS11 current may become one useful data point for future fault detection.
- PS11 current alone should not be treated as proof of a fault.

---

## What PS11 Is

For this project, PS11 should be described as:

- A physical fuse.
- A board-level protection component.
- A power path feeding the driver IC.
- A possible current-monitoring location.

PS11 should not be described as:

- The entire optical-drive power system.
- The entire laser-control system.
- The entire servo system.
- A complete measurement of optical-drive health.
- A proven fault-detection point.
- A guaranteed protection trigger.

---

## Current Monitoring Goal

The goal is to measure current flowing through the PS11 fuse path.

This may help document how the driver IC current changes during different optical-drive states.

Useful states to compare may include:

- Console startup.
- No disc.
- Disc detection.
- Focus search.
- Disc spin-up.
- Normal PS2 DVD read.
- Normal PS2 CD read.
- Normal PS1 disc read.
- Audio CD read.
- DVD video read.
- Read retry behavior.
- Failed read behavior.
- Weak laser behavior.
- Dirty disc behavior.
- Scratched disc behavior.

The purpose is to collect data first, then decide later whether the data is useful for detection.

---

## Planned Physical Method

The current physical method being considered is:

1. Identify PS11 on the target PS2 motherboard.
2. Confirm that PS11 provides power to the driver IC.
3. Lift one side of the PS11 fuse.
4. Route the lifted fuse side through a known low-value current-sense path.
5. Measure the voltage drop across the current-sense path.
6. Use that measured voltage drop to estimate current.
7. Confirm that normal console operation is not affected.
8. Record current behavior during different optical-drive states.

This method should be tested carefully on sacrificial or non-critical boards first.

---

## Basic Current Calculation

If a known current-sense resistance is used, current can be estimated with Ohm's law.

Formula:

`I = V / R`

Where:

- `I` is the current through the PS11 fuse path.
- `V` is the voltage measured across the current-sense resistance.
- `R` is the known current-sense resistance.

Example:

If the current-sense resistance is `0.1 ohm` and the measured voltage across it is `0.05 V`, then the estimated current is:

`0.05 V / 0.1 ohm = 0.5 A`

This is only an example. The correct shunt value must be chosen after research and testing.

---

## Current-Sense Resistance Concerns

The current-sense resistance must be selected carefully.

If the value is too high:

- Too much voltage may be dropped.
- The driver IC may not receive proper voltage.
- Optical-drive behavior may change.
- The console may fail to read discs.
- The measurement circuit may create a new problem.

If the value is too low:

- The voltage drop may be difficult to measure.
- Noise may dominate the measurement.
- The ESP32 ADC may not have enough resolution.
- An amplifier may be required.

The best value must balance measurement accuracy with minimal effect on the PS2.

---

## Voltage Drop Concern

Adding a current-sense path at PS11 will introduce some voltage drop.

That voltage drop must be low enough that the driver IC still operates normally.

Important questions:

- What voltage normally appears across PS11?
- What voltage does the driver IC require?
- How much voltage drop can be added before behavior changes?
- Does voltage drop change during high current events?
- Does voltage drop affect focus or tracking behavior?
- Does voltage drop affect disc detection?
- Does voltage drop affect read reliability?

The current-monitoring circuit must not create the fault it is trying to observe.

---

## Preserving Fuse Protection

PS11 is a fuse, so the protection purpose of the fuse must be respected.

The current-monitoring method should not simply bypass the fuse protection.

Important safety goals:

- Do not remove protection without understanding the risk.
- Do not replace the fuse path with an unsafe wire.
- Do not use a shunt or wiring path that allows excessive current without protection.
- Do not defeat the original safety function of PS11.
- Do not create a path that prevents PS11 from opening during a fault.
- Do not use undersized wiring or traces that create a fire or heat risk.
- Do not use a current-sense resistor with an inadequate power rating.

The final design should preserve or replace the protective function in a controlled and documented way.

---

## Power Dissipation

The current-sense element will dissipate power.

Power can be estimated with:

`P = I x I x R`

Where:

- `P` is the power dissipated by the current-sense resistor.
- `I` is the current through the PS11 fuse path.
- `R` is the current-sense resistance.

The current-sense resistor must be rated high enough for the expected current and fault conditions.

A current-sense part that is too small may overheat, drift, fail open, fail short, or damage the board.

---

## Measurement Methods

Possible ways to measure current through the PS11 fuse path include:

- Measuring voltage across a low-value shunt with a multimeter.
- Measuring voltage across a low-value shunt with an oscilloscope.
- Using a current-sense amplifier.
- Using a differential amplifier.
- Using an external ADC.
- Feeding a conditioned signal into the ESP32.
- Logging current behavior over time.

The early research stage may begin with oscilloscope or multimeter measurements before the ESP32 is involved.

---

## ESP32 Measurement Concerns

The ESP32 may eventually log PS11 current, but the signal must be conditioned properly.

ESP32 concerns include:

- ADC accuracy limitations.
- ADC noise.
- Input voltage limits.
- Ground reference quality.
- Sampling speed.
- Calibration.
- Brownout behavior.
- Wi-Fi noise.
- Boot-time pin states.
- Backfeeding risk.

The ESP32 should not be connected directly to the PS11 fuse path without proper conditioning and protection.

---

## Current-Sense Amplifier Consideration

A current-sense amplifier may be useful if the voltage across the shunt is very small.

Possible benefits:

- Better measurement resolution.
- Differential measurement across the shunt.
- Reduced noise problems.
- Easier ESP32 ADC input scaling.
- Safer signal conditioning.

Possible concerns:

- Adds parts.
- Adds board space.
- Requires correct common-mode voltage range.
- Requires stable power.
- Can introduce offset error.
- Can be damaged by incorrect wiring.
- Must not affect the PS11 power path.

The correct amplifier should be selected only after the expected voltage and current range are known.

---

## High-Side Versus Low-Side Measurement

Since PS11 is a fuse in a power path, the measurement may behave like a high-side current measurement depending on the exact circuit.

High-side current monitoring measures current on the supply side of the load.

Possible benefits:

- Preserves the normal ground path.
- Measures current in the actual supply path.
- Usually better for detecting load current.

Possible concerns:

- Requires a current-sense amplifier that can handle the common-mode voltage.
- More complex than low-side measurement.
- Incorrect measurement design can inject noise or cause voltage drop.

The exact measurement type should be determined after confirming the PS11 circuit location on the target board.

---

## What PS11 Current May Show

PS11 current may provide useful information about the driver IC load.

Possible useful observations:

- Current during startup.
- Current during disc detection.
- Current during focus search.
- Current during normal read.
- Current during failed read.
- Current during repeated retries.
- Current when the laser or optical pickup is weak.
- Current when the disc is dirty or scratched.
- Current when the drive mechanism is binding.
- Current when the driver IC behaves abnormally.

This information may help support future detection logic.

---

## What PS11 Current May Not Show

PS11 current may not show everything that matters.

PS11 current may not directly show:

- Laser diode health.
- Optical feedback quality.
- Exact focus position.
- Exact tracking position.
- Disc data quality.
- DSP internal state.
- Mechacon or Syscon decision-making.
- Every optical-drive power rail.
- Every possible drive fault.
- Every board-revision difference.

PS11 current is only one measurement point.

It should be used with other signals, such as focus activity, tracking activity, timing, voltage behavior, and test context.

---

## Possible Normal Current States

The project should eventually document current behavior during normal states.

Possible normal states to measure:

| State | Purpose |
|---|---|
| Power on | Check current behavior during console startup |
| Browser idle | Check behavior with no active disc read |
| No disc | Check baseline behavior |
| Disc detection | Check initial optical-drive activity |
| Focus search | Check driver IC current during focusing |
| Disc spin-up | Check current during early drive activity |
| Normal DVD read | Check PS2 DVD behavior |
| Normal CD read | Check PS2 CD behavior |
| Normal PS1 read | Check PS1 disc behavior |
| Audio CD read | Check audio CD behavior |
| DVD video read | Check DVD video behavior |
| Game loading | Check current during normal loading |
| Read retry | Check current during normal recovery attempts |

---

## Possible Abnormal Current States

The project should also document current behavior during abnormal states.

Possible abnormal states to measure:

| State | Purpose |
|---|---|
| Weak laser | Compare against known-good behavior |
| Dirty lens | Observe effect of poor optical feedback |
| Dirty disc | Observe read retry current behavior |
| Scratched disc | Observe difficult-read behavior |
| Failed read | Observe current during read failure |
| Repeated retries | Check sustained driver IC activity |
| Bad ribbon cable | Observe missing or unstable drive behavior |
| Mechanical binding | Observe current behavior during movement problems |
| Driver IC heat | Compare current against temperature behavior |
| Suspected flatline | Compare current with missing signal activity |

These tests should be performed carefully and with risk in mind.

---

## Relationship to Flatline Detection

PS11 current may help support flatline detection.

A possible future detection theory may be:

- Focus or tracking activity appears missing or stuck.
- PS11 current is still present or abnormal.
- The condition lasts longer than a safe timing window.
- The console is past startup and disc-detection ignore periods.
- Multiple signals agree that the behavior is suspicious.

This is only a theory.

PS11 current alone should not trigger protection until validated.

---

## Relationship to Coil Activity

Current monitoring should be compared with coil activity.

Useful comparisons:

- Current present while focus activity is normal.
- Current present while tracking activity is normal.
- Current present while focus activity is missing.
- Current present while tracking activity is missing.
- Current high while coil activity is stuck.
- Current low while expected activity is missing.
- Current changes during read retries.
- Current changes during failed reads.

These comparisons may help separate harmless idle behavior from possible unsafe behavior.

---

## Relationship to Driver IC Temperature

The driver IC may heat differently depending on current and load.

The project may eventually compare:

- PS11 current.
- Driver IC temperature.
- Focus coil activity.
- Tracking coil activity.
- Failed-read behavior.
- Long-duration testing.

Possible tools:

- Finger check with caution.
- Thermal camera.
- Temperature probe.
- Infrared thermometer.

Thermal testing should be done carefully.

---

## Measurement Safety

Before measuring PS11 current:

- Confirm the console works before modification.
- Confirm the board revision.
- Confirm PS11 location.
- Confirm which side of PS11 is input and output.
- Confirm the fuse is not already open.
- Confirm no shorts are present.
- Confirm the current-sense path is connected correctly.
- Confirm the shunt value.
- Confirm the shunt power rating.
- Confirm the measurement ground reference.
- Confirm the measurement circuit cannot short the fuse path.
- Confirm wires are insulated and secured.
- Confirm the lifted fuse side is mechanically stable.

Do not power the console if the PS11 path is uncertain.

---

## Lifted Fuse Risks

Lifting one side of PS11 creates mechanical and electrical risks.

Possible risks:

- Breaking the fuse.
- Lifting the pad.
- Damaging the trace.
- Weak solder joint.
- Intermittent connection.
- Short to nearby components.
- Excessive wire strain.
- Bypassing the fuse accidentally.
- Incorrect current-sense routing.
- Reversing sense leads.
- Damaging the driver IC if the power path is unstable.

The lifted fuse should be supported mechanically and the wiring should be strain-relieved.

---

## Current-Sense Wiring Risks

Current-sense wiring should be short, secure, and insulated.

Long or poor wiring may cause:

- Added resistance.
- Added inductance.
- Noise pickup.
- Voltage drop.
- Mechanical stress.
- Intermittent power.
- Oscillation or instability.
- Incorrect measurement.
- Short circuits.

A future PCB should make the PS11 current-sense path as clean and reliable as possible.

---

## Test Equipment

Recommended equipment for PS11 current research:

- Multimeter.
- Oscilloscope.
- Differential probe, if available.
- Current-sense amplifier test board, if used.
- Known low-value shunt resistor.
- Magnification.
- Fine soldering tools.
- Flux.
- Insulated wire.
- Kapton tape or insulation.
- Thermal camera or temperature probe, if available.
- Known-good PS2 test discs.
- Sacrificial or non-critical PS2 console.

---

## Test Data to Record

Each PS11 current test should document:

- PS2 model.
- Motherboard revision.
- Region, if useful.
- Driver IC marking.
- Laser model, if known.
- Optical-drive assembly, if known.
- PS11 fuse rating, if known.
- Shunt resistance value.
- Shunt power rating.
- Measurement method.
- Measurement tool.
- Ground reference.
- Disc type.
- Disc condition.
- Test duration.
- Current range.
- Voltage drop across shunt.
- Console behavior.
- Driver IC temperature, if checked.
- Any abnormal behavior.

---

## PS11 Current Test Template

Use this template when documenting a PS11 current test.

## PS11 Current Test Entry

### Console Information

- PS2 model:
- Board revision:
- Region:
- Driver IC marking:
- DSP marking:
- Optical-drive assembly:
- Laser model:
- Other mods installed:

### PS11 Setup

- PS11 location confirmed:
- PS11 input side:
- PS11 output side:
- Fuse lifted:
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
- Shunt voltage during no-disc state:
- Shunt voltage during disc detection:
- Shunt voltage during focus search:
- Shunt voltage during normal read:
- Shunt voltage during failed read:
- Estimated current range:
- Driver IC temperature:
- Voltage drop concern:

### Observed Behavior

- Console booted normally:
- Disc detected:
- Disc read normally:
- Any read errors:
- Any abnormal sound:
- Any abnormal heat:
- Any instability:
- Did measurement affect operation:

### Conclusion

- Current behavior appears normal:
- Current behavior appears abnormal:
- Shunt value acceptable:
- Measurement method acceptable:
- Useful for future detection:
- Follow-up test needed:

---

## Suggested Data File Names

Suggested file naming format:

- PS2MODEL-BOARD-PS11-current-CONDITION-DATE
- SCPH75001-GH040-PS11-current-no_disc-2026-05-13
- SCPH75001-GH040-PS11-current-good_dvd-2026-05-13
- SCPH75001-GH040-PS11-current-failed_read-2026-05-13
- SCPH79001-GH061-PS11-current-startup-2026-05-13

Keep names simple, consistent, and searchable.

---

## Early Testing Procedure

Recommended early PS11 testing process:

1. Confirm the PS2 works normally before modification.
2. Identify the motherboard revision.
3. Locate PS11.
4. Confirm PS11 is not open.
5. Identify which side feeds the driver IC.
6. Lift one side of PS11 carefully.
7. Add the current-sense path.
8. Check continuity through the new path.
9. Check for shorts to ground.
10. Confirm the shunt value.
11. Confirm the measurement setup.
12. Power on without a disc.
13. Confirm normal console behavior.
14. Measure baseline current.
15. Test with a known-good disc.
16. Compare current during different states.
17. Stop testing if heat, instability, or abnormal behavior occurs.

---

## Stop Testing If

Stop testing immediately if:

- The console does not power on normally.
- PS11 area becomes hot.
- The shunt becomes hot.
- The driver IC becomes unusually hot.
- A fuse opens.
- There is a burning smell.
- The disc drive behaves abnormally.
- The console resets or locks up.
- The current is much higher than expected.
- The voltage drop is excessive.
- The measurement wiring moves or disconnects.
- A short is suspected.

Investigate before continuing.

---

## Open Questions

Current open questions:

- Which driver IC power input is fed by PS11?
- Does PS11 behavior vary by PS2 board revision?
- What is the expected current range through PS11?
- What is the safe maximum current through PS11?
- What shunt value provides useful measurement without affecting operation?
- What voltage drop is acceptable?
- Should the current sense be measured with a dedicated amplifier?
- Can the ESP32 ADC measure the current accurately enough?
- How noisy is the PS11 current signal?
- Does PS11 current change clearly during failed reads?
- Does PS11 current correlate with focus or tracking activity?
- Can PS11 current help confirm a flatline condition?
- How can the fuse protection be preserved in a final board design?
- Should the final kit use the original fuse, a replacement fuse, or a protected current-sense path?

---

## Development Notes

Current development notes:

- PS11 should be described as a physical fuse.
- One side of PS11 may be lifted for measurement.
- The measurement is across the current-sense path added at the PS11 location.
- The project is not assuming PS11 represents the entire optical-drive system.
- The project is not assuming PS11 current alone proves a fault.
- The fuse protection function must be respected.
- Current monitoring is for data collection first.
- Fault detection should use PS11 current only as one supporting signal.

---

## Future Hardware Goals

A future Layzr Savre hardware revision may include:

- Dedicated PS11 current-sense pads.
- Fuse-safe current path.
- Low-value shunt resistor footprint.
- Current-sense amplifier.
- Filtered analog output.
- ESP32 ADC input protection.
- Test pads for oscilloscope measurement.
- Clear PS11 input and output labels.
- Board-revision-specific install notes.
- Mechanical strain relief.
- Fuse protection or replacement protection.

These should be added only after the measurement method is tested.

---

## Future Firmware Goals

Future ESP32 firmware may use PS11 current data to:

- Log current over time.
- Display current in a web interface.
- Record current during fault events.
- Compare current against expected ranges.
- Support detection logic.
- Correlate current with focus and tracking activity.
- Warn when current appears abnormal.
- Store fault history.

Firmware should begin in logging-only mode.

---

## Summary

PS11 current monitoring is an important research area for Layzr Savre.

PS11 is a physical fuse that provides power to the driver IC in the area being studied. The current plan is to lift one side of the fuse and use that fuse location as a current-monitoring point.

The goal is to measure current through the PS11 fuse path during normal and abnormal optical-drive conditions.

At this stage, PS11 current monitoring is only for observation, logging, and research.

It should not be treated as a proven protection trigger until real test data shows how useful and reliable it is.
