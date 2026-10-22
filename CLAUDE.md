# Robot car

A radio-controlled robot car built from scratch: firmware, wiring and a 3D-printed chassis. The workspace rules are in `../CLAUDE.md`.

## Goals
- Bare-metal **register-level C**: no HAL, no LL, no CubeIDE. CMSIS device headers only.
- Learn and understand every peripheral from the reference manual.
- Later: a **custom PCB** with a smaller chip from the same family (candidate: STM32G431CB, LQFP48, same G4 registers), carrying only the peripherals the car needs.

## Hardware (known so far)

| Role | Part | Notes |
|---|---|---|
| Car MCU | **NUCLEO-G474RE** | Cortex-M4F at 170 MHz, 512 KB flash, 128 KB RAM. On-board ST-LINK V3 with a virtual COM port. OpenOCD: `target/stm32g4x.cfg` |
| Remote MCU | **2× Blue Pill STM32F103C8T6** | May be relabelled clones: verify the chip ID. OpenOCD: `target/stm32f1x.cfg`, possibly `set CPUTAPID 0x2ba01477` |
| Remote input | joystick modules | analog, read with the ADC |
| Drive | 2 DC motors + 1 omni/caster wheel | the motor wheels and the caster sit at different heights |
| Radio | Bluetooth module (HC-05 or HC-06?) | HC-05 can act as master on the remote. HC-06 is slave only. nRF24L01+ is the suggested alternative |
| Other | "minor sensors" | still to be listed |
| Programmer | ST-LINK V2 (clone?) | had problems with the Blue Pills in the past, see Flashing |

The full BOM is still to come: see `tasks/T-001-bom.md`. Record it in `docs/bom.md` once known.

## Firmware architecture (planned)
```
robot-car/
├── common/     packet protocol, utilities (no register access)
├── car/        G474: motors (TIM PWM), sensors, radio receive
├── remote/     F103: joysticks (ADC), buttons, radio transmit
├── cmake/      toolchain file, flash/debug targets
├── cad/        FreeCAD models, exported STEP/STL
├── docs/       BOM, pin maps, decisions
└── tasks/      technical tasks (see tasks/README.md)
```
- **G4 and F1 GPIO are different generations.** G4 uses `MODER`, `OTYPER`, `OSPEEDR`, `PUPDR` and `AFR`. F1 uses `CRL`/`CRH` plus `AFIO`. Register drivers are written separately for each chip. Only `common/` is shared.
- Build: CMake + Ninja + arm-none-eabi-gcc. Debug: VS Code + Cortex-Debug + OpenOCD, with SVD files for the register views.

## Daily loop
edit → `cmake --build build` → flash (OpenOCD, or F5 in Cortex-Debug) → observe (Serial Monitor over the ST-LINK VCP, debugger register views, logic analyzer) → small git commit.

## Flashing: its own topic
The Blue Pills in the past could not be reflashed from CubeIDE until they were erased in CubeProgrammer. Likely causes, in order:
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
- First part: the **motor bracket** (practice part and fit test). Print test pieces before the full body.
- Unknown: printer model, filament, part measurements.

## Status (2026-10-22)
Toolchain installed (see `../CLAUDE.md`). Everything else waits until the user is home with the hardware: see `tasks/`.
