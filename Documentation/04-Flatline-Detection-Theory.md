# Flatline Detection Theory

**Project:** PS2 Layzr Savre  
**Owner:** FatBaldDad  
**Status:** Early research / planning / prototype development  
**Document:** 04 - Flatline Detection Theory  

---

## Overview

Flatline detection is one of the main research goals of the PS2 Layzr Savre project.

The idea is to monitor optical-drive activity and look for conditions where a signal, coil drive, or driver behavior becomes stuck, inactive, or abnormal when activity is expected.

In simple terms, Layzr Savre is trying to answer this question:

Can the PS2 optical-drive system be monitored well enough to detect a dangerous stuck or flatline condition before damage occurs?

At this stage, flatline detection is only a theory and research goal. It has not yet been validated as a finished protection method.

---

## Purpose of This Document

This document explains the current theory behind flatline detection for Layzr Savre.

It is intended to define:

- What flatline detection means in this project.
- Which signals may be useful.
- Why simple detection is not enough.
- Why timing matters.
- Why current monitoring may help.
- Why multiple signals should be compared.
- Why passive data collection must happen before active protection.
- What must be proven before Layzr Savre can cut power safely.

This document should be updated as real test data is collected.

---

## What Flatline Means in This Project

In the Layzr Savre project, a flatline condition generally means that a signal or drive output stops behaving dynamically when activity is expected.

This may include:

- A coil-drive signal that becomes stuck high.
- A coil-drive signal that becomes stuck low.
- A coil-drive signal that stops changing.
- A driver IC output that appears inactive when activity should be present.
- A focus or tracking signal that loses expected movement.
- A current path that shows abnormal sustained current.
- A repeated read failure where the drive keeps trying without normal recovery behavior.

A flatline does not automatically mean damage is occurring.

A flatline-like signal must be interpreted in context.

---

## Important Warning

Flatline detection should not be trusted until real test data proves what normal and abnormal behavior look like.

Normal PS2 optical-drive behavior may include short pauses, idle states, no-disc states, read retries, focus searching, disc spin-up, disc spin-down, and other conditions that may look like low activity or no activity for short periods.

A protection system that reacts too quickly may false-trigger during normal operation.

A protection system that reacts too slowly may not protect anything.

The goal is to find the correct balance through measurement.

---

## Flatline Detection Goal

The goal of flatline detection is to identify a sustained abnormal condition where the optical-drive system may be stressing the laser, focusing coils, tracking coils, driver IC, or related circuitry.

A useful flatline detector should:

- Ignore normal startup behavior.
- Ignore normal disc-detection behavior.
- Ignore short pauses.
- Ignore short glitches.
- Ignore normal no-disc behavior.
- Detect sustained abnormal behavior.
- Use more than one signal where possible.
- Consider current behavior.
- Consider timing.
- Avoid false triggers.
- Trigger only when a fault is likely enough to justify protection action.

---

## What Flatline Detection Is Not

Flatline detection is not:

- A simple single-signal check.
- A guarantee that a laser will be protected.
- A replacement for proper laser adjustment.
- A replacement for optical-drive maintenance.
- A way to make a bad laser read discs.
- A universal repair method.
- A proven protection system at this stage.
- A reason to skip testing.
- A reason to assume every PS2 board revision behaves the same.

---

## Why This Matters

The PS2 optical-drive system may continue trying to read a disc even when the read is failing.

If the control system keeps driving the optical-drive hardware during a bad condition, there may be stress on:

- Focus coils.
- Tracking coils.
- Driver IC outputs.
- Driver IC power path.
- Laser-related control circuitry.
- Optical pickup.
- Power fuses.
- Related motherboard circuitry.

Layzr Savre is being developed to study whether these conditions can be detected early enough to take protective action.

---

## Signals That May Be Useful

Flatline detection may eventually use several types of monitored data.

Possible useful signals include:

| Signal Area | Possible Use |
|---|---|
| Focus coil activity | Detect whether focus movement is dynamic, missing, or stuck |
| Tracking coil activity | Detect whether tracking correction is dynamic, missing, or stuck |
| Driver IC outputs | Observe whether output behavior appears normal or abnormal |
| PS11 current | Monitor current through the fuse path feeding the driver IC |
| Driver IC supply voltage | Detect voltage sag or abnormal power behavior |
| Optical-drive state timing | Separate normal behavior from abnormal behavior |
| ESP32 event timing | Track how long a condition has been present |
| Optional console UART data | Add context if useful and available |

No single signal should be treated as enough proof by itself during early development.

---

## PS11 Current Role

PS11 is a physical fuse on the PS2 motherboard that provides power to the driver IC.

For Layzr Savre, the current plan is to lift one side of the PS11 fuse and use that fuse location as a current-monitoring point.

The goal is to measure current through the PS11 fuse path during different optical-drive conditions.

PS11 current may help support flatline detection, but it should not be treated as the entire fault-detection system.

Important points:

- PS11 is a fuse.
- PS11 feeds the driver IC in the area being studied.
- PS11 does not represent the entire optical-drive system by itself.
- PS11 current does not represent every laser-control signal.
- PS11 current alone should not be treated as proof of a dangerous condition.
- PS11 current may help confirm whether the driver IC is drawing abnormal current during a suspected fault.
- The original protective function of the fuse must be preserved.

---

## Focus Coil Activity

The focus coils move the optical pickup lens up and down to keep the laser beam focused on the disc.

During normal operation, the focus system may show activity during:

- Startup.
- Disc detection.
- Focus search.
- Disc spin-up.
- Initial read.
- Normal read.
- Read retries.
- Failed reads.

A possible focus-related flatline concern may exist if focus activity becomes stuck, missing, or abnormal during a time when focus correction should be happening.

Possible focus-related abnormal behavior:

- No focus activity during expected focus search.
- Focus output stuck high.
- Focus output stuck low.
- Focus activity stops while current remains abnormal.
- Focus activity remains excessive for too long.
- Focus behavior does not recover after a failed read.

These behaviors need to be measured before they can be used for detection.

---

## Tracking Coil Activity

The tracking coils move the optical pickup lens side to side to keep the laser aligned with the disc track.

During normal operation, the tracking system may show activity during:

- Initial read.
- Seeking.
- Normal game loading.
- Error correction.
- Read retries.
- Recovery from poor reads.
- Failed reads.

A possible tracking-related flatline concern may exist if tracking activity becomes stuck, missing, or abnormal during a time when tracking correction should be happening.

Possible tracking-related abnormal behavior:

- No tracking activity during expected read activity.
- Tracking output stuck high.
- Tracking output stuck low.
- Tracking activity disappears during a failed read.
- Tracking activity remains excessive for too long.
- Tracking behavior does not recover after retries.

These behaviors need to be measured before they can be used for detection.

---

## Driver IC Output Behavior

The driver IC controls outputs related to optical-drive movement and coil drive, depending on the board revision and circuit design.

Flatline detection may use driver IC output behavior as one data source.

Possible driver IC concerns:

- Output stuck high.
- Output stuck low.
- Output inactive during expected activity.
- Output active too long.
- Output behavior changes when the drive fails to read.
- Output behavior differs between good and weak lasers.
- Output behavior differs between board revisions.

Driver IC outputs should be treated carefully because they may be analog, dynamic, differential, or sensitive to loading.

---

## Normal Behavior That May Look Like Flatline

A major problem with flatline detection is that some normal behavior may look inactive or flat for short periods.

Examples include:

- No disc inserted.
- Browser idle state.
- Startup delay before disc detection.
- Lid open or tray open state.
- Disc spin-down.
- Pauses between read attempts.
- Disc type detection.
- Switching from CD behavior to DVD behavior.
- Short read retry pauses.
- Game loading transitions.
- Console waiting for the drive to respond.

Flatline detection must not treat every quiet period as a fault.

---

## Abnormal Behavior to Research

The project should collect data from abnormal or suspicious conditions.

Possible abnormal conditions to research:

- Weak laser.
- Dirty lens.
- Scratched disc.
- Dirty disc.
- Bad ribbon cable.
- Poor ribbon cable seating.
- Failed focus search.
- Failed tracking recovery.
- Repeated read retries.
- Disc spins but does not read.
- Disc does not spin.
- Optical pickup stuck at home position.
- Sled binding.
- Driver IC heating.
- PS11 current higher than normal.
- PS11 current lower than expected.
- Coil activity missing during expected operation.
- Coil activity stuck during failure.

Each condition should be logged and compared against known-good behavior.

---

## Detection Inputs

A future flatline detector may use multiple inputs.

Possible inputs:

| Input | Description |
|---|---|
| FOCUS_ACTIVITY | Indicates whether focus coil behavior is changing |
| TRACK_ACTIVITY | Indicates whether tracking coil behavior is changing |
| PS11_CURRENT | Current through the PS11 fuse path |
| DRIVER_VCC | Driver IC supply voltage |
| DRIVE_STATE_TIMER | Time since drive activity started |
| FAULT_TIMER | Time a suspected fault has been present |
| STARTUP_IGNORE_TIMER | Time window to ignore startup behavior |
| RETRY_IGNORE_TIMER | Time window to ignore normal retry pauses |
| MANUAL_RESET | User or firmware reset after fault |
| FAULT_LATCH | Latched fault state after detection |

These names are placeholders and should be refined during firmware development.

---

## Signal Conditioning Concept

Raw coil signals may not be safe or useful to feed directly into an ESP32.

The signals may need conditioning before logging or detection.

Possible conditioning methods:

- High-impedance buffer.
- Differential amplifier.
- Comparator.
- RC filter.
- Peak detector.
- Envelope detector.
- Protection resistor.
- Clamp diode.
- Level shifting.
- Isolation buffer.
- External ADC.
- Current-sense amplifier.

The correct method depends on the signal being measured.

Early prototypes should focus on measurement accuracy and low circuit loading.

---

## Activity Detection Concept

Instead of trying to fully decode every waveform, Layzr Savre may first detect whether activity is present.

A simple activity detector may look for:

- Signal changes over time.
- AC movement above a threshold.
- Difference between two coil lines.
- Pulse activity.
- Repeated movement.
- Variation over a time window.

This may be easier than trying to interpret the full optical-drive control system.

However, activity detection alone may not be enough to declare a fault.

---

## Current-Based Detection Concept

PS11 current may be useful as a supporting signal.

Possible current-based observations:

- Normal current range during startup.
- Normal current range during focus search.
- Normal current range during disc read.
- Normal current range during failed read.
- Current spike during abnormal behavior.
- Sustained high current.
- Sustained current with no coil activity.
- Current behavior that differs between good and weak drives.

Current data may help confirm that the driver IC is still being powered and drawing current during a suspected signal flatline.

Current should not be used alone as the only trigger.

---

## Multi-Signal Confirmation

A safer detection method should require more than one condition before declaring a fault.

Example theory:

- Focus or tracking activity is missing.
- PS11 current is still present or abnormal.
- The condition lasts longer than a defined time.
- The console is past the startup ignore period.
- The condition is not part of a known no-disc or idle state.

Only then would Layzr Savre consider the condition suspicious.

A possible future detection rule may look like this in plain language:

If coil activity is missing or stuck while the driver IC is still drawing current, and this condition lasts longer than the allowed time window during expected drive activity, then latch a fault.

This rule is only a theory and must be tested.

---

## Timing Windows

Timing is important because normal behavior changes quickly.

Possible timing windows:

| Timing Window | Purpose |
|---|---|
| Startup ignore window | Prevent false triggers during console boot |
| Disc detection window | Prevent false triggers while the console checks for a disc |
| Focus search window | Allow normal focus attempts before declaring a fault |
| Retry window | Allow normal read retries |
| Fault confirmation window | Require the fault to remain present long enough to be trusted |
| Fault latch duration | Keep the fault state active until reset |
| Recovery window | Allow safe recovery after a fault clears |

These values cannot be guessed. They must be based on measured data.

---

## Possible Detection States

A future firmware state machine may use states similar to these:

| State | Description |
|---|---|
| BOOT | ESP32 is starting and should not control anything |
| IDLE | No active detection is running |
| STARTUP_IGNORE | Console has just powered on, ignore normal startup behavior |
| MONITORING | Signals are being watched |
| ACTIVITY_PRESENT | Coil or driver activity appears normal |
| ACTIVITY_MISSING | Expected activity appears missing |
| CURRENT_ABNORMAL | PS11 current is outside expected range |
| SUSPECT_FAULT | A possible fault has been detected but not confirmed |
| CONFIRMED_FAULT | Fault timing and conditions have been met |
| PROTECTION_ACTIVE | Future cutoff or fault response is active |
| FAULT_LATCHED | Fault remains latched until reset or power cycle |
| RECOVERY | System is returning from fault state |

The first firmware versions should log these states before controlling hardware.

---

## Possible Fault Types

Future firmware may classify faults instead of using one generic fault.

Possible fault types:

| Fault Type | Description |
|---|---|
| FOCUS_STUCK_HIGH | Focus signal appears stuck high |
| FOCUS_STUCK_LOW | Focus signal appears stuck low |
| FOCUS_NO_ACTIVITY | Focus activity is missing when expected |
| TRACK_STUCK_HIGH | Tracking signal appears stuck high |
| TRACK_STUCK_LOW | Tracking signal appears stuck low |
| TRACK_NO_ACTIVITY | Tracking activity is missing when expected |
| PS11_OVERCURRENT | Current through PS11 is above expected range |
| PS11_UNDERRANGE | Current through PS11 is below expected range during expected activity |
| DRIVER_POWER_FAULT | Driver IC supply behavior appears abnormal |
| MULTI_SIGNAL_FAULT | Multiple monitored conditions suggest a fault |
| UNKNOWN_FAULT | Fault detected but not classified |

These names are placeholders.

---

## False Trigger Risk

False triggers are a major risk.

A false trigger could:

- Stop the drive during normal operation.
- Cause failed reads.
- Interrupt game loading.
- Confuse troubleshooting.
- Create customer support problems.
- Make the kit seem unreliable.
- Possibly stress the drive if cutoff behavior is poorly designed.

Avoiding false triggers is just as important as detecting real faults.

---

## Missed Fault Risk

A missed fault is also a major risk.

A missed fault could:

- Allow unsafe behavior to continue.
- Fail to protect the driver IC or coils.
- Fail to protect the laser-related system.
- Make the protection feature ineffective.
- Create false confidence in the kit.

The system must be tested against real fault conditions before protection claims are made.

---

## Protection Action Theory

A future version of Layzr Savre may take action after a confirmed fault.

Possible protection actions:

- Log the fault only.
- Light a fault LED.
- Send fault status to the ESP32 interface.
- Stop logging and latch the event.
- Cut power to the driver IC path being monitored.
- Cut power to the coil-driver path.
- Request or trigger a safe shutdown, if a safe method is found.
- Require manual reset before restoring normal operation.

The first confirmed-fault behavior should probably be logging only.

Active cutoff should come later.

---

## Cutoff Theory

A future active protection version may cut power after a confirmed fault.

This must be researched carefully.

Cutoff questions:

- What exact power path should be cut?
- Should the cutoff happen at the PS11 fuse path or elsewhere?
- Does cutting that path stop the unsafe behavior?
- Does cutting that path create a partial power condition?
- Does cutting that path stress the driver IC?
- Does cutting that path affect other systems?
- Can the console recover cleanly?
- Should the fault latch until power cycle?
- Should the user be able to reset the fault?
- What happens if the ESP32 crashes during cutoff?
- What happens if the cutoff circuit fails?

Cutoff should not be implemented until passive monitoring and detection are validated.

---

## ESP32 Role in Detection

The ESP32 may be used for detection and logging, but it has limitations.

ESP32 concerns:

- Boot delay.
- GPIO boot states.
- Floating pins.
- ADC noise.
- ADC calibration.
- Limited sampling rate.
- Missed fast events.
- Brownout behavior.
- Firmware crash.
- Watchdog reset.
- Wi-Fi timing effects.
- Web interface delays.
- User configuration mistakes.

Because of this, the ESP32 should first be used to log data and test detection theory.

If the ESP32 eventually controls protection, the hardware should be designed so unsafe GPIO states do not create damage.

---

## Hardware Versus Firmware Detection

Flatline detection may be handled in hardware, firmware, or a combination of both.

### Hardware Detection

Possible benefits:

- Fast response.
- Less dependent on firmware.
- Can be fail-safe if designed correctly.
- May catch events the ESP32 misses.

Possible downsides:

- Less flexible.
- Harder to tune.
- More parts.
- More board space.
- More risk if thresholds are wrong.

### Firmware Detection

Possible benefits:

- Easy to tune.
- Can log events.
- Can use multiple conditions.
- Can be updated.
- Can support different board profiles.

Possible downsides:

- Slower response.
- Depends on ESP32 boot state.
- Depends on firmware reliability.
- May miss fast events.
- ADC limitations may affect accuracy.

A hybrid approach may eventually be best.

---

## Detection Thresholds

Detection thresholds should not be guessed.

Thresholds should be based on measured behavior.

Possible thresholds:

- Minimum activity level.
- Maximum allowed inactive time.
- Current high limit.
- Current low limit.
- Voltage sag limit.
- Startup ignore time.
- Retry ignore time.
- Fault confirmation time.
- Recovery time.

Each threshold should be documented with the test data that supports it.

---

## Data Needed Before Detection Can Be Trusted

Before flatline detection can be trusted, the project needs data from:

- Known-good console.
- Known-good laser.
- Known-good PS2 DVD game.
- Known-good PS2 CD game.
- Known-good PS1 disc.
- Audio CD.
- DVD video.
- No-disc state.
- Dirty disc.
- Scratched disc.
- Weak laser.
- Failed read.
- Repeated retry behavior.
- Different board revisions.
- Different optical-drive assemblies.
- Different power supplies.

The more data the project has, the safer the detection logic can become.

---

## Test Procedure Concept

A basic flatline research test may follow this process:

1. Confirm the console works normally before modification.
2. Install passive monitoring hardware.
3. Confirm the console still works normally.
4. Capture focus coil behavior with no disc.
5. Capture tracking coil behavior with no disc.
6. Capture PS11 current with no disc.
7. Capture focus coil behavior with a known-good disc.
8. Capture tracking coil behavior with a known-good disc.
9. Capture PS11 current with a known-good disc.
10. Repeat with different disc types.
11. Repeat with a dirty or scratched disc.
12. Repeat with a weak or questionable laser.
13. Compare normal and abnormal data.
14. Identify possible detection thresholds.
15. Test thresholds in logging-only mode.
16. Only consider cutoff after false triggers are understood.

---

## Logging-Only Detection Mode

Before active protection is added, firmware should support a logging-only detection mode.

In logging-only mode, Layzr Savre may:

- Detect a suspected fault.
- Log the time of the suspected fault.
- Log signal state.
- Log PS11 current.
- Log voltage readings.
- Log fault duration.
- Show a warning.
- Avoid cutting power.

This allows the detection logic to be tested safely.

If the firmware falsely detects faults during normal operation, the logic can be improved before active cutoff is added.

---

## Fault Latching Theory

If active protection is added later, confirmed faults may need to latch.

A latched fault means the system stays in the fault state until a reset condition occurs.

Possible reset conditions:

- Console power cycle.
- ESP32 reset.
- Manual reset button.
- Web interface reset.
- Timed recovery, if proven safe.
- Service-mode override, if added.

Fault latching may help prevent rapid on/off cycling during a dangerous condition.

---

## Recovery Theory

Recovery behavior must be planned before active cutoff is added.

Important recovery questions:

- Should the driver IC power be restored automatically?
- Should the user need to power cycle the console?
- Should the fault remain latched?
- Should the web interface display the last fault?
- Should logs be saved before recovery?
- What if the fault happens again immediately?
- What if the console is stuck during recovery?
- What if the optical drive is still in a bad state?

Automatic recovery should be avoided until the behavior is understood.

---

## Board Revision Profiles

Different PS2 board revisions may need different detection settings.

A future firmware may use board profiles.

Possible board profile information:

- PS2 model.
- Board revision.
- Driver IC type.
- PS11 behavior.
- Focus signal type.
- Tracking signal type.
- Current range.
- Startup timing.
- Detection thresholds.
- Known limitations.

Board profiles should be based on test data, not guesses.

---

## Data File Suggestions

Flatline research data should be saved in a consistent format.

Suggested file name examples:

- SCPH75001-GH040-FOCUS-good_dvd-normal_read
- SCPH75001-GH040-TRACK-good_dvd-normal_read
- SCPH75001-GH040-PS11-current-good_dvd-normal_read
- SCPH75001-GH040-FOCUS-scratched_dvd-failed_read
- SCPH75001-GH040-TRACK-weak_laser-failed_read
- SCPH75001-GH040-PS11-current-weak_laser-failed_read

Each file should include notes explaining the test setup.

---

## Research Log Template

Use this template when documenting a possible flatline event.

## Flatline Research Entry

### Console Information

- PS2 model:
- Board revision:
- Region:
- Optical-drive assembly:
- Laser model:
- Driver IC marking:
- DSP marking:
- Other mods installed:

### Hardware Setup

- Layzr Savre hardware revision:
- Current-sense method:
- PS11 fuse lifted:
- Measurement point:
- Ground reference:
- Probe type:
- ESP32 firmware version:

### Test Condition

- Disc type:
- Disc condition:
- Console state:
- Power supply:
- Test duration:

### Observed Behavior

- Focus activity:
- Tracking activity:
- PS11 current:
- Driver IC voltage:
- Startup behavior:
- Read behavior:
- Failed-read behavior:
- Abnormal behavior observed:

### Suspected Fault

- Fault type:
- Time fault started:
- Duration:
- Was current abnormal:
- Was activity missing:
- Was signal stuck high:
- Was signal stuck low:
- Did the console recover:

### Conclusion

- Likely normal behavior:
- Likely abnormal behavior:
- Useful for detection:
- False trigger risk:
- Follow-up test needed:

---

## Open Questions

Current open questions for flatline detection:

- What does normal focus activity look like on each target board?
- What does normal tracking activity look like on each target board?
- How much quiet time is normal during startup?
- How much quiet time is normal during disc detection?
- How much quiet time is normal during read retries?
- What does PS11 current look like during normal reads?
- What does PS11 current look like during failed reads?
- What current value is abnormal?
- What activity level is abnormal?
- Can focus and tracking activity be reduced to a simple activity signal?
- Does current remain high during a dangerous flatline?
- Does current drop during harmless idle states?
- Can the system distinguish no-disc from fault?
- Can the system distinguish read retry from fault?
- Does behavior differ between CD and DVD media?
- Does behavior differ between PS1 and PS2 discs?
- Does behavior differ between PS2 board revisions?
- What cutoff method is safest if a fault is confirmed?

---

## Early Working Theory

The current working theory is:

- Focus and tracking coil activity may provide useful information about optical-drive behavior.
- A dangerous condition may appear as missing, stuck, or abnormal coil-drive activity.
- PS11 current may help show whether the driver IC is still drawing current during a suspected fault.
- Current alone is not enough to prove a fault.
- Coil activity alone is not enough to prove a fault.
- A safer detection system should use timing and multiple signals.
- Detection should begin in logging-only mode.
- Active cutoff should only be added after false triggers are understood.
- Board revision differences must be documented.

This theory must be tested.

---

## Development Rule

For Layzr Savre, the safest development rule is:

Observe first.  
Log second.  
Detect third.  
Cut power last.

---

## Summary

Flatline detection is the theory that Layzr Savre may be able to identify unsafe optical-drive behavior by watching focus activity, tracking activity, driver IC behavior, PS11 current, and timing.

At this stage, the theory is not proven.

The project must collect real data from normal and abnormal drive conditions before detection thresholds or protection behavior can be trusted.

The first flatline detection firmware should only log suspected faults.

Active power cutoff should come later, after the detection logic has been validated across real PS2 hardware.
