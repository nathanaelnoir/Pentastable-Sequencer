[![KiCad 9](https://img.shields.io/badge/KiCad-9-blue)](https://kicad.org)
[![Schematic v1.0](https://img.shields.io/badge/Sch-v1.0-blueviolet)](KiCad/5%20Step%20Sequencer.kicad_sch)
[![PCB v1.0](https://img.shields.io/badge/PCB-v1.0-blue)](KiCad/5%20Step%20Sequencer.kicad_pcb)
[![PCBs: 1](https://img.shields.io/badge/PCBs-1-brightgreen)](KiCad/5%20Step%20Sequencer.kicad_pcb)
[![Core: Arduino Nano](https://img.shields.io/badge/Core-Arduino%20Nano-00979D?logo=arduino&logoColor=white)](#overview)
[![Format: Eurorack](https://img.shields.io/badge/Format-Eurorack-0093ff)](#overview)
[![License: TBD](https://img.shields.io/badge/License-TBD-lightgrey)](#license--contributing)

# Pentastable Sequencer

Pentastable Sequencer is a 5-step Eurorack sequencer inspired by the Buchla Sound Easel. The project files still carry the working name `5 Step Sequencer`, but the PCB silkscreen and module name are `Pentastable Sequencer`.

## Contents

- Overview
- Features
- Quick start (KiCad 9)
- Files
- Build & assembly notes
- Testing
- License & contributing

## Overview

This repository contains the KiCad 9 design files for Pentastable Sequencer. The module is built around an `Arduino Nano` with a `TL072` handling the analog output stage. Five pots set the sequence voltages, five LEDs show the active step, `TRIG IN` and `RESET IN` let the module sync to the rack, and `CV OUT` plus `TRIG OUT` bring the sequence back out.

The front panel also carries five step toggles, one `TEMPO` pot for the internal clock, one extra pot in the CV output section, and two center-off mode switches wired as `3st / off / 5st` and `FWD / off / RND_TIE`.

Revision in the KiCad title block is `v1.0`, dated `2026-03-13`.

## Features

- 5-step sequencer built around `Arduino Nano v3.x` and `TL072`.
- Five 10 k step pots: `CV1` to `CV5`.
- Five step LEDs for position indication.
- Internal clock with dedicated `TEMPO` control.
- External `TRIG IN` and `RESET IN`.
- Separate `CV OUT` and `TRIG OUT`.
- Five panel toggles tied to the individual stage outputs: `OUT1` to `OUT5`.
- Center-off mode switches for stage count (`3st` / `5st`) and playback behavior (`FWD` / `RND_TIE`).
- Eurorack power sheet using `+12V`, `-12V`, `+5V`, and `GND` on a 16-pin IDC connector.
- Mixed build with SMD passives and ICs plus through-hole panel hardware.

## Quick start

1. Install KiCad 9.
2. Open `KiCad/5 Step Sequencer.kicad_pro`.
3. Review the schematic sheets and board, then run ERC and DRC before generating fabrication files.

## Files

- `KiCad/5 Step Sequencer.kicad_sch` - main schematic
- `KiCad/power.kicad_sch` - Eurorack power sheet
- `KiCad/5 Step Sequencer.kicad_pcb` - PCB
- `KiCad/5 Step Sequencer.kicad_pro` - KiCad project file
- `KiCad/5 Step Sequencer.kicad_prl` - local KiCad project state

Note: this repository currently contains the hardware design files only. There is no Arduino firmware or sketch in the repo.

## Build & assembly notes

- Check `A1` orientation and header alignment before soldering the `Arduino Nano`.
- Check `U1` orientation before soldering the `TL072`.
- Double-check the Eurorack power header orientation before first power-up.
- The panel hardware count is not small: four 3.5 mm jacks, seven potentiometers, seven toggle switches, and five LEDs.
- `SW6` and `SW7` are center-off switches. The schematic note calls this out explicitly because the symbol can look misleading if you read it too quickly.
- The output side uses a buffered CV stage around `U1`, `R7`, `R8`, and the extra panel pot. If you change values there, expect the CV output behavior to change with it.

## Testing

1. Program the `Arduino Nano` with the matching firmware before expecting the module to run. This repository does not include that firmware.
2. Power the module from a current-limited Eurorack supply and verify `+12V`, `-12V`, `+5V`, and `GND` first.
3. Turn the internal `TEMPO` control and confirm the step LEDs advance.
4. Feed a pulse into `TRIG IN` and confirm the sequencer advances from the external trigger.
5. Trigger `RESET IN` and confirm the sequence returns to the first stage.
6. Check `CV OUT` and `TRIG OUT` with a scope or a known-good downstream module.

## License & contributing

No `LICENSE` file has been added to this repository yet. Until that changes, assume the design is shared for reference and not under an explicit open-source license.
