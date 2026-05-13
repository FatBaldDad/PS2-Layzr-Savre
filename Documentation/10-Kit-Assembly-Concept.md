# Kit Assembly Concept

**Project:** PS2 Layzr Savre  
**Owner:** FatBaldDad  
**Status:** Early research / planning / prototype development  
**Document:** 10 - Kit Assembly Concept  

---

## Overview

The long-term goal of PS2 Layzr Savre is to become a documented kit for the PS2 community.

This kit is intended for advanced PS2 modders, repair technicians, preservation-focused builders, and hardware developers who want to monitor, study, and eventually help protect the PS2 optical-drive system.

At this stage, Layzr Savre is not a finished kit.

This document is a planning document for what a future kit may include, how it may be assembled, how it may be packaged, and what documentation should exist before it is offered publicly.

---

## Purpose of This Document

This document explains the early kit assembly concept for Layzr Savre.

It is intended to document:

- What a future kit may include.
- What hardware may be part of the kit.
- What firmware may be included.
- What documentation is required.
- What safety warnings are needed.
- What testing should happen before packaging.
- What quality-control checks should be performed.
- What customer-facing limitations should be stated.
- What should be included for beta kits versus public kits.

This document should be updated as the hardware and firmware become real.

---

## Important Notice

Layzr Savre is currently an experimental research and prototype project.

No public kit should be offered until the project has:

- Stable hardware.
- Stable firmware.
- Tested passive monitoring.
- Tested PS11 current monitoring.
- Tested ESP32 logging.
- Validated detection behavior.
- Documented false-trigger behavior.
- Tested cutoff behavior, if cutoff is included.
- Clear supported model information.
- Clear unsupported model information.
- Installation documentation.
- Safety documentation.
- Troubleshooting documentation.

A kit should not be released based only on theory.

---

## Kit Philosophy

The Layzr Savre kit should be built around a preservation-first goal.

The purpose of the kit is to help preserve the PS2’s original ability to read discs by providing better monitoring, logging, and eventually protection of the optical-drive system.

The kit should prioritize:

- Honest documentation.
- Safe installation.
- Clear limitations.
- Board-revision awareness.
- Repeatable testing.
- Repairability.
- Community usefulness.
- Clear support expectations.
- No overpromising.

The kit should be useful even as a diagnostic and research tool.

---

## Intended Audience

Layzr Savre should be treated as an advanced kit.

The intended audience includes:

- Advanced PS2 modders.
- PS2 repair technicians.
- Console preservation builders.
- Hardware developers.
- Beta testers with soldering experience.
- Users comfortable with multimeters and test points.
- Users who understand that prototype hardware carries risk.

The early kit should not be marketed as beginner-friendly.

---

## Not Intended For

Early Layzr Savre kits are not intended for:

- Beginners with no soldering experience.
- Users who cannot identify a PS2 board revision.
- Users who cannot follow test instructions.
- Users who expect guaranteed protection.
- Users who want a simple plug-and-play repair.
- Users who want to avoid all risk.
- Customer consoles without prior validation.
- Rare or valuable consoles during early testing.

The kit may become easier to install later, but the first versions should be aimed at advanced users.

---

## Possible Kit Types

Layzr Savre may eventually be offered in different kit levels.

| Kit Type | Purpose | Status |
|---|---|---|
| Research Kit | Passive monitoring and test pads only | Future concept |
| Logging Kit | Passive monitoring plus ESP32 logging | Future concept |
| Current Monitor Kit | Adds PS11 current monitoring | Future concept |
| Detection Kit | Adds logging-only flatline detection | Future concept |
| Protection Kit | Adds validated active cutoff behavior | Future concept |
| Beta Kit | Limited release for trusted testers | Future concept |
| Public Kit | Final documented community release | Future goal |

The first release should likely be a research or logging kit, not a full protection kit.

---

## Possible Kit Contents

A future Layzr Savre kit may include:

- Layzr Savre interposer board.
- ESP32 interface board.
- Current-sense hardware.
- Low-value shunt resistor or current-sense assembly.
- Required wire.
- Required connectors.
- Optional flex cable.
- Optional test pads or probe points.
- Optional fault LED.
- Optional manual reset button.
- Optional cutoff enable jumper.
- Optional insulation material.
- Printed or digital quick-start guide.
- Link to full GitHub documentation.
- Firmware file or flashing instructions.
- Test checklist.
- Safety warning card.

The final kit contents should depend on the validated hardware revision.

---

## Research Kit Concept

A research kit would focus on passive monitoring only.

Possible contents:

- Passive interposer board.
- Test pads.
- Ground reference pads.
- Signal breakout pads.
- Basic install notes.
- Scope probing guide.
- Board-revision notes.
- Safety warning.

A research kit should not include active cutoff.

Purpose:

- Learn signal behavior.
- Collect scope captures.
- Confirm board compatibility.
- Help build project data.

---

## Logging Kit Concept

A logging kit would add ESP32 data collection.

Possible contents:

- Passive interposer board.
- ESP32 interface board.
- Conditioned signal inputs.
- PS11 current-monitor input, if validated.
- USB or serial programming access.
- Logging firmware.
- Serial logging instructions.
- Optional web interface instructions.
- Test report template.

Purpose:

- Record optical-drive behavior.
- Log focus activity.
- Log tracking activity.
- Log PS11 current.
- Support future detection development.

---

## Current Monitor Kit Concept

A current monitor kit would focus on PS11 current observation.

Possible contents:

- PS11 current-sense board or section.
- Low-value current-sense path.
- Fuse-aware installation method.
- Test pads for shunt voltage.
- Optional current-sense amplifier.
- ESP32 current input.
- PS11 install instructions.
- Current measurement guide.

Purpose:

- Measure current through the PS11 fuse path.
- Compare normal and abnormal drive behavior.
- Provide current data for future detection logic.

Important note:

PS11 is a physical fuse. The kit must preserve or properly replace the protective role of the fuse path.

---

## Detection Kit Concept

A detection kit would run flatline detection in logging-only mode.

Possible contents:

- Interposer board.
- ESP32 interface board.
- Signal-conditioning hardware.
- PS11 current monitoring.
- Detection firmware.
- Fault logging.
- Fault LED or status output.
- Cutoff simulation mode.
- No active cutoff by default.

Purpose:

- Test detection logic.
- Identify false triggers.
- Record suspected fault events.
- Build confidence before active protection.

This kit should still be treated as experimental.

---

## Protection Kit Concept

A protection kit would include active cutoff behavior.

This should only happen after validation.

Possible contents:

- Interposer board.
- ESP32 interface board.
- PS11 current monitoring.
- Signal-conditioning hardware.
- Validated cutoff circuit.
- Fault latch.
- Fault indicator.
- Manual reset or recovery method.
- Cutoff enable hardware.
- Firmware with active protection mode.
- Full install guide.
- First-power-on checklist.
- Troubleshooting guide.
- Compatibility list.
- Safety warnings.

A protection kit should not be released until false triggers, recovery behavior, and board compatibility are documented.

---

## Beta Kit Concept

A beta kit should be a limited release for trusted testers.

Beta kit goals:

- Find install issues.
- Find documentation gaps.
- Collect test data.
- Identify board-revision differences.
- Test ESP32 logging.
- Test PS11 current monitoring.
- Test detection logic.
- Identify false triggers.
- Validate recovery behavior if cutoff is included.

Beta testers should understand that the kit is experimental.

---

## Public Kit Concept

A public kit should only be offered after testing and documentation are mature.

Public kit requirements:

- Stable hardware revision.
- Stable firmware revision.
- Tested installation process.
- Supported model list.
- Unsupported model list.
- Known issues list.
- Safety warnings.
- Clear customer-facing description.
- Full installation guide.
- First-power-on checklist.
- Troubleshooting guide.
- Firmware flashing guide.
- Quality-control checklist.
- Support process.

A public kit should not rely on undocumented assumptions.

---

## Possible Hardware Pieces

The final kit may include several hardware pieces.

| Hardware Piece | Purpose | Status |
|---|---|---|
| Interposer board | Monitor optical-drive signals | Planned |
| ESP32 board | Logging and interface | Planned |
| PS11 current-sense section | Monitor current through PS11 fuse path | Planned |
| Signal-conditioning circuit | Protect ESP32 inputs and clean signals | Planned |
| Fault LED | Show fault or warning state | Future concept |
| Cutoff switch circuit | Future active protection | Future research |
| Manual reset | Clear latched faults | Future concept |
| Cutoff enable jumper | Prevent accidental active cutoff | Future concept |
| Programming header | Flash ESP32 firmware | Planned |
| Test pads | Allow measurement and troubleshooting | Planned |
| Mechanical mounting aids | Secure kit inside console | Future concept |

---

## Interposer Board Assembly Concept

The interposer board is expected to be the main signal access point.

Possible interposer features:

- Optical-drive signal breakout.
- Focus activity monitor points.
- Tracking activity monitor points.
- Ground reference pads.
- Test pads for oscilloscope probing.
- Connection to ESP32 interface board.
- Clear silkscreen labels.
- Board-revision-specific notes.
- Minimal signal loading.
- Mechanical fitment designed for the PS2 shell.

The first interposer should be passive or mostly passive.

---

## ESP32 Interface Assembly Concept

The ESP32 interface board may be separate from the interposer or integrated later.

Possible ESP32 board features:

- ESP32 module or dev-board footprint.
- Power regulation.
- Protected inputs.
- Current-sense amplifier input.
- Voltage monitoring inputs.
- Serial programming header.
- USB programming access, if practical.
- Fault LED output.
- Optional reset button.
- Optional web interface support.
- Optional cutoff control output for future versions.

The ESP32 should begin as a logger, not a controller.

---

## PS11 Current-Sense Assembly Concept

The PS11 current-sense portion is one of the more sensitive parts of the kit.

Current concept:

- PS11 is a physical fuse.
- One side of PS11 may be lifted.
- The lifted fuse location may be routed through a known current-sense path.
- The voltage across the current-sense path may be measured.
- That voltage may be used to estimate current through the PS11 fuse path.

Important requirements:

- Preserve the protective role of the fuse.
- Avoid excessive voltage drop.
- Avoid unsafe bypasses.
- Use a properly rated current-sense part.
- Provide strain relief.
- Provide clear installation instructions.
- Clearly mark input and output sides.
- Test on sacrificial hardware first.

---

## Signal-Conditioning Assembly Concept

Signal conditioning is needed before PS2 signals reach the ESP32.

Possible signal-conditioning parts:

- High-impedance buffers.
- Voltage dividers.
- Clamp diodes.
- Protection resistors.
- RC filters.
- Comparators.
- Differential amplifiers.
- Current-sense amplifiers.
- External ADC.
- ESD protection.

The goal is to protect the PS2 and the ESP32 while preserving useful signal information.

---

## Cutoff Assembly Concept

A cutoff assembly may be added in a later version.

Possible cutoff parts:

- MOSFET switch.
- Load switch IC.
- Hardware fault latch.
- Cutoff enable jumper.
- Fault LED.
- Manual reset circuit.
- ESP32 cutoff control input.
- Test pads for cutoff verification.

Cutoff should be disabled by default during development.

Active cutoff should only be included in a kit after validation.

---

## Mechanical Assembly Concept

The kit must fit inside the PS2 without interfering with normal operation.

Mechanical concerns:

- Disc clearance.
- Optical pickup movement.
- Sled travel.
- Ribbon cable movement.
- Shielding clearance.
- Screw posts.
- Shell clearance.
- Airflow.
- Heat sources.
- Wire strain.
- Insulation.
- Serviceability.

The kit should not make the console harder to service than necessary.

---

## Wiring Concept

Wiring should be kept clean, short, and strain-relieved.

Wiring concerns:

- Avoid long signal wires.
- Avoid wires near moving parts.
- Avoid wires under mechanical stress.
- Avoid uninsulated solder joints.
- Avoid wires that can be pinched by the shell.
- Avoid routing near the spinning disc.
- Avoid routing that blocks the optical pickup.
- Avoid creating ground loops.
- Label wires or use consistent colors where possible.

A final kit should include clear wiring diagrams.

---

## Connector Concept

A future kit may use connectors where practical.

Possible connector benefits:

- Easier installation.
- Easier removal.
- Easier testing.
- Less soldering during service.
- Cleaner assembly.
- Better repeatability.

Possible connector concerns:

- Space limitations.
- Cost.
- Mechanical reliability.
- Added height.
- Signal integrity.
- User plugging things in backwards.

Connector orientation should be clearly marked.

---

## Insulation and Strain Relief

The kit should include or recommend insulation and strain relief.

Possible materials:

- Kapton tape.
- Fish paper.
- Heat shrink tubing.
- Foam spacer, if safe.
- 3D printed bracket.
- Adhesive standoff.
- Cable tie point.
- Solder mask-covered boards.
- Clear keepout markings.

Nothing should be able to short against the RF shield, shell, or drive assembly.

---

## Firmware Included With Kit

A future kit may include firmware or firmware flashing instructions.

Possible firmware types:

- ESP32 Logger firmware.
- ESP32 Detection firmware.
- ESP32 Cutoff Simulation firmware.
- ESP32 Protection Beta firmware.
- ESP32 Release firmware.

Firmware should clearly identify:

- Firmware name.
- Firmware version.
- Hardware revision supported.
- Board profiles supported.
- Active cutoff status.
- Logging mode.
- Known issues.

Active cutoff firmware should not be confused with logging-only firmware.

---

## Firmware Safety

Kit firmware should use safe defaults.

Safe default ideas:

- Logging-only mode by default.
- Active cutoff disabled by default.
- Unsupported board profiles locked to logging-only mode.
- Cutoff requires physical jumper and firmware enable.
- Serial output reports safety state at boot.
- Web interface clearly shows active protection status.
- Fault thresholds have safe limits.
- Configuration can be reset to defaults.

Firmware should not enable dangerous features silently.

---

## Documentation Included With Kit

A future kit should include clear documentation.

Required documentation may include:

- Kit contents list.
- Supported model list.
- Unsupported model list.
- Required tools list.
- Installation guide.
- First-power-on checklist.
- ESP32 flashing guide.
- Logging guide.
- PS11 current-monitoring guide.
- Troubleshooting guide.
- Safety and limitations document.
- FAQ.
- Warranty or no-warranty statement.
- Support contact information.

Documentation should be available in the repo and linked from the kit.

---

## Required Tools List

A future kit may require tools such as:

- Precision screwdriver set.
- Fine-tip soldering iron.
- Flux.
- Fine solder.
- Tweezers.
- Magnification.
- Multimeter.
- Kapton tape.
- Flush cutters.
- Small wire.
- USB cable or programming adapter.
- Oscilloscope, for development or beta testing.
- Logic analyzer, only for confirmed safe logic signals.

The public kit should clearly state which tools are required and which are optional.

---

## Installation Skill Level

Early kits should be labeled as advanced.

Expected skills:

- PS2 disassembly.
- Fine soldering.
- Fuse lifting.
- Wire routing.
- Continuity testing.
- Reading install diagrams.
- Identifying board revisions.
- Flashing ESP32 firmware.
- Using a multimeter.
- Understanding risk.

A public release may become easier later, but the first versions should be honest about difficulty.

---

## First-Power-On Kit Checklist

A kit should include a first-power-on checklist.

Example checklist:

- [ ] Confirm PS2 model.
- [ ] Confirm board revision.
- [ ] Confirm kit hardware revision.
- [ ] Confirm firmware revision.
- [ ] Inspect solder joints.
- [ ] Check for shorts.
- [ ] Check PS11 current-sense path.
- [ ] Confirm fuse protection is preserved.
- [ ] Confirm ESP32 power wiring.
- [ ] Confirm signal input protection.
- [ ] Confirm cutoff disabled, if installed.
- [ ] Confirm wires are insulated.
- [ ] Confirm no mechanical interference.
- [ ] Power on with no disc.
- [ ] Confirm normal browser behavior.
- [ ] Confirm ESP32 logging.
- [ ] Test with known-good disc only after no-disc test passes.

---

## Quality-Control Checklist

Each kit should be checked before shipping.

Possible QC checks:

- [ ] PCB revision verified.
- [ ] Correct components installed.
- [ ] Visual inspection passed.
- [ ] No solder bridges.
- [ ] Connector orientation verified.
- [ ] Continuity checks passed.
- [ ] Power rails checked.
- [ ] ESP32 boots.
- [ ] Firmware version verified.
- [ ] Serial output verified.
- [ ] Fault LED verified, if installed.
- [ ] Cutoff disabled by default.
- [ ] Current-sense path inspected.
- [ ] Kit contents verified.
- [ ] Documentation link included.
- [ ] Packaging label applied.

QC results should be stored for each kit if possible.

---

## Kit Labeling

Kits should be labeled clearly.

Possible label information:

- Project name.
- Hardware revision.
- Firmware version, if flashed.
- Kit type.
- Batch number.
- Date assembled.
- Supported board revision, if applicable.
- Warning that the kit is experimental, if beta.
- Link to documentation.

Example label fields:

- Layzr Savre Kit Type:
- Hardware Revision:
- Firmware Version:
- Batch:
- Date:
- Tested By:
- Notes:

---

## Batch Tracking

Batch tracking may help with support and quality control.

Possible batch tracking information:

- Batch number.
- PCB manufacturer.
- PCB order date.
- Assembly date.
- Component lot notes.
- Firmware version.
- Known issues.
- Tester initials.
- Shipping date.
- Customer or beta tester reference, if applicable.

Batch tracking helps identify problems later.

---

## Packaging Concept

A future kit may be packaged with:

- Anti-static bag.
- Small labeled parts bags.
- Protective cardboard or foam.
- Printed warning card.
- QR code to GitHub documentation.
- QR code to firmware download.
- Kit contents checklist.
- Revision label.
- Optional sticker or branding.

Packaging should protect the hardware and make the kit easy to identify.

---

## Documentation Link Concept

The kit should point users to the latest documentation.

Possible link methods:

- QR code.
- Short URL.
- GitHub repository link.
- Website support page.
- Printed quick-start card.

The printed material should avoid becoming outdated by relying on the repo for full instructions.

---

## Website, Etsy, and eBay Listing Considerations

If Layzr Savre is offered as a kit, listings should be careful and honest.

Avoid wording such as:

- Guaranteed laser protection.
- Works on every PS2.
- Prevents all optical-drive damage.
- Beginner-friendly.
- No testing required.
- Impossible to damage the console.

Better wording:

- Experimental optical-drive telemetry and protection kit.
- Designed for advanced PS2 modders.
- Monitors optical-drive behavior.
- Supports PS11 current monitoring.
- Designed to help detect certain abnormal conditions.
- Requires correct installation.
- Supported models only.
- Cannot protect against every failure.

The listing should clearly state what is included and what is not included.

---

## What the Kit Should Not Include

The kit should not include:

- BIOS files.
- ROM files.
- Game files.
- Disc images.
- Copyrighted Sony service manual scans.
- Piracy-related files.
- Unlicensed copyrighted material.
- Unsupported firmware builds.
- Unverified install instructions.
- Claims that have not been tested.

The kit should focus on original hardware preservation and documented testing.

---

## Beta Kit Requirements

Before sending beta kits, the project should have:

- Beta hardware revision.
- Firmware version for beta.
- Known risks list.
- Install guide draft.
- Test checklist.
- Feedback form or issue template.
- Supported test console notes.
- Clear warning that the hardware is experimental.
- Clear instruction that active cutoff is disabled unless intentionally enabled.
- Clear request for test data and photos.

Beta testers should know what kind of feedback is needed.

---

## Beta Tester Feedback

Beta testers should be asked to provide:

- PS2 model.
- Board revision.
- Driver IC marking.
- Laser model, if known.
- Install photos.
- Test setup photos.
- Baseline console behavior.
- ESP32 logs.
- PS11 current data, if tested.
- Focus and tracking observations.
- False trigger reports.
- Failed tests.
- Suggestions for documentation.
- Safety concerns.
- Fitment issues.

Failed results are useful and should be reported.

---

## Public Kit Requirements

Before public release, the project should have:

- Stable hardware revision.
- Stable firmware revision.
- Tested installation guide.
- Confirmed supported models.
- Confirmed unsupported models.
- Known limitations.
- Troubleshooting guide.
- First-power-on checklist.
- QC checklist.
- Packaging checklist.
- Firmware flashing instructions.
- Clear customer-facing explanation.
- Support process.

A public kit should not be released until these are ready.

---

## Support Process Concept

A future support process may include:

- GitHub Issues for technical reports.
- Website support page.
- Email support.
- Discord support channel.
- FAQ.
- Troubleshooting flowchart.
- Known issues page.
- Firmware update notes.
- Compatibility list.

Support expectations should be realistic.

---

## Return and Warranty Concept

A future kit should have a clear warranty or no-warranty statement.

Because this project involves user installation into old consoles, support terms must be clear.

Possible policy points:

- Kit tested before shipping.
- Damage from incorrect installation is not covered.
- Console damage is not covered.
- Experimental beta kits have limited support.
- Firmware updates may be provided.
- Replacement parts may be available depending on situation.
- User must follow documentation.

This should be written clearly before sales begin.

---

## Manufacturing Files

Manufacturing files may eventually include:

- Gerbers.
- Drill files.
- BOM.
- Pick-and-place files.
- Assembly drawings.
- Schematic PDF.
- PCB render images.
- Test fixture notes.
- QC checklist.
- Packaging labels.

Manufacturing files should only be published if the chosen license allows it.

The current license status should be checked before releasing files.

---

## Assembly Documentation

Assembly documentation should include:

- PCB revision.
- Component placement.
- Polarity notes.
- Connector orientation.
- Fuse orientation.
- Shunt value.
- ESP32 module orientation.
- Programming steps.
- Test points.
- QC steps.
- Known assembly risks.

Assembly notes should be clear enough to repeat the build later.

---

## Revision Control

Every kit revision should be tracked.

Revision notes should include:

- Hardware revision.
- Firmware revision.
- What changed.
- Why it changed.
- Compatibility changes.
- Known issues.
- Required documentation updates.
- Test status.
- Release status.

Changes should also be added to `CHANGELOG.md`.

---

## Kit Release Stages

Suggested release stages:

| Stage | Meaning |
|---|---|
| Internal Prototype | Built and tested by project owner only |
| Research Prototype | Used for signal and current measurement |
| Alpha Hardware | Early hardware with known risks |
| Beta Kit | Limited trusted tester release |
| Release Candidate | Nearly final kit under validation |
| Public Release | Community-ready kit |
| Revised Release | Updated hardware or firmware after feedback |

The repo should clearly state the current stage.

---

## Compatibility List Concept

A kit should include a compatibility list.

Suggested compatibility fields:

| Field | Description |
|---|---|
| PS2 model | Console model number |
| Board revision | Motherboard revision |
| Driver IC | Driver IC marking |
| Laser model | Optical pickup model |
| Kit revision | Tested Layzr Savre hardware revision |
| Firmware version | Tested firmware version |
| Status | Untested, research, beta, supported, unsupported |
| Notes | Known issues or install differences |

Compatibility should be based on testing.

---

## Unsupported Model List

Unsupported models should be documented clearly.

A model may be unsupported because:

- Not tested yet.
- Board layout differs.
- PS11 path differs.
- Driver IC differs.
- Signal points are not confirmed.
- Mechanical fitment is not confirmed.
- Detection thresholds are not validated.
- Active cutoff is not tested.
- Known unsafe behavior exists.

Unsupported does not always mean impossible. It means not validated.

---

## Customer-Facing Safety Summary

A future kit should include a simple safety summary.

Example wording:

Layzr Savre is an advanced PS2 optical-drive telemetry and protection project. It requires soldering, correct board identification, and careful installation. Incorrect installation can damage the console. This kit cannot guarantee protection from every laser, optical-drive, or motherboard failure. Use only on supported models and follow the documentation carefully.

This wording should be refined before release.

---

## Kit Assembly Open Questions

Current open questions:

- Should the interposer and ESP32 board be separate or combined?
- What PS2 model should be targeted first?
- What board revision should be the first supported version?
- What connector style is best?
- What current-sense method is safest at PS11?
- Should the kit include the shunt preinstalled?
- Should active cutoff be physically impossible unless enabled by jumper?
- Should the kit include a fault LED?
- Should the kit include a reset button?
- Should beta kits include printed cards?
- Should public kits include full printed instructions or QR links?
- What firmware platform should be used?
- How should firmware updates be distributed?
- How should each kit be serialized or batch labeled?
- What support process is realistic?

---

## Current Working Theory

The current working theory is:

- The first kit should be a research or logging kit.
- Active protection should not be included until validated.
- PS11 current monitoring should be treated as measurement first.
- ESP32 logging should be available before ESP32 control.
- Cutoff should be disabled by default during development.
- The kit should be aimed at advanced users.
- Documentation must be finished before public release.
- Compatibility should be based on test data.
- The kit should preserve the PS2’s original disc-reading function.

This theory will be updated as the project develops.

---

## Future Kit Goals

Future kit goals may include:

- Clean interposer board.
- Reliable ESP32 logging.
- Safe PS11 current monitoring.
- Clear install guide.
- Good fitment inside supported PS2 models.
- Simple serial or web interface.
- Fault logging.
- Logging-only detection mode.
- Optional active protection after validation.
- Batch tracking.
- QC process.
- Support documentation.
- Website, Etsy, and eBay-ready listing copy.

---

## Summary

The Layzr Savre kit should be developed carefully and honestly.

The project should begin with research, passive monitoring, PS11 current observation, and ESP32 logging before moving toward detection and active cutoff.

A future kit should include tested hardware, stable firmware, clear documentation, safety warnings, compatibility notes, and realistic customer-facing claims.

The goal is to offer a useful preservation-focused kit for the PS2 community without overpromising what the system can do.
