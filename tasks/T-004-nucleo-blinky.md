# T-004: Nucleo: blinky, flashing and debugging
**Status:** todo
**Depends on:** T-003

## Goal
The full edit → build → flash → debug loop works on the car board, through its on-board ST-LINK V3.

## Done when
- [ ] Blinky on LD2 (PA5) at the reset clock, GPIO set up by hand (`RCC->AHB2ENR`, `MODER`, `ODR`/`BSRR`; RM0440)
- [ ] Read-only probe: `STM32_Programmer_CLI -c port=SWD` shows the G474 device ID (0x469)
- [ ] CMake target `flash-car` (OpenOCD, `target/stm32g4x.cfg`)
- [ ] `.vscode/tasks.json` + `launch.json`: F5 flashes and stops at `main`
- [ ] In Cortex-Debug: a breakpoint hits, stepping works, `GPIOA->ODR` changes in the SVD register view
- [ ] Written down in `docs/flashing.md`: how the car board is flashed and debugged

## Notes / log
