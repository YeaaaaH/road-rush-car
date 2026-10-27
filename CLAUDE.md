# Robot car

A radio-controlled robot car built from scratch: firmware, wiring and a 3D-printed chassis. The workspace rules are in `../CLAUDE.md`.

## Goals
- Bare-metal **register-level C**: no HAL, no LL, no CubeIDE. CMSIS device headers only.
- Learn and understand every peripheral from the reference manual.
- Later: a **custom PCB** with a smaller chip from the same family (candidate: STM32G431CB, LQFP48, same G4 registers), carrying only the peripherals the car needs.

## Stages
1. **Breadboard MVP**: Nucleo + Blue Pill + modules on wires, in two steps:
   - **1a. Phone over BLE:** the car takes commands from a smartphone through the HM-10 (UART). Used to bring up and test the motors before the remote exists.
   - **1b. Own remote over nRF24:** Blue Pill + joystick + nRF24L01+ talks to an nRF24L01+ on the car. Done when the car drives from the remote, with the failsafe working.
2. **Engineering prototype**: printed chassis, wiring tidied (perfboard or connectors), power system final, runtime measured.
3. **Custom PCB**: KiCad, STM32G431-class chip, SWD header, only the needed peripherals. Firmware ported from the Nucleo.

Work on the current stage. Bring up the next one only when the current one's exit criteria are met or the user asks.

## Planning rule
Every plan or design proposal ends with its **2–4 biggest risks**, one line each (power, flashing/debug access, parts availability, mechanical fit, learning curve...).

## Parts sourcing
Region: Ukraine. Stores: ask the user.

## Hardware (known so far)

| Role | Part | Notes |
|---|---|---|
| Car MCU | **NUCLEO-G474RE** | Cortex-M4F at 170 MHz, 512 KB flash, 128 KB RAM. On-board ST-LINK V3 with a virtual COM port. OpenOCD: `target/stm32g4x.cfg` |
| Remote MCU | **Blue Pill STM32F103C8T6** | Replaceable: if T-002 can't make flashing reliable, the remote moves to another board. May be a relabelled clone: verify the chip ID. OpenOCD: `target/stm32f1x.cfg`, possibly `set CPUTAPID 0x2ba01477` |
| Remote input | 2× KY-023 analog joystick | each: 2 pots (ADC) + push button. Power from 3.3 V, not 5 V |
| Drive | 2 N20-size micro gear motors, L298N driver | L298N drops ~2–3 V, so the motors see well under the battery voltage |
| Car power | 2× NCR18650B (2S, 7.2 V nominal, 8.4 V full), 2× 1000 µF / 16 V | Cells usually unprotected: BMS, charger, switch and fuse still missing |
| Radio, main | 2× nRF24L01+, plain PCB-antenna version (SPI) | one on the car, one on the remote. VCC 3.3 V only, 10 µF at the module |
| Radio, test | BLE ZS-040, likely HM-10 / CC2541 (UART) | On the car, for phone control (stage 1a). BLE, not classic Bluetooth: needs a BLE app on the phone |
| Wheels | 2 rubber-tyred drive wheels (D-hole for the N20 shaft) + 1 caster | all on hand; the drive wheels and the caster sit at different heights |
| Other | sensors | none listed yet |
| Programmer | ST-LINK V2 clone (green aluminium case, has an RST pin) | for the Blue Pill. Had problems with Blue Pills in the past, see Flashing |

Full list with status: `docs/bom.md`. Photos: `../road-rush-car-components/`. Still open: see `tasks/T-001-bom.md`.
A wooden test plate already carries the Nucleo, the battery holder, the L298N and both motors, wired up. Good enough for stage 1a bench tests (wheels off the ground or short runs), but the car pulls to one side on it because the plate and mounts are uneven. The 3D-printed chassis replaces it.

## Firmware architecture (planned)
```
road-rush-car/
├── common/     packet protocol, utilities (no register access)
├── car/        G474: motors (TIM PWM), BLE (UART), nRF24 receive (SPI), sensors
├── remote/     F103: joystick (ADC), button, nRF24 transmit (SPI)
├── cmake/      toolchain file, flash/debug targets
├── cad/        FreeCAD models, exported STEP/STL
├── docs/       BOM, pin maps, decisions
└── tasks/      technical tasks (see tasks/README.md)
```
- **G4 and F1 GPIO are different generations.** G4 uses `MODER`, `OTYPER`, `OSPEEDR`, `PUPDR` and `AFR`. F1 uses `CRL`/`CRH` plus `AFIO`. Register drivers are written separately for each chip. Only `common/` is shared.
- The car's command handling must not care whether a command came from BLE or nRF24: both feed the same command structure from `common/`, and both go through the same failsafe timeout.
- Build: CMake + Ninja + arm-none-eabi-gcc. Debug: VS Code + Cortex-Debug + OpenOCD, with SVD files for the register views.

## Daily loop
edit → `cmake --build build` → flash (OpenOCD, or F5 in Cortex-Debug) → observe (Serial Monitor over the ST-LINK VCP, debugger register views, logic analyzer) → small git commit.

## Flashing: its own topic
The Blue Pill is flashed with the ST-LINK V2, the Nucleo with its on-board ST-LINK V3. Blue Pills in the past could not be reflashed from CubeIDE until they were erased in CubeProgrammer. Likely causes, in order:
1. The firmware disabled SWD. CubeMX's F103 default `SYS → Debug: No Debug` remaps PA13/PA14. **Rule: never touch `AFIO->MAPR.SWJ_CFG` and never use PA13/PA14.**
2. The ST-LINK V2 clone has no RST wired, so connect-under-reset fails. Hold RESET manually, or wire NRST.
3. The chip is a clone with a different IDCODE (OpenOCD needs `CPUTAPID`).
4. Missing common GND or bad power.

Rescue: `STM32_Programmer_CLI -c port=SWD mode=UR -e all`. Fallback: the F103 ROM UART bootloader (BOOT0=1, USART1 PA9/PA10, `-c port=COMx`), which works even with SWD locked but gives no debugging.
Planned CMake targets: `flash-car`, `flash-remote` (with connect-under-reset), `rescue-remote`.
Still to check: whether the Nucleo-G474RE's ST-LINK V3 can program external boards (UM2505).

## Chassis (3D print)
- **FreeCAD**: the user models by hand to refresh their engineering-design skills. Claude acts as mentor and reviewer: sets tasks with requirements, gives hints, checks fits and tolerances, does the calculations. Don't model for them unless asked.
- Concept: a **flat base plate**. The height difference is absorbed by the motor brackets and a caster spacer:
  `spacer = (wheel radius − distance from base to motor axle) − caster height`. If the result is negative, recess the caster into the base.
- FDM rules: M3 clearance hole 3.2–3.4 mm, fit clearance 0.2–0.3 mm per side (calibrate with a test print), heat-set inserts instead of printed threads, avoid overhangs over ~45°, orient the part so loads don't split layers.
- **Straight driving is a mechanical requirement first.** The test rig pulls to one side: the two motor axles must be coaxial and parallel to the base, both wheels must touch the ground with the same load, and the caster must not lift a drive wheel. Firmware trim can correct a small speed mismatch between the motors, not a skewed axle.
- First part: the **motor bracket** (practice part and fit test). Print test pieces before the full body.
- Unknown: printer model, filament, part measurements (motors, wheels, caster).

## Status (2026-10-27)
Toolchain installed (see `../CLAUDE.md`). BOM mostly known (`docs/bom.md`). Remote link decided: nRF24L01+ as the main radio, HM-10 BLE for phone tests. Next: the open BOM items and the dev environment, see `tasks/`.
