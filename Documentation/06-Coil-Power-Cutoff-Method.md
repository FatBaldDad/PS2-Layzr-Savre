# Coil Power Cutoff Method

**Project:** PS2 Layzr Savre  
**Owner:** FatBaldDad  
**Status:** Early research / planning / prototype development  
**Document:** 06 - Coil Power Cutoff Method  

---

## Overview

Coil power cutoff is a future protection concept for the PS2 Layzr Savre project.

The goal is to eventually create a controlled method for stopping unsafe driver or coil activity when a confirmed fault condition is detected.

At this stage, the cutoff method is not finalized.

The project is currently focused on research, passive monitoring, PS11 current observation, signal logging, and flatline detection theory. Active cutoff should only be added after the project has enough test data to understand normal and abnormal optical-drive behavior.

---

## Purpose of This Document

This document explains the current thinking around future coil or driver power cutoff for Layzr Savre.

It is intended to document:

- Why a cutoff method may be useful.
- Why active cutoff is risky.
- What must be proven before cutoff is added.
- What power paths may be considered.
- Why PS11 should be treated carefully.
- What fail-safe behavior should look like.
- What testing must happen before active protection.
- What questions still need to be answered.

This document should be updated as real measurements and prototype results become available.

---

## Important Warning

Active cutoff is one of the riskiest parts of this project.

Cutting the wrong signal, cutting the wrong power path, cutting at the wrong time, or using an unsafe control circuit may damage the console or optical-drive system.

Possible damage may include:

- Driver IC damage
- Laser or optical pickup damage
- Focus or tracking coil problems
- Blown fuses
- Damaged traces or pads
- Console lockups
- Failed reads
- Partial power states
- Unexpected current paths
- Mechacon or Syscon issues
- Board-level damage

Active cutoff should not be tested on a valuable console first.

---

## Current Development Position

The current position of the project is:

- Passive monitoring comes first.
- PS11 current monitoring comes first.
- Coil activity logging comes first.
- ESP32 logging comes first.
- Flatline detection should start in logging-only mode.
- Active cutoff should come later.
- Cutoff should not be treated as proven until tested.
- The cutoff point should not be assumed until the circuit is verified.

The first hardware revision should not cut power.

---

## What Cutoff Means

In this project, cutoff means intentionally interrupting a power path or control path after a confirmed unsafe condition is detected.

A cutoff method may eventually be used to stop power to the driver IC path, coil-driver path, or another validated point in the optical-drive system.

Cutoff does not currently mean:

- Cutting random optical-drive signals.
- Cutting the laser diode directly without research.
- Cutting DSP signals.
- Cutting Mechacon or Syscon signals.
- Cutting motor signals without understanding the result.
- Pulling unknown control lines high or low.
- Bypassing the original fuse protection.
- Replacing proper repair or calibration.

---

## Why Cutoff May Be Useful

A future cutoff method may be useful if testing proves that certain failure conditions continue to stress the optical-drive system.

Possible conditions that may justify cutoff include:

- Focus coil output stuck high.
- Focus coil output stuck low.
- Tracking coil output stuck high.
- Tracking coil output stuck low.
- Missing coil activity while driver current remains abnormal.
- Sustained abnormal current through the PS11 fuse path.
- Driver IC overheating during a failed read condition.
- Repeated failed reads with abnormal signal behavior.
- Confirmed flatline behavior that does not recover normally.

These conditions must be verified with real measurements.

---

## What Must Be Proven First

Before any active cutoff method is trusted, the project must prove several things.

Required proof:

- Normal focus activity has been documented.
- Normal tracking activity has been documented.
- Normal PS11 current has been documented.
- Failed-read behavior has been documented.
- Flatline-like behavior has been documented.
- Detection logic has been tested in logging-only mode.
- False triggers have been studied.
- The cutoff point has been electrically verified.
- The cutoff method does not damage the console.
- The console can recover safely after a cutoff.
- Board-revision differences have been documented.

No cutoff method should be considered safe until these items are addressed.

---

## Cutoff Should Be a Last Step

Layzr Savre should follow this development order:

1. Observe signals.
2. Log data.
3. Compare normal and abnormal behavior.
4. Detect suspected faults in logging-only mode.
5. Validate detection logic.
6. Test cutoff on sacrificial hardware.
7. Validate recovery behavior.
8. Document supported board revisions.
9. Only then consider a kit-ready cutoff design.

The project should not start with power cutoff.

---

## Relationship to PS11

PS11 is a physical fuse on the PS2 motherboard.

For this project, PS11 is currently being treated as a fuse that provides power to the driver IC in the area being studied.

The current PS11 plan is to lift one side of the fuse and use that fuse location as a current-monitoring point.

Important notes:

- PS11 is a fuse.
- PS11 provides power to the driver IC in the area being studied.
- PS11 is currently a measurement point.
- PS11 should not automatically be treated as the final cutoff point.
- PS11 should not be assumed to represent the entire optical-drive power system.
- PS11 should not be assumed to represent the entire laser-control system.
- PS11 current alone should not trigger cutoff until validated.
- The protective function of PS11 must be preserved.

A future cutoff method may involve the PS11 path only if testing proves that it is safe and useful.

---

## Cutoff Point Research

The correct cutoff point is not yet confirmed.

Possible cutoff areas to research:

| Candidate Area | Purpose | Current Status |
|---|---|---|
| PS11 fuse path | Interrupt power feeding the driver IC area being studied | Research needed |
| Driver IC supply path | Interrupt driver IC power if safely isolated | Research needed |
| Coil-driver supply path | Interrupt only the coil-driver portion if identifiable | Research needed |
| Driver IC enable or mute control | Disable driver IC through an existing control input if safe | Research needed |
| External fault latch path | Use Layzr Savre hardware to latch a fault state | Future research |
| Console reset or shutdown request | Request safe shutdown if a safe method is found | Future research |

The safest point must be determined by measurement and board-revision research.

---

## Cutoff Method Candidates

Possible cutoff methods may include:

| Method | Possible Benefit | Possible Risk |
|---|---|---|
| MOSFET power switch | Fast, compact, solid-state control | Must be selected and driven correctly |
| Load switch IC | Integrated protection features may help | Must handle current, voltage, and fault behavior |
| Relay | Simple isolation and visible behavior | Large, slow, mechanical wear |
| Fuse-and-shunt path with controlled switch | Combines measurement and control | Must preserve fuse protection |
| Driver IC enable control | May be cleaner than cutting power if available | Must confirm the pin function and safe state |
| Fault latch circuit | Can keep protection active after fault | Must avoid false latching |
| Hardware comparator cutoff | Fast and independent of firmware | Thresholds may be hard to tune |
| ESP32-controlled cutoff | Flexible and loggable | Firmware and boot-state risks |

No method should be selected as final until tested.

---

## MOSFET Cutoff Concept

A MOSFET-based cutoff may eventually be useful for switching a driver IC power path.

Possible benefits:

- Fast response.
- Compact PCB footprint.
- No moving parts.
- Can be controlled by logic.
- Can be combined with fault-latch logic.

Possible concerns:

- Correct high-side or low-side design must be chosen.
- MOSFET must handle expected current.
- MOSFET must handle fault current.
- Gate must have a safe default state.
- Gate must not float.
- Body diode behavior must be considered.
- Heat dissipation must be checked.
- On-resistance must be low enough.
- The circuit must not create partial power paths.
- The circuit must not backfeed the PS2.

A MOSFET cutoff should be tested on sacrificial hardware before use in a working console.

---

## Load Switch Concept

A load switch IC may be useful if a dedicated protected switch is needed.

Possible benefits:

- Controlled turn-on and turn-off.
- Built-in current limit on some parts.
- Thermal protection on some parts.
- Small footprint.
- Logic input control.

Possible concerns:

- Current rating must be high enough.
- Voltage rating must match the PS2 circuit.
- On-resistance must be low enough.
- Fault behavior must be understood.
- Enable pin default state must be safe.
- Some load switches may not behave well with inductive or dynamic loads.
- The part must not interfere with normal driver IC operation.

A load switch should only be considered after current levels are measured.

---

## Relay Cutoff Concept

A relay may be useful for early bench testing because it provides simple physical isolation.

Possible benefits:

- Easy to understand.
- Clear open or closed state.
- Good isolation.
- Useful for proof-of-concept testing.

Possible concerns:

- Large size.
- Coil current draw.
- Slow switching.
- Contact bounce.
- Mechanical wear.
- Coil flyback protection required.
- May not fit a final kit.
- May be overkill for the final design.

A relay may be useful during early experiments but may not be ideal for a final product.

---

## Driver IC Enable or Mute Concept

Some driver ICs may have enable, mute, standby, or control pins.

If a safe control input exists, using it may be cleaner than cutting power.

Possible benefits:

- May avoid interrupting the power path.
- May allow cleaner shutdown of outputs.
- May reduce risk of partial power states.
- May be how the circuit was intended to be disabled.

Possible concerns:

- The pin function must be confirmed.
- The safe state must be confirmed.
- The pin may be controlled by another IC.
- Pulling it externally may fight the original circuit.
- Behavior may vary by board revision.
- It may disable more than intended.
- It may not respond fast enough.
- It may not stop the dangerous condition.

No enable or mute pin should be driven until the circuit is fully understood.

---

## Hardware Comparator Concept

A hardware comparator may eventually detect activity or current thresholds without relying fully on firmware.

Possible benefits:

- Fast reaction.
- Can work even if firmware is slow.
- Can create a simple fault signal.
- Can support a hardware fault latch.

Possible concerns:

- Thresholds must be correct.
- Noise can cause false triggers.
- Filtering may add delay.
- Different board revisions may need different thresholds.
- Comparator output still needs safe control logic.
- It may not understand console state.

A comparator may be useful as part of a hybrid hardware and firmware detection system.

---

## ESP32-Controlled Cutoff Concept

The ESP32 may eventually control the cutoff circuit after detecting a confirmed fault.

Possible benefits:

- Flexible thresholds.
- Logs the event.
- Can support board profiles.
- Can use multiple signals.
- Can provide a web interface.
- Can support manual reset or service mode.

Possible concerns:

- ESP32 boot delay.
- GPIO boot states.
- Firmware crashes.
- Watchdog resets.
- Brownout behavior.
- Wi-Fi timing effects.
- User configuration mistakes.
- Missed fast events.
- Unsafe default pin states.

The cutoff hardware must be safe even when the ESP32 is not ready.

---

## Safe Default State

The cutoff circuit must have a safe default state.

The project must decide what safe means for each design stage.

For a development prototype, safe may mean:

- If the ESP32 is off, the PS2 behaves normally.
- If the ESP32 crashes, the cutoff does not randomly trigger.
- If a signal wire disconnects, the console does not enter an unsafe state.
- If the cutoff control floats, the power path remains in a known state.

For a final protection device, safe may mean:

- If a confirmed fault is latched, the driver path is disabled.
- If the protection circuit loses power, it fails in the least dangerous state.
- If firmware fails, hardware prevents unsafe switching.
- If installed incorrectly, damage risk is minimized where possible.

This must be defined and tested.

---

## Normally-On Versus Normally-Off

The cutoff circuit may be designed as normally-on or normally-off.

### Normally-On Concept

The PS2 driver path is connected by default and Layzr Savre opens the path only during a confirmed fault.

Possible benefit:

- Console works normally if Layzr Savre is inactive.
- Easier for passive and early logging prototypes.
- Less risk from ESP32 boot delay.

Possible concern:

- If Layzr Savre fails completely, it may not protect anything.

### Normally-Off Concept

The PS2 driver path is disconnected until Layzr Savre allows it to turn on.

Possible benefit:

- More control over when the driver path is enabled.
- Could be safer if the protection circuit is fully trusted.

Possible concern:

- ESP32 boot delay may prevent normal console startup.
- Firmware fault may stop normal operation.
- False lockout may create support issues.
- More complex to design safely.

Early prototypes should likely avoid normally-off behavior.

---

## Fault Latching

A future cutoff system should probably latch confirmed faults.

Fault latching means that once a confirmed fault occurs, the protection state remains active until reset.

Possible reset methods:

- Power cycle.
- Manual reset button.
- ESP32 reset command.
- Web interface reset.
- Service-mode reset.
- Timed recovery, if proven safe.

Fault latching may help prevent rapid on/off cycling during a bad condition.

Automatic recovery should be avoided until tested.

---

## Fault Indicator

A future cutoff board should include a way to show that a fault occurred.

Possible indicators:

- Fault LED.
- ESP32 web interface fault message.
- Serial log message.
- Stored fault history.
- Optional buzzer or warning output.
- Test pad for fault status.
- Dedicated fault output pin.

A fault indicator helps with troubleshooting and prevents confusion after a cutoff event.

---

## Recovery Behavior

Recovery behavior must be planned carefully.

Important questions:

- Does the console need a full power cycle after cutoff?
- Can the driver IC path be safely restored?
- Should the fault stay latched?
- Should the user remove the disc before reset?
- Should the ESP32 save logs before reset?
- What happens if the same fault returns immediately?
- What happens if the optical drive is still mechanically stuck?
- What happens if the PS2 is frozen after cutoff?

A safe recovery method is as important as the cutoff method itself.

---

## Avoiding Partial Power States

A partial power state can happen when part of a circuit is powered while another related part is unpowered.

Partial power states can create unexpected current paths through signal pins, protection diodes, or IC inputs.

Cutoff design must consider:

- Driver IC supply voltage.
- Driver IC input signals.
- DSP outputs.
- Coil outputs.
- Motor outputs.
- Pull-up and pull-down paths.
- ESD diode paths.
- ESP32 input and output paths.
- Measurement circuit power.
- Backfeeding through signal conditioners.

The cutoff circuit should not create a worse condition than the fault it is trying to stop.

---

## Preserving Fuse Protection

If the cutoff circuit interacts with the PS11 fuse path, the fuse protection must be preserved.

The design should avoid:

- Bypassing PS11 with an unprotected wire.
- Replacing the fuse with an unsafe current path.
- Using traces or wires that cannot handle fault current.
- Hiding a fault condition from the original protection circuit.
- Creating a path that prevents the fuse from opening.
- Using a shunt or switch without proper power rating.

The final design may need a protected current-sense and switching path that respects the original fuse function.

---

## Detection Before Cutoff

The cutoff circuit should not operate from a single raw signal.

A future cutoff decision should likely consider:

- Focus activity.
- Tracking activity.
- PS11 current.
- Timing.
- Startup ignore window.
- Disc-detection ignore window.
- Fault confirmation window.
- Possibly driver IC voltage.
- Possibly board-revision profile.
- Possibly user configuration.

The project should start with logging-only detection before active cutoff.

---

## Logging-Only Cutoff Simulation

Before real cutoff is enabled, firmware should support a simulation mode.

In simulation mode:

- The system detects a suspected fault.
- The system logs that cutoff would have happened.
- The system records signal states.
- The system records PS11 current.
- The system records timing.
- The system does not actually cut power.

This helps find false triggers before hardware control is enabled.

---

## Cutoff Enable Jumper

A development board may include a physical jumper or solder bridge that enables active cutoff.

Possible behavior:

- Default state: cutoff disabled.
- Logging and detection still work.
- Active cutoff only works when the jumper is installed.
- Testers must intentionally enable active protection.
- Documentation can clearly separate monitoring from control.

This may reduce risk during early testing.

---

## Manual Override

A future board may need a manual override or service mode.

Possible uses:

- Disable active cutoff for testing.
- Force logging-only mode.
- Clear a latched fault.
- Allow normal console testing.
- Recover from false trigger conditions.

Manual override must be documented clearly so users understand the risk.

---

## Hardware Revision Strategy

Cutoff should be added in stages.

Suggested hardware revisions:

| Version | Purpose |
|---|---|
| v0.1 | Passive monitoring only |
| v0.2 | ESP32 logging only |
| v0.3 | PS11 current monitoring |
| v0.4 | Flatline detection in logging-only mode |
| v0.5 | Cutoff circuit present but disabled by default |
| v0.6 | Controlled cutoff testing on sacrificial boards |
| v0.7 | Integrated protection prototype |
| v0.8 | Validation prototype |
| v0.9 | Beta kit |
| v1.0 | Public kit, only after validation |

The first cutoff-capable board should still default to safe monitoring behavior.

---

## Firmware Revision Strategy

Firmware should also be staged.

Suggested firmware stages:

| Firmware Stage | Purpose |
|---|---|
| Logger v0.1 | Log raw or conditioned signals |
| Logger v0.2 | Add PS11 current logging |
| Detection v0.1 | Detect suspected faults but only log them |
| Detection v0.2 | Add timing windows and false-trigger filters |
| Cutoff Test v0.1 | Simulate cutoff events |
| Cutoff Test v0.2 | Enable hardware cutoff only with physical jumper |
| Protection Beta v0.1 | Test active cutoff with trusted testers |
| Release v1.0 | Stable behavior after validation |

Firmware should never enable active cutoff by accident.

---

## Cutoff Test Procedure Concept

A basic cutoff research procedure may look like this:

1. Confirm the console works normally before modification.
2. Install passive monitoring hardware.
3. Confirm the console still works normally.
4. Add PS11 current monitoring.
5. Confirm current monitoring does not affect normal operation.
6. Collect normal focus, tracking, and current data.
7. Collect failed-read data.
8. Test detection logic in logging-only mode.
9. Confirm false triggers are not happening.
10. Install cutoff-capable hardware with cutoff disabled.
11. Confirm normal operation.
12. Enable cutoff only on sacrificial hardware.
13. Trigger a controlled test condition.
14. Confirm the cutoff activates correctly.
15. Confirm no overheating or damage occurs.
16. Confirm recovery behavior.
17. Repeat across different conditions.
18. Document every result.

---

## Active Cutoff Test Requirements

Before active cutoff testing:

- Use a sacrificial or non-critical console.
- Confirm board revision.
- Confirm driver IC marking.
- Confirm PS11 path.
- Confirm cutoff circuit wiring.
- Confirm current-sense wiring.
- Confirm no shorts.
- Confirm cutoff disabled by default.
- Confirm manual disable works.
- Confirm fault indicator works.
- Confirm ESP32 firmware version.
- Confirm detection settings.
- Confirm logs are working.
- Confirm power supply is stable.
- Confirm a known-good disc reads normally before testing.

Do not enable cutoff until the basic system works.

---

## Stop Testing If

Stop testing immediately if:

- The console does not power on normally.
- The optical drive behaves abnormally.
- The disc does not spin normally.
- The driver IC becomes unusually hot.
- The PS11 area becomes hot.
- The cutoff switch becomes hot.
- The shunt becomes hot.
- The ESP32 resets unexpectedly.
- The console resets repeatedly.
- The console locks up.
- The fault triggers repeatedly without cause.
- The cutoff chatters or cycles rapidly.
- Current draw is much higher than expected.
- Voltage drop is excessive.
- Smoke or burning smell occurs.

Investigate before continuing.

---

## Cutoff Data to Record

Each cutoff test should document:

- PS2 model.
- Board revision.
- Driver IC marking.
- Laser model, if known.
- Optical-drive assembly, if known.
- Layzr Savre hardware revision.
- Firmware revision.
- Cutoff circuit type.
- Cutoff point.
- PS11 current-sense method.
- Fault condition tested.
- Detection settings.
- Timing settings.
- Current before cutoff.
- Current after cutoff.
- Voltage before cutoff.
- Voltage after cutoff.
- Console behavior after cutoff.
- Recovery behavior.
- Driver IC temperature.
- Any abnormal behavior.
- Whether the test was repeated.

---

## Cutoff Test Template

Use this template when documenting a cutoff test.

## Coil Power Cutoff Test Entry

### Console Information

- PS2 model:
- Board revision:
- Region:
- Driver IC marking:
- DSP marking:
- Optical-drive assembly:
- Laser model:
- Other mods installed:

### Layzr Savre Setup

- Hardware revision:
- Firmware revision:
- Cutoff method:
- Cutoff point:
- PS11 current monitoring installed:
- Current-sense value:
- Fault indicator:
- Manual override:
- Cutoff enable jumper installed:

### Test Condition

- Disc type:
- Disc condition:
- Console state:
- Power supply:
- Test duration:
- Fault condition being tested:

### Detection Settings

- Startup ignore time:
- Disc detection ignore time:
- Fault confirmation time:
- Current threshold:
- Activity threshold:
- Fault latch enabled:
- Recovery mode:

### Measurements

- PS11 current before fault:
- PS11 current during fault:
- PS11 current after cutoff:
- Driver IC voltage before cutoff:
- Driver IC voltage after cutoff:
- Driver IC temperature:
- Cutoff switch temperature:
- Voltage drop across cutoff path:

### Observed Behavior

- Fault detected:
- Cutoff activated:
- False trigger:
- Console froze:
- Console recovered:
- Disc read after recovery:
- Abnormal sound:
- Abnormal heat:
- Notes:

### Conclusion

- Cutoff method appears safe:
- Cutoff method needs changes:
- Detection settings need changes:
- Recovery behavior acceptable:
- Follow-up test needed:

---

## Open Questions

Current open questions:

- What is the safest cutoff point?
- Should cutoff happen at the PS11 path or somewhere else?
- Does cutting PS11 stop the unsafe behavior being studied?
- Does cutting PS11 create a partial power state?
- Does the driver IC have a safe enable or mute input?
- Does cutoff need to happen quickly, or is a delayed response acceptable?
- What current level is abnormal?
- What signal condition confirms a real fault?
- How long should a suspected fault exist before cutoff?
- Should cutoff latch until power cycle?
- Can the console recover cleanly after cutoff?
- Does cutoff behavior differ by board revision?
- What hardware method is most fail-safe?
- What happens if the ESP32 crashes?
- What happens if the cutoff control wire disconnects?
- What happens if the current-sense circuit fails?
- How should a beta tester safely enable or disable cutoff?

---

## Current Working Theory

The current working theory is:

- A dangerous condition may be detectable through focus activity, tracking activity, PS11 current, and timing.
- PS11 current may help confirm whether the driver IC is drawing current during a suspected fault.
- PS11 current alone should not trigger cutoff.
- Coil activity alone should not trigger cutoff.
- Active cutoff should only happen after a confirmed sustained fault.
- The first detection firmware should only log suspected faults.
- The first cutoff-capable hardware should default to cutoff disabled.
- A final design should include fail-safe behavior and clear recovery behavior.

This theory must be tested.

---

## Future Hardware Goals

A future cutoff-capable board may include:

- PS11 current-sense path.
- Protected fuse-aware current path.
- Cutoff switch or load switch.
- Safe default gate or enable control.
- Hardware fault latch.
- Fault LED.
- Manual cutoff enable jumper.
- Manual override.
- ESP32 fault input.
- ESP32 cutoff control output.
- Test pads for current and voltage.
- Board-revision-specific install options.
- Clear silkscreen labels.
- Mechanical strain relief.
- Protection against backfeeding.

---

## Future Firmware Goals

Future firmware may include:

- Logging-only detection mode.
- Cutoff simulation mode.
- Active cutoff mode.
- Startup ignore timer.
- Disc-detection ignore timer.
- Fault confirmation timer.
- Fault latch logic.
- Manual reset.
- Fault history.
- Web interface warning page.
- Board-revision profiles.
- Configurable thresholds.
- Exportable logs.
- Safety lockout for untested profiles.

Active cutoff should require intentional configuration or hardware enable during development.

---

## Documentation Requirements Before Release

Before any cutoff-enabled kit is released, documentation should include:

- Exact supported PS2 models.
- Exact supported board revisions.
- Exact cutoff point.
- Exact PS11 current-monitoring method.
- Hardware revision.
- Firmware revision.
- Install guide.
- First-power-on checklist.
- Fault behavior explanation.
- Recovery procedure.
- Manual override instructions.
- Known false-trigger cases.
- Known unsupported models.
- Safety warnings.
- Troubleshooting guide.
- Test results.

A cutoff-enabled kit should not be released without clear documentation.

---

## Customer-Facing Limitation

If Layzr Savre becomes a product, the cutoff feature should be described carefully.

Avoid wording such as:

- Guaranteed laser protection.
- Prevents all optical-drive damage.
- Works on every PS2.
- Impossible to damage the console.
- No testing required.
- Safe for beginners.

Better wording:

- Designed to monitor optical-drive behavior.
- Designed to detect certain abnormal driver or coil conditions.
- Includes a tested protection response on supported board revisions.
- Requires correct installation.
- Requires supported hardware.
- Cannot protect against every failure.
- Intended for advanced PS2 modders and technicians.

---

## Development Rule

For Layzr Savre, the cutoff development rule is:

Monitor first.  
Log second.  
Detect third.  
Simulate cutoff fourth.  
Cut power last.

---

## Summary

Coil or driver power cutoff is a future Layzr Savre protection concept.

The project may eventually cut power to a validated driver or coil-related path after a confirmed unsafe condition is detected.

At this stage, the cutoff method is not finalized.

PS11 is currently being used as a current-monitoring research point, not a proven cutoff point.

Active cutoff should only be added after passive monitoring, PS11 current logging, flatline detection, false-trigger testing, and recovery behavior are properly validated.

The final goal is a cutoff method that is useful, documented, fail-safe where possible, and safe enough for a future advanced PS2 modding kit.
