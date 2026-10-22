# T-004: Firmware project skeleton + blinky on both boards
**Status:** todo
**Depends on:** T-002, T-003

## Goal
A minimal bare-metal build for G474 and F103 that the user fully understands: no generated code.

## Done when
- [ ] CMake toolchain file (`-mcpu=cortex-m4 -mfpu=fpv4-sp-d16 -mfloat-abi=hard` for G4, `-mcpu=cortex-m3` for F1)
- [ ] A linker script and startup file per chip, explained section by section (.isr_vector, .text, .data, .bss, stack)
- [ ] Clock setup by hand (G4: HSI16 → PLL up to 170 MHz, with flash wait states and the voltage range set; F1: start on HSI, then optionally HSE 8 MHz → PLL 72 MHz)
- [ ] Blinky: the Nucleo LD2 LED, and the Blue Pill LED on PC13
- [ ] UART "hello" over the Nucleo ST-LINK VCP
- [ ] CMake targets `flash-car`, `flash-remote`, `rescue-remote`
- [ ] `.vscode/tasks.json` and `launch.json` (Cortex-Debug + OpenOCD + SVD)

## Notes / log
