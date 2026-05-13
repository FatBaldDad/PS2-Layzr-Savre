# Safety and Limitations

**Project:** PS2 Layzr Savre  
**Owner:** FatBaldDad  
**Status:** Early research / planning / prototype development  

---

## Overview

PS2 Layzr Savre is an experimental optical-drive protection and telemetry project for the PlayStation 2.

The purpose of this project is to study, monitor, log, and eventually help protect the PS2 optical-drive system. This includes observing tracking and focusing coil behavior, monitoring current consumption, detecting possible unsafe flatline conditions, and exploring safe methods for cutting coil or servo power when a confirmed fault condition is detected.

This project is not currently a finished product, public kit, or guaranteed protection device.

---

## Important Warning

Layzr Savre interacts with sensitive parts of the PlayStation 2 optical-drive, laser, servo, DSP, Mechacon, Syscon, and power systems.

Incorrect installation, incorrect wiring, incorrect firmware, incorrect board-revision assumptions, or incorrect testing may damage the console.

Possible damage may include:

- Optical-drive failure
- Laser failure
- Servo-driver damage
- DSP-related damage
- Mechacon or Syscon issues
- Motherboard damage
- Blown fuses
- Damaged traces or pads
- Unstable console behavior
- Loss of disc-reading function

Use early versions of this project only if you understand the risks.

---

## Current Project Limitation

Layzr Savre is currently in the research and prototype planning stage.

At this stage:

- No production-ready hardware has been released.
- No production-ready firmware has been released.
- No final kit has been released.
- No universal PS2 compatibility has been confirmed.
- No guaranteed protection behavior has been validated.
- No final flatline-detection threshold has been established.
- No final cutoff circuit has been validated.
- No public installation procedure should be considered final.

Early documentation is intended to guide research and development, not to serve as a final install manual.

---

## No Guarantee of Protection

Layzr Savre is intended to help study and potentially protect the PS2 optical-drive system, but it cannot be guaranteed to prevent all damage.

This project may not protect against every possible failure, including:

- Bad lasers
- Weak lasers
- Shorted coils
- Servo-driver failures
- DSP faults
- Mechacon faults
- Power-supply faults
- Incorrect laser adjustment
- Bad ribbon cables
- Dirty or damaged discs
- Incorrect installation
- Incorrect firmware settings
- Board-revision differences
- Unknown failure modes

Protection behavior must be tested and validated before any protection claim can be made.

---

## Experimental Hardware Notice

Early Layzr Savre hardware should be treated as experimental.

Prototype hardware may contain:

- Incorrect assumptions
- Unverified signal mappings
- Layout mistakes
- Connector orientation issues
- Current-sense errors
- Voltage-sense errors
- Signal-loading problems
- Noise issues
- Incomplete protection circuits
- Firmware dependency risks
- Board-revision compatibility problems

Do not install prototype hardware into a console that you are not willing to risk.

---

## Prototype Testing Recommendation

Early testing should be performed on sacrificial or non-critical PS2 consoles.

Recommended testing order:

1. Visual inspection only.
2. Continuity testing before installation.
3. Power-off resistance checks.
4. Passive signal observation only.
5. Confirm normal console operation.
6. Measure voltages.
7. Measure current behavior.
8. Capture oscilloscope data.
9. Add ESP32 logging only after passive behavior is confirmed.
10. Test any active cutoff feature only after passive monitoring and detection behavior are understood.

Active cutoff testing should not be the first step.

---

## Board Revision Risk

The PlayStation 2 has many models and motherboard revisions.

Different board revisions may use different:

- DSP chips
- Mechacon or Syscon behavior
- Servo-driver circuits
- Fuse layouts
- Laser assemblies
- Ribbon cable pinouts
- Power paths
- Signal names
- Test points
- Ground references
- Optical-drive behavior

A circuit that works on one PS2 board revision may not work safely on another.

Before installation, the board revision should be identified and documented.

---

## Supported Models

No PS2 model should be considered officially supported until tested and documented.

Future compatibility notes should include:

- PS2 model number
- Motherboard revision
- Laser model
- Optical-drive assembly type
- Tested hardware revision
- Tested firmware revision
- Test result
- Known issues
- Required install differences

---

## Unsupported Models

A model or board revision should be considered unsupported if:

- The signal path has not been mapped.
- The PS11 or servo power path has not been confirmed.
- The optical-drive connector differs from tested versions.
- The board behaves differently during startup or read failure.
- The cutoff method has not been tested.
- The install procedure has not been documented.
- The project owner has not confirmed compatibility.

Unsupported does not always mean impossible. It means not tested and not validated.

---

## Optical-Drive Signal Risk

Layzr Savre may monitor or interact with signals related to:

- Tracking coils
- Focusing coils
- Servo-driver outputs
- DSP control signals
- Optical-drive power
- PS11 or related fuse paths
- Laser and sled behavior
- Disc read and retry behavior

These signals may be sensitive to loading, added capacitance, noise, bad grounding, or incorrect probing.

Even a monitoring circuit can affect normal operation if it loads a signal too heavily.

---

## Monitoring Versus Control

The project should separate monitoring from control.

Monitoring means:

- Observing signals
- Logging voltage or current
- Capturing behavior
- Sending data to the ESP32
- Creating test records

Control means:

- Cutting power
- Pulling a signal high or low
- Resetting part of the circuit
- Changing drive behavior
- Interrupting coil or servo operation

Early prototypes should prioritize monitoring before control.

---

## Passive Prototype Limitation

The first passive interposer revision should not be treated as a protection device.

A passive monitor board is intended to:

- Break out signals
- Provide test points
- Allow oscilloscope measurements
- Allow data collection
- Help identify normal and abnormal behavior

A passive monitor board is not intended to:

- Protect the laser
- Cut coil power
- Reset the console
- Prevent all damage
- Make automatic decisions
- Replace proper troubleshooting

---

## ESP32 Limitation

The ESP32 is useful for logging, communication, and interface features, but it should not be blindly trusted with protection behavior until fully tested.

ESP32-related risks may include:

- Boot delay
- Firmware crash
- Pin state during boot
- Floating GPIO pins
- Incorrect ADC readings
- Noise on analog inputs
- Missed fast events
- Watchdog resets
- Brownout behavior
- Incorrect threshold settings
- Web interface configuration mistakes

Any ESP32-controlled cutoff feature should be designed with safe default behavior.

---

## Firmware Limitation

Early firmware should be considered experimental.

Firmware may contain:

- Incorrect thresholds
- Timing errors
- False-trigger behavior
- Missed fault detection
- Logging errors
- ADC calibration errors
- Pin assignment mistakes
- Unsafe default states
- Incomplete fault handling
- Incomplete recovery handling

Do not rely on early firmware to protect a console.

---

## Flatline Detection Limitation

Flatline detection is one of the main goals of this project, but it must be validated carefully.

A flatline-like condition may not always mean a dangerous fault. Normal drive behavior may include periods of reduced movement, pauses, retries, startup delays, or disc-detection behavior.

Detection logic must avoid false triggers during:

- Console startup
- Disc insertion
- Disc detection
- Laser focusing
- Normal seeking
- Read retries
- Disc spin-up
- Disc spin-down
- No-disc state
- Browser screen behavior
- Game loading transitions

A valid fault trigger should require more than a simple single-signal state.

---

## Current Monitoring Limitation

Monitoring current through PS11 or a related servo power path may provide useful information, but it may not tell the entire story.

Current behavior may vary depending on:

- PS2 model
- Board revision
- Laser model
- Disc type
- Disc condition
- Servo-driver design
- Power supply
- Optical-drive condition
- Temperature
- Mechanical drag
- Ribbon cable condition
- Console modifications

Current monitoring should be used as part of a larger detection strategy, not as the only source of truth.

---

## Coil or Servo Power Cutoff Risk

Cutting coil or servo power is an advanced and risky feature.

Incorrect cutoff behavior may cause:

- Failed disc reads
- Console freezing
- Optical-drive errors
- Servo-driver stress
- Unexpected current paths
- Reset issues
- Partial power states
- Damage to surrounding circuitry
- Unrecoverable fault states

Before any cutoff circuit is used, the safest cutoff point must be identified and validated.

---

## Fail-Safe Design Requirement

Any future active protection circuit should aim for fail-safe behavior.

A safer design should consider:

- What happens if the ESP32 is not powered
- What happens during ESP32 boot
- What happens if firmware crashes
- What happens if a GPIO floats
- What happens if the board is partially connected
- What happens if the current-sense circuit fails
- What happens if the user installs it backwards
- What happens if the console loses power during a fault
- What happens after the fault clears

The console should not be placed into a worse condition because the protection board failed.

---

## Installation Risk

Installation may require fine soldering, test-point wiring, ribbon cable work, connector alignment, and board-revision knowledge.

Installation risks include:

- Lifted pads
- Torn traces
- Solder bridges
- Cold joints
- Reversed connectors
- Wrong fuse connection
- Wrong ground point
- Wrong signal tap
- Damaged ribbon cable
- Mechanical interference
- Short circuits after reassembly

This project is not intended for beginners in its early stages.

---

## Required Skill Level

Early Layzr Savre prototypes are intended for advanced users.

Recommended skills include:

- PS2 disassembly and reassembly
- Fine soldering
- Multimeter use
- Reading schematics
- Identifying board revisions
- Understanding fuses and power paths
- Oscilloscope use
- Logic-analyzer use
- ESP32 flashing and debugging
- Basic firmware troubleshooting
- Safe electronics testing practices

---

## Required Test Equipment

Recommended equipment for development and validation:

- Multimeter
- Oscilloscope
- Logic analyzer
- Bench power supply, if available
- Current measurement tools
- USB-to-serial adapter
- ESP32 programming tools
- Magnification
- Good lighting
- Fine soldering tools
- Known-good PS2 discs
- Known-good optical-drive assemblies
- Sacrificial PS2 test console

Not every future installer may need all of this equipment, but early development does.

---

## Power Supply Risk

Power supply behavior can affect testing.

Risks may include:

- Incorrect voltage
- Weak power adapter
- Noisy power supply
- Voltage sag
- Bad ground reference
- USB-C trigger board issues
- Brownout behavior
- Inrush current
- Poor filtering
- Shared ground noise

Power conditions should be documented during testing.

---

## Mechanical Risk

The interposer, wires, test pads, ESP32 board, and cutoff hardware must not interfere mechanically with the PS2.

Mechanical risks include:

- Pinched wires
- Ribbon cable strain
- Shorting against shielding
- Board movement
- Insufficient insulation
- Pressure on optical-drive parts
- Interference with tray movement
- Interference with disc spin
- Heat buildup
- Poor mounting

All installed hardware should be mechanically secure before final testing.

---

## Heat Risk

Additional hardware may introduce heat or block airflow.

Heat-related risks include:

- ESP32 heat
- Regulator heat
- Current-sense resistor heat
- MOSFET or switch heat
- Servo-driver heat
- Localized heating near optical-drive components
- Reduced airflow after installation

Thermal behavior should be checked during longer tests.

---

## Data Logging Limitation

Logged data is only useful when the test conditions are documented.

Useful logs should include:

- PS2 model
- Board revision
- Laser model
- Disc type
- Disc condition
- Power supply used
- Hardware revision
- Firmware revision
- Probe points
- Current-sense method
- Test duration
- Observed behavior

A log without context may be difficult to compare or reproduce.

---

## Test Data Warning

Test data collected from one console should not be assumed to apply to all consoles.

A single successful test does not prove universal compatibility.

A single failed test does not always mean the concept is wrong.

Multiple controlled tests are needed before drawing conclusions.

---

## Community Testing Warning

Community testing is useful, but it must be organized.

Testers should understand:

- The hardware is experimental.
- Console damage is possible.
- Results must include board information.
- Photos are important.
- Logs are more useful with context.
- Failed tests should still be reported.
- Safety concerns should be reported immediately.

---

## Product and Kit Limitation

Layzr Savre is not currently a finished kit.

Before any kit release, the project should have:

- Stable hardware revision
- Stable firmware revision
- Compatibility list
- Unsupported model list
- Installation guide
- Test procedure
- Troubleshooting guide
- Safety warnings
- Known limitations
- Kit contents list
- Quality-control checklist
- Recovery procedure
- Clear customer-facing explanation

Until then, it should be treated as a development project.

---

## Customer-Facing Limitation

If Layzr Savre becomes a product or kit, the description should avoid overpromising.

Avoid claims such as:

- Guaranteed laser protection
- Works on every PS2
- Prevents all optical-drive damage
- Impossible to damage the console
- Beginner-friendly install
- No testing required

Better wording:

- Experimental optical-drive protection and telemetry system
- Designed to monitor laser and servo behavior
- Intended to help detect unsafe drive conditions
- Requires correct installation and supported board revision
- Protection behavior depends on testing and validation
- Designed for advanced PS2 modders and technicians

---

## Legal and Trademark Notice

PlayStation, PlayStation 2, PS2, and related names are trademarks of their respective owners.

Layzr Savre is an independent preservation and hardware research project.

This project is not affiliated with, endorsed by, sponsored by, or approved by Sony Interactive Entertainment or any related company.

---

## Warranty Disclaimer

This project is provided for research and development purposes only.

No warranty is provided.

The project owner is not responsible for damage caused by:

- Incorrect installation
- Incorrect wiring
- Incorrect firmware
- Incorrect testing
- Incorrect board revision use
- Incorrect assumptions
- Defective parts
- User modification
- Console condition
- Power-supply issues
- Manufacturing defects in prototype hardware

Use at your own risk.

---

## Recommended Safety Rules

Follow these rules during development:

1. Do not test on a valuable console first.
2. Do not add active cutoff before passive monitoring works.
3. Do not assume all PS2 board revisions are the same.
4. Do not trust firmware until it is tested.
5. Do not rely on one signal for protection decisions.
6. Do not ignore false triggers.
7. Do not skip continuity testing.
8. Do not power the console if a short is suspected.
9. Do not install the board without insulation and strain relief.
10. Do not claim the project is finished until it has been validated.

---

## Development Safety Checklist

Before powering a console with Layzr Savre hardware installed:

- [ ] Confirm board revision.
- [ ] Confirm connector orientation.
- [ ] Inspect all solder joints.
- [ ] Check for solder bridges.
- [ ] Check continuity on power paths.
- [ ] Check for shorts to ground.
- [ ] Confirm ground connection.
- [ ] Confirm no signal is accidentally pulled high or low.
- [ ] Confirm ESP32 pins are safe during boot.
- [ ] Confirm the interposer does not mechanically interfere.
- [ ] Confirm wires are secured.
- [ ] Confirm exposed pads are insulated.
- [ ] Confirm the optical drive can move freely.
- [ ] Confirm the disc cannot contact added hardware.
- [ ] Confirm the power supply is correct.

---

## First Power-On Checklist

Recommended first power-on process:

- [ ] Power on without a disc first.
- [ ] Watch for smoke, heat, noise, or abnormal behavior.
- [ ] Confirm standby and power behavior.
- [ ] Confirm the console reaches the browser screen.
- [ ] Confirm the optical drive does not behave abnormally.
- [ ] Check voltage readings.
- [ ] Check current readings.
- [ ] Confirm ESP32 logging starts normally, if installed.
- [ ] Test with a known-good disc only after basic behavior is confirmed.
- [ ] Stop testing immediately if abnormal behavior occurs.

---

## Stop Testing If

Stop testing immediately if any of the following occur:

- Burning smell
- Smoke
- Excessive heat
- Blown fuse
- Console will not power on
- Console resets repeatedly
- Optical drive makes abnormal noises
- Laser does not behave normally
- Disc does not spin normally
- Servo driver becomes unusually hot
- ESP32 becomes unusually hot
- Current draw is abnormal
- Voltage rail is pulled down
- Protection circuit triggers repeatedly without cause

Investigate the issue before continuing.

---

## Documentation Requirement

Every hardware revision should document:

- Purpose of the revision
- What changed
- What was tested
- What was not tested
- Known risks
- Supported boards
- Unsupported boards
- Required firmware
- Install notes
- Safety notes
- Known issues

---

## Summary

PS2 Layzr Savre is a preservation-focused research and development project.

The goal is to better understand and eventually help protect the PS2 optical-drive system, but the project is not yet a finished or guaranteed protection device.

Early revisions should be treated as experimental hardware for advanced users only.

The safest path forward is:

1. Research first.
2. Monitor passively.
3. Collect real test data.
4. Validate detection behavior.
5. Add active cutoff only after testing.
6. Document limitations honestly.
7. Release a kit only when the design is stable and well understood.
