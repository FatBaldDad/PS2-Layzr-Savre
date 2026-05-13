# QA Checklist

**Project:** PS2 Layzr Savre  
**Owner:** FatBaldDad  
**Status:** Early research / planning / prototype development  
**Folder:** Manufacturing  

---

## Overview

This document is the quality-assurance checklist for PS2 Layzr Savre hardware, firmware, kit assembly, packaging, and release preparation.

The goal of this checklist is to make sure every Layzr Savre board or kit is inspected, tested, documented, and packaged consistently before it is used for development, sent to a beta tester, or eventually sold as a public kit.

At this stage, Layzr Savre is still experimental.

No checklist should be treated as final until the hardware, firmware, PS11 current monitoring, ESP32 logging, detection behavior, and any future cutoff method have been validated.

---

## Purpose of This Document

This checklist is intended to help track:

- PCB inspection.
- Component inspection.
- Soldering quality.
- Assembly quality.
- PS11 current-monitoring path safety.
- ESP32 firmware flashing.
- ESP32 boot behavior.
- Logging behavior.
- Cutoff-disabled status.
- Kit contents.
- Packaging.
- Labels.
- Documentation links.
- Beta tester readiness.
- Public release readiness.

This document should be updated as the project develops.

---

## QA Philosophy

Layzr Savre should be treated as a preservation-focused hardware project.

Every board or kit should be checked carefully because this hardware may connect to sensitive parts of the PS2 optical-drive system.

QA priorities:

1. Prevent damage to the PS2.
2. Prevent unsafe installation.
3. Prevent confusing hardware revisions.
4. Prevent incorrect firmware use.
5. Prevent active cutoff from being enabled by accident.
6. Preserve the PS11 fuse protection role.
7. Confirm logging works before detection.
8. Confirm detection works before cutoff.
9. Document all known limitations.
10. Ship only what has been checked.

---

## QA Stages

| Stage | Purpose | Status |
|---|---|---|
| Stage 0 | Documentation review | Planned |
| Stage 1 | Incoming PCB inspection | Planned |
| Stage 2 | Component inspection | Planned |
| Stage 3 | Assembly inspection | Planned |
| Stage 4 | Electrical inspection | Planned |
| Stage 5 | ESP32 firmware flashing | Planned |
| Stage 6 | Bench functional test | Planned |
| Stage 7 | PS2 development test | Planned |
| Stage 8 | Kit contents check | Planned |
| Stage 9 | Packaging check | Planned |
| Stage 10 | Final release check | Planned |

---

## Important Safety Warning

Layzr Savre hardware may interact with the PS2 optical-drive system, driver IC, focus and tracking signals, PS11 fuse path, and future cutoff hardware.

Incorrect assembly or incorrect firmware could damage a console.

Before any board or kit is used:

- Confirm the hardware revision.
- Confirm the firmware revision.
- Confirm the operating mode.
- Confirm active cutoff is disabled unless intentionally testing it.
- Confirm the PS11 current-monitoring path does not bypass fuse protection.
- Confirm inputs are protected.
- Confirm no shorts are present.
- Confirm documentation matches the hardware.

Do not test experimental hardware on a valuable or customer console first.

---

## Batch Information

Each manufacturing or prototype batch should have a batch record.

### Batch Record

- Batch ID:
- Hardware revision:
- PCB manufacturer:
- PCB order number:
- PCB color:
- PCB thickness:
- PCB quantity:
- Assembly date:
- Assembled by:
- Firmware version:
- Intended use:
- Notes:

---

## Board Identification

Each board should be clearly identifiable.

### Board ID Checklist

- [ ] Project name visible.
- [ ] Board revision visible.
- [ ] Orientation markers visible.
- [ ] Pin 1 markers visible, where needed.
- [ ] PS11 input and output sides labeled, where applicable.
- [ ] ESP32 connector labels visible, where applicable.
- [ ] Test pads labeled.
- [ ] Cutoff enable area clearly marked, if present.
- [ ] Logging-only or prototype status marked, if applicable.
- [ ] Serial number or batch number added, if used.

---

## Incoming PCB Inspection

Inspect bare PCBs before assembly.

### PCB Visual Inspection

- [ ] Correct project name.
- [ ] Correct board revision.
- [ ] Correct PCB thickness.
- [ ] Correct solder mask color.
- [ ] Correct silkscreen color.
- [ ] No obvious scratches.
- [ ] No broken corners.
- [ ] No delamination.
- [ ] No missing pads.
- [ ] No damaged castellations, if used.
- [ ] No blocked holes.
- [ ] No obvious copper defects.
- [ ] No silkscreen covering critical pads.
- [ ] No solder mask missing from areas that should be insulated.
- [ ] Test pads are readable.
- [ ] Connector orientation markings are readable.

### PCB Dimensional Inspection

- [ ] Board outline appears correct.
- [ ] Mounting holes appear correct.
- [ ] Connector footprint alignment appears correct.
- [ ] Interposer fitment areas appear correct.
- [ ] Clearance areas appear correct.
- [ ] No unexpected tab or panelization artifact remains.
- [ ] Board fits intended mechanical location, if checked.

---

## Bare PCB Electrical Check

Before assembly, check critical nets where possible.

### Bare PCB Continuity Check

- [ ] Ground continuity confirmed.
- [ ] Power net continuity confirmed.
- [ ] No short between power and ground.
- [ ] PS11 input path continuity checked, if applicable.
- [ ] PS11 output path continuity checked, if applicable.
- [ ] Current-sense pads continuity checked, if applicable.
- [ ] Cutoff switch pads checked, if applicable.
- [ ] ESP32 power pads checked, if applicable.
- [ ] Signal input pads checked for shorts.
- [ ] Adjacent fine-pitch pads checked for shorts.
- [ ] Test pads checked for expected connectivity.

---

## Component Inspection

Before assembly, verify components.

### Component Checklist

- [ ] Correct BOM revision used.
- [ ] Correct resistor values.
- [ ] Correct capacitor values.
- [ ] Correct shunt resistor value.
- [ ] Correct shunt resistor power rating.
- [ ] Correct current-sense amplifier, if used.
- [ ] Correct ESP32 module or board.
- [ ] Correct voltage regulator, if used.
- [ ] Correct MOSFET or load switch, if used.
- [ ] Correct connectors.
- [ ] Correct LEDs, if used.
- [ ] Correct buttons or jumpers, if used.
- [ ] Correct programming header.
- [ ] Correct fuse or fuse replacement part, if used.
- [ ] Components are not visibly damaged.
- [ ] Moisture-sensitive parts handled correctly, if applicable.

---

## Assembly Inspection

Inspect the assembled board before applying power.

### Solder Joint Checklist

- [ ] No solder bridges.
- [ ] No cold joints.
- [ ] No lifted pads.
- [ ] No tombstoned components.
- [ ] No missing components.
- [ ] No wrong-value components.
- [ ] No reversed polarized components.
- [ ] No damaged connectors.
- [ ] No loose parts.
- [ ] No excess solder balls.
- [ ] No flux residue in critical areas.
- [ ] Fine-pitch pins inspected under magnification.
- [ ] ESP32 module soldering inspected, if applicable.
- [ ] Current-sense shunt soldering inspected.
- [ ] Cutoff switch or MOSFET soldering inspected, if applicable.

### Mechanical Assembly Checklist

- [ ] Connectors seated correctly.
- [ ] Headers are straight.
- [ ] Buttons move freely, if installed.
- [ ] Jumpers fit correctly, if installed.
- [ ] Board does not flex excessively.
- [ ] No component height issue is visible.
- [ ] No sharp wire ends.
- [ ] No exposed conductor where insulation is required.
- [ ] Strain relief added where needed.
- [ ] Board can be handled safely.

---

## Electrical Inspection After Assembly

Do not flash or power the board until these checks pass.

### Power and Ground Checks

- [ ] No short between main power and ground.
- [ ] No short between ESP32 power and ground.
- [ ] No short between current-sense output and ground.
- [ ] No short between signal inputs and power.
- [ ] No short between signal inputs and ground unless expected.
- [ ] Voltage regulator input and output checked for shorts.
- [ ] ESP32 3.3V rail checked.
- [ ] Pull-up and pull-down resistors checked where applicable.
- [ ] Cutoff control line default state checked, if applicable.
- [ ] Fault LED line checked, if applicable.

### Current-Sense Checks

- [ ] Shunt resistor installed correctly.
- [ ] Shunt value verified.
- [ ] Shunt path continuity confirmed.
- [ ] Sense positive and sense negative are not reversed, if known.
- [ ] Current-sense amplifier orientation verified, if used.
- [ ] Current-sense amplifier output is not shorted.
- [ ] Current-sense path does not bypass fuse protection.
- [ ] Current-sense path does not create an unexpected short.
- [ ] Current-sense wiring or traces appear suitable for expected current.

---

## PS11-Specific QA

PS11 is a physical fuse on the PS2 motherboard.

For Layzr Savre, PS11 is currently being used as a current-monitoring point. The plan is to lift one side of PS11 and measure current through the PS11 fuse path.

### PS11 Installation QA

- [ ] PS11 location confirmed on the target board.
- [ ] PS11 is confirmed as a physical fuse.
- [ ] Correct side of PS11 identified before lifting.
- [ ] Lifted side documented.
- [ ] PS11 pad not damaged.
- [ ] Fuse body not cracked.
- [ ] Current-sense path connected correctly.
- [ ] Fuse protection role preserved.
- [ ] No unsafe bypass added.
- [ ] Shunt value documented.
- [ ] Shunt power rating documented.
- [ ] Voltage drop risk considered.
- [ ] Wiring is short and strain-relieved.
- [ ] Installation is insulated.
- [ ] Continuity checked before power.
- [ ] Shorts checked before power.

---

## ESP32 Firmware Flashing QA

Firmware must be matched to the hardware revision.

### Firmware Flash Checklist

- [ ] Correct ESP32 module selected.
- [ ] Correct firmware file selected.
- [ ] Correct firmware version selected.
- [ ] Correct hardware revision selected.
- [ ] Active cutoff status confirmed.
- [ ] Firmware is logging-only unless intentionally testing cutoff.
- [ ] Firmware build date recorded.
- [ ] Firmware flashes successfully.
- [ ] ESP32 boots after flashing.
- [ ] Serial monitor works.
- [ ] Firmware name prints at boot.
- [ ] Firmware version prints at boot.
- [ ] Hardware revision prints at boot, if supported.
- [ ] Board profile prints at boot, if supported.
- [ ] Active cutoff status prints at boot.
- [ ] Cutoff simulation status prints at boot.
- [ ] No boot loop.
- [ ] No unexpected reset.
- [ ] No unexpected GPIO behavior observed.

---

## Firmware Safety QA

### Firmware Safety Checklist

- [ ] Active cutoff disabled by default.
- [ ] Unknown board profile defaults to logging-only mode.
- [ ] Unsupported board profile cannot enable active cutoff.
- [ ] Cutoff output does not change state during boot, or is hardware-protected.
- [ ] Cutoff output does not change state during reset, or is hardware-protected.
- [ ] GPIO pins have safe default states.
- [ ] ADC inputs are protected.
- [ ] Inputs do not exceed ESP32 limits.
- [ ] Firmware prints warning if experimental.
- [ ] Firmware prints warning if active cutoff is enabled.
- [ ] Firmware can be reset safely.
- [ ] Firmware can be reflashed safely.
- [ ] Firmware documentation matches behavior.

---

## Bench Functional Test

Bench test before connecting to a PS2.

### Bench Test Checklist

- [ ] Board powers from intended bench supply.
- [ ] Current draw is within expected range.
- [ ] ESP32 boots.
- [ ] Serial output starts.
- [ ] Firmware version is correct.
- [ ] Fault LED works, if installed.
- [ ] Manual reset works, if installed.
- [ ] Mode select works, if installed.
- [ ] Cutoff enable jumper reads correctly, if installed.
- [ ] ADC test input reads correctly.
- [ ] PS11 current input reads safe dummy value.
- [ ] Focus input reads safe dummy signal.
- [ ] Tracking input reads safe dummy signal.
- [ ] No part becomes hot.
- [ ] No unexpected outputs toggle.
- [ ] Board survives reset cycle.
- [ ] Board survives power cycle.

---

## Logging QA

### Serial Logging Checklist

- [ ] Serial monitor connects at correct baud rate.
- [ ] Boot message is readable.
- [ ] Firmware name is shown.
- [ ] Firmware version is shown.
- [ ] Hardware revision is shown, if supported.
- [ ] Operating mode is shown.
- [ ] Active cutoff status is shown.
- [ ] Input readings are displayed.
- [ ] Event messages are displayed.
- [ ] Error messages are understandable.
- [ ] Log format is consistent.
- [ ] Log can be copied into a test report.

### Data Logging Checklist

- [ ] Timestamp is included.
- [ ] Focus activity field exists, if supported.
- [ ] Tracking activity field exists, if supported.
- [ ] PS11 current field exists, if supported.
- [ ] Voltage field exists, if supported.
- [ ] Fault state field exists, if supported.
- [ ] Operating mode field exists.
- [ ] Active cutoff field exists.
- [ ] Data format matches documentation.
- [ ] Log file name follows project naming convention.

---

## Signal Input QA

### Focus Input QA

- [ ] Focus input is protected.
- [ ] Focus input is not directly connected to raw unsafe signal.
- [ ] Signal-conditioning circuit installed.
- [ ] Input voltage range confirmed.
- [ ] Input does not backfeed PS2 circuit.
- [ ] Input reads correctly on bench.
- [ ] Input state logs correctly.
- [ ] No false activity when input is idle.

### Tracking Input QA

- [ ] Tracking input is protected.
- [ ] Tracking input is not directly connected to raw unsafe signal.
- [ ] Signal-conditioning circuit installed.
- [ ] Input voltage range confirmed.
- [ ] Input does not backfeed PS2 circuit.
- [ ] Input reads correctly on bench.
- [ ] Input state logs correctly.
- [ ] No false activity when input is idle.

### PS11 Current Input QA

- [ ] PS11 current input is protected.
- [ ] Input is from conditioned current-sense circuit.
- [ ] Input is not directly connected to unsafe fuse path.
- [ ] ADC range is safe.
- [ ] Raw ADC value logs.
- [ ] Converted current value logs, if supported.
- [ ] Shunt value is documented.
- [ ] Amplifier gain is documented, if used.
- [ ] Zero-current value is checked.
- [ ] Known dummy current test passes, if possible.

---

## Cutoff Hardware QA

This section applies only to hardware revisions that include future cutoff capability.

### Cutoff Disabled QA

- [ ] Cutoff hardware is not populated, or disabled by default.
- [ ] Cutoff enable jumper is not installed by default.
- [ ] Firmware reports active cutoff disabled.
- [ ] Cutoff control output does not activate on boot.
- [ ] Cutoff control output does not activate on reset.
- [ ] Cutoff circuit has safe default state.
- [ ] Manual override works, if installed.
- [ ] Fault LED does not imply active protection if cutoff is disabled.

### Cutoff Enabled QA

Use only for sacrificial or validated test hardware.

- [ ] Sacrificial console selected.
- [ ] Active cutoff firmware intentionally selected.
- [ ] Hardware cutoff enable intentionally installed.
- [ ] Cutoff point verified.
- [ ] Cutoff behavior tested on bench first.
- [ ] Fault indicator works.
- [ ] Manual override works.
- [ ] Cutoff does not chatter.
- [ ] Cutoff does not activate falsely during startup.
- [ ] Cutoff logs event correctly.
- [ ] Recovery behavior documented.

---

## PS2 Development Test QA

Use only after bench tests pass.

### Pre-Console Connection Checklist

- [ ] Console baseline test completed.
- [ ] PS2 model documented.
- [ ] Board revision documented.
- [ ] Driver IC marking documented.
- [ ] PS11 location documented, if used.
- [ ] Laser model documented, if known.
- [ ] Optical-drive assembly documented, if known.
- [ ] Layzr Savre hardware revision documented.
- [ ] Firmware version documented.
- [ ] Active cutoff disabled.
- [ ] Input voltage ranges confirmed.
- [ ] No backfeeding confirmed.
- [ ] Wires insulated.
- [ ] Wires strain-relieved.
- [ ] No mechanical interference.
- [ ] Emergency power-off plan ready.

### First Power-On Checklist

- [ ] Power on with no disc.
- [ ] Console reaches browser.
- [ ] ESP32 boots.
- [ ] Serial logging starts.
- [ ] No abnormal heat.
- [ ] No abnormal sound.
- [ ] No unexpected reset.
- [ ] Optical drive does not behave abnormally.
- [ ] PS11 current reading appears reasonable, if used.
- [ ] Focus activity reading appears reasonable, if used.
- [ ] Tracking activity reading appears reasonable, if used.
- [ ] Active cutoff remains disabled.

### Known-Good Disc Checklist

- [ ] Known-good disc selected.
- [ ] Disc condition documented.
- [ ] Console detects disc.
- [ ] Disc reads normally.
- [ ] Logs are collected.
- [ ] No false fault action occurs.
- [ ] No abnormal heat.
- [ ] No abnormal drive noise.
- [ ] Test data saved.
- [ ] Notes added.

---

## Kit Contents QA

For beta or public kits, verify all included items.

### Kit Contents Checklist

- [ ] Layzr Savre board included.
- [ ] ESP32 board included, if separate.
- [ ] Required wires included.
- [ ] Required connectors included.
- [ ] Current-sense parts included, if applicable.
- [ ] Shunt value correct, if included.
- [ ] Fault LED included, if applicable.
- [ ] Reset button included, if applicable.
- [ ] Cutoff enable jumper included only if appropriate.
- [ ] Insulation material included or recommended.
- [ ] Printed quick-start card included, if used.
- [ ] Documentation link included.
- [ ] Firmware link included.
- [ ] Safety warning included.
- [ ] Kit contents list included.
- [ ] Batch label included.
- [ ] Revision label included.

---

## Documentation QA

Before releasing or sending a kit, documentation must match the hardware.

### Documentation Checklist

- [ ] README updated.
- [ ] PROJECT_STATUS updated.
- [ ] ROADMAP updated, if needed.
- [ ] CHANGELOG updated.
- [ ] SAFETY_AND_LIMITATIONS updated.
- [ ] Firmware README updated.
- [ ] Testing plan updated.
- [ ] Kit assembly concept updated.
- [ ] PS11 current monitoring notes updated.
- [ ] Hardware revision notes added.
- [ ] Firmware version notes added.
- [ ] Supported models documented, if any.
- [ ] Unsupported models documented, if any.
- [ ] Known issues documented.
- [ ] First-power-on checklist included.
- [ ] Troubleshooting notes included.
- [ ] Active cutoff status documented clearly.

---

## Label QA

Labels should prevent confusion.

### Label Checklist

- [ ] Project name shown.
- [ ] Hardware revision shown.
- [ ] Firmware version shown, if flashed.
- [ ] Batch number shown.
- [ ] Date assembled shown.
- [ ] Kit type shown.
- [ ] Experimental or beta status shown, if applicable.
- [ ] Active cutoff status shown, if applicable.
- [ ] QR code or documentation link included, if used.
- [ ] Label is readable.
- [ ] Label is attached securely.

---

## Packaging QA

Packaging should protect the hardware and make the kit easy to understand.

### Packaging Checklist

- [ ] Board placed in anti-static bag.
- [ ] Small parts placed in labeled bags.
- [ ] Sharp pins protected.
- [ ] Connectors protected.
- [ ] Kit contents checklist included.
- [ ] Safety warning included.
- [ ] Documentation link included.
- [ ] Firmware link included, if needed.
- [ ] Label applied.
- [ ] Packaging protects against bending.
- [ ] Packaging protects against moisture as reasonable.
- [ ] Package is clean and presentable.
- [ ] Nothing loose can damage the board during shipping.

---

## Beta Kit QA

Beta kits require extra warnings.

### Beta Kit Checklist

- [ ] Beta status clearly marked.
- [ ] Experimental warning included.
- [ ] Active cutoff disabled unless intentionally part of test.
- [ ] Known risks listed.
- [ ] Known limitations listed.
- [ ] Test instructions included.
- [ ] Feedback instructions included.
- [ ] Required photos listed.
- [ ] Required logs listed.
- [ ] Board revision reporting requested.
- [ ] Tester understands risk.
- [ ] Tester is not using a valuable or customer console.
- [ ] Support channel or contact method included.

---

## Public Kit QA

Public kits should not be released until the project is validated.

### Public Release Checklist

- [ ] Hardware revision stable.
- [ ] Firmware revision stable.
- [ ] Supported models documented.
- [ ] Unsupported models documented.
- [ ] Install guide complete.
- [ ] First-power-on checklist complete.
- [ ] Troubleshooting guide complete.
- [ ] Safety warnings complete.
- [ ] Known limitations complete.
- [ ] QC process complete.
- [ ] Packaging process complete.
- [ ] Labels complete.
- [ ] Website copy reviewed.
- [ ] Etsy copy reviewed.
- [ ] eBay copy reviewed.
- [ ] Support process defined.
- [ ] Return or warranty policy defined.
- [ ] CHANGELOG updated.
- [ ] Release notes created.

---

## Etsy, eBay, and Website Copy QA

Customer-facing copy must be accurate and not overpromise.

### Listing Copy Checklist

- [ ] Does not claim guaranteed laser protection.
- [ ] Does not claim compatibility with every PS2.
- [ ] Does not claim beginner-friendly install unless proven.
- [ ] Does not claim no risk.
- [ ] Does not claim it prevents all damage.
- [ ] Clearly states supported models.
- [ ] Clearly states unsupported or untested models.
- [ ] Clearly states required skill level.
- [ ] Clearly states kit contents.
- [ ] Clearly states what is not included.
- [ ] Clearly states this is for advanced users.
- [ ] Clearly explains current project status.
- [ ] Uses accurate PS11 wording.
- [ ] Uses accurate active cutoff wording.
- [ ] Mentions documentation link.
- [ ] Mentions safety limitations.

---

## Reject Criteria

A board or kit should be rejected or held for rework if any of these are found.

### Reject Conditions

- [ ] Wrong PCB revision.
- [ ] Missing required component.
- [ ] Wrong component value.
- [ ] Solder bridge.
- [ ] Lifted pad.
- [ ] Damaged connector.
- [ ] Short between power and ground.
- [ ] ESP32 does not boot.
- [ ] Firmware version mismatch.
- [ ] Active cutoff enabled unintentionally.
- [ ] Current-sense path unsafe.
- [ ] PS11 fuse protection bypassed unsafely.
- [ ] Signal input unprotected.
- [ ] Board becomes hot on bench.
- [ ] Serial output fails.
- [ ] Documentation does not match hardware.
- [ ] Label missing or incorrect.
- [ ] Kit contents incomplete.
- [ ] Packaging unsafe.

---

## Rework Checklist

If a board needs rework, document the issue.

### Rework Record

- Board serial or batch:
- Hardware revision:
- Issue found:
- Date found:
- Found by:
- Rework performed:
- Parts replaced:
- Firmware reflashed:
- Retested:
- Result:
- Notes:

### Rework QA

- [ ] Rework visually inspected.
- [ ] Continuity checked.
- [ ] Shorts checked.
- [ ] Bench test repeated.
- [ ] Firmware test repeated.
- [ ] Logs saved, if useful.
- [ ] Board marked as reworked, if needed.
- [ ] Rework notes saved.

---

## Final Sign-Off

Use this section before a board or kit is considered ready.

### Final QA Sign-Off

- Project:
- Hardware revision:
- Firmware revision:
- Batch ID:
- Board serial:
- Kit type:
- QA date:
- QA performed by:
- Result:
- Notes:

### Final Checklist

- [ ] PCB inspection passed.
- [ ] Assembly inspection passed.
- [ ] Electrical inspection passed.
- [ ] Firmware flashed.
- [ ] Firmware verified.
- [ ] Bench test passed.
- [ ] Logging test passed.
- [ ] Active cutoff disabled unless intentionally enabled.
- [ ] PS11 current path checked, if applicable.
- [ ] Kit contents checked.
- [ ] Documentation checked.
- [ ] Label checked.
- [ ] Packaging checked.
- [ ] Ready for internal use, beta, or release.

---

## QA Record Template

Use this template for each board or kit.

## QA Record

### Basic Information

- Date:
- QA performed by:
- Batch ID:
- Board serial:
- Hardware revision:
- Firmware revision:
- Kit type:
- Intended use:

### PCB Inspection

- Visual inspection:
- Dimensional inspection:
- Notes:

### Assembly Inspection

- Solder joints:
- Component values:
- Connector orientation:
- Notes:

### Electrical Inspection

- Power-to-ground short check:
- PS11 path check:
- Current-sense path check:
- ESP32 power check:
- Notes:

### Firmware

- Firmware name:
- Firmware version:
- Flash result:
- Boot result:
- Active cutoff status:
- Notes:

### Bench Test

- Power-on result:
- Serial output:
- Input readings:
- Current draw:
- Heat:
- Notes:

### Kit Contents

- Contents complete:
- Labels complete:
- Documentation included:
- Packaging complete:
- Notes:

### Final Result

- Pass:
- Fail:
- Hold for rework:
- Ready for internal testing:
- Ready for beta:
- Ready for release:
- Notes:

---

## Stop Ship Conditions

Do not ship or release a kit if:

- Hardware revision is unclear.
- Firmware revision is unclear.
- Active cutoff status is unclear.
- Documentation is missing.
- Safety warnings are missing.
- PS11 instructions are unclear.
- Kit contents are incomplete.
- Board failed bench test.
- ESP32 firmware does not boot.
- Current-sense path is unsafe.
- Cutoff behavior is untested but enabled.
- Supported models are not documented.
- Listing copy overpromises protection.
- Known safety issue is unresolved.

---

## Current Working Theory

The current working theory is:

- QA should begin during prototype development, not after release.
- Every board should have a known hardware revision.
- Every firmware build should identify itself at boot.
- Active cutoff must be disabled by default during development.
- PS11 current monitoring must preserve the fuse protection role.
- Bench testing should happen before console testing.
- Kit contents should be checked before packaging.
- Documentation must match the hardware being shipped.
- Beta kits need extra warnings.
- Public kits should only be released after validation.

This theory will be updated as the project develops.

---

## Summary

The QA checklist is meant to keep Layzr Savre hardware, firmware, and kits consistent, safe, and traceable.

Every board should be inspected before power.

Every firmware build should be verified before use.

Every kit should be checked before shipping.

The goal is to prevent avoidable mistakes while developing a useful PS2 optical-drive telemetry and protection kit for the community.
