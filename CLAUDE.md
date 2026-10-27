# Robot car

A radio-controlled robot car built from scratch: firmware, wiring and a 3D-printed chassis. The workspace rules are in `../CLAUDE.md`.

## Goals
- Bare-metal **register-level C**: no HAL, no LL, no CubeIDE. CMSIS device headers only.
- Learn and understand every peripheral from the reference manual.
- Later: a **custom PCB** with a smaller chip from the same family (candidate: STM32G431CB, LQFP48, same G4 registers), carrying only the peripherals the car needs.

## Stages
1. **Breadboard MVP**: Nucleo + Black Pill + modules on wires, in two steps:
   - **1a. Phone over BLE:** the car takes commands from a smartphone through the HM-10 (UART). Used to bring up and test the motors before the remote exists.
   - **1b. Own remote over nRF24:** Black Pill + 2 joysticks + nRF24L01+ talks to an nRF24L01+ on the car. Done when the car drives from the remote, with the failsafe working.
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
| Remote MCU | **Black Pill STM32F411CEU6** (to buy) | Cortex-M4F at 100 MHz, 512 KB flash, 128 KB RAM. HSE 25 MHz, LED on PC13 (active low), KEY button on PA0, BOOT0 button, USB with ROM DFU bootloader. OpenOCD: `target/stm32f4x.cfg`. Verify the chip on arrival: device ID 0x431. Replaces the Blue Pill F103 (decision 2026-10-27), which stays as an unused spare |
| Remote input | 2× KY-023 analog joystick | each: 2 pots (ADC) + push button. Power from 3.3 V, not 5 V |
| Drive | 2 N20-size micro gear motors, L298N driver | L298N drops ~2–3 V, so the motors see well under the battery voltage |
| Car power | 2× NCR18650B (2S, 7.2 V nominal, 8.4 V full), 2× 1000 µF / 16 V | Cells usually unprotected: BMS, charger, switch and fuse still missing |
| Radio, main | 2× nRF24L01+, plain PCB-antenna version (SPI) | one on the car, one on the remote. VCC 3.3 V only, 10 µF at the module |
| Radio, test | BLE ZS-040, likely HM-10 / CC2541 (UART) | On the car, for phone control (stage 1a). BLE, not classic Bluetooth: needs a BLE app on the phone |
| Wheels | 2 rubber-tyred drive wheels (D-hole for the N20 shaft) + 1 caster | all on hand; the drive wheels and the caster sit at different heights |
| Other | sensors | none listed yet |
| Programmer | ST-LINK V2 clone (green aluminium case, has an RST pin) | for the Black Pill over SWD. See Flashing |

Full list with status: `docs/bom.md`. Photos: `../road-rush-car-components/`. Missing measurements are collected in the task that needs them (C-001 for CAD, T-009 for power).
A wooden test plate already carries the Nucleo, the battery holder, the L298N and both motors, wired up. Good enough for stage 1a bench tests (wheels off the ground or short runs), but the car pulls to one side on it because the plate and mounts are uneven. The 3D-printed chassis replaces it.

## Firmware architecture (planned)
```
road-rush-car/
├── common/     packet protocol, utilities (no register access)
├── car/        G474: motors (TIM PWM), BLE (UART), nRF24 receive (SPI), sensors
├── remote/     F411: joysticks (ADC + DMA), buttons, nRF24 transmit (SPI)
├── cmake/      toolchain file, flash/debug targets
├── cad/        FreeCAD models, exported STEP/STL
├── docs/       BOM, pin maps, decisions
└── tasks/      technical tasks (see tasks/README.md)
```
- **G4 and F4 are close but not the same.** GPIO has the same layout on both (`MODER`, `OTYPER`, `OSPEEDR`, `PUPDR`, `AFR`), but the clock enable bits sit in different registers (GPIO: `AHB2ENR` on G4, `AHB1ENR` on F4). RCC/PLL, flash latency, ADC and USART differ (F4 USART: `SR`/`DR`; G4: `ISR`/`ICR`/`RDR`/`TDR`). Reference manuals: RM0440 (G4), RM0383 (F411). Register drivers are written per chip. Only `common/` is shared.
- The car's command handling must not care whether a command came from BLE or nRF24: both feed the same command structure from `common/`, and both go through the same failsafe timeout.
- Build: CMake + Ninja + arm-none-eabi-gcc. Debug: VS Code + Cortex-Debug + OpenOCD, with SVD files for the register views.

## Daily loop
edit → `cmake --build build` → flash (OpenOCD, or F5 in Cortex-Debug) → observe (Serial Monitor over the ST-LINK VCP, debugger register views, logic analyzer) → small git commit.

## Flashing: its own topic
The Nucleo is flashed with its on-board ST-LINK V3; the Black Pill with the ST-LINK V2 clone over SWD (wire RST → NRST too).

Lessons from the Blue Pill (it could not be reflashed until erased in CubeProgrammer):
1. Firmware that reconfigures PA13/PA14 kills SWD. **Rule: never use PA13/PA14 as GPIO or for any other function, on either board.**
2. If SWD is dead, connect under reset (`mode=UR`) still works, but only if NRST is wired (or RESET is held by hand).
3. Clone chips can have a different IDCODE. Check the device ID on every new board.
4. Missing common GND or bad power.

Rescue for the Black Pill, in order: `STM32_Programmer_CLI -c port=SWD mode=UR -e all`; then the ROM **USB DFU** bootloader (hold BOOT0, reset or replug → `-c port=USB1`), which works whatever the firmware did but gives no debugging. If DFU doesn't enumerate, retry with BOOT0 held through a power cycle.
Planned CMake targets: `flash-car`, `flash-remote` (with connect-under-reset), `rescue-remote` (DFU).
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
Toolchain installed (see `../CLAUDE.md`). BOM known (`docs/bom.md`). Remote link decided: nRF24L01+ as the main radio, HM-10 BLE for phone tests. Remote board: Black Pill F411 (to buy). Task plan reordered into phases A–D (`tasks/README.md`). Next: T-002 dev environment.
