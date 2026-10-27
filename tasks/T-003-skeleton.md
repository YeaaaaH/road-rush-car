# T-003: Firmware project skeleton (build only)
**Status:** todo
**Depends on:** T-002

## Goal
A minimal bare-metal build for the G474 (car) and the F411 (remote) that the user fully understands: no generated code. This task only has to **build**; flashing is T-004 and T-005.

## Done when
- [ ] Folder layout from `../CLAUDE.md` (`car/`, `remote/`, `common/`, `cmake/`)
- [ ] CMake toolchain file. Both chips are Cortex-M4F: `-mcpu=cortex-m4 -mfpu=fpv4-sp-d16 -mfloat-abi=hard`
- [ ] A linker script and startup file per chip, explained section by section (.isr_vector, .text, .data, .bss, stack). Memory: G474RE 512 KB flash / 128 KB SRAM; F411CE 512 KB flash / 128 KB SRAM
- [ ] The FPU enabled in the startup code (`SCB->CPACR`, CP10/CP11 full access) before any float instruction runs
- [ ] An empty `main` on the reset clock (G4: HSI16; F4: HSI 16 MHz) builds for both targets with no warnings
- [ ] `.map` file read together: where `.text`, `.data`, `.bss` and the stack ended up

## Notes / log
