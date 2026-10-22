# T-002: Make Blue Pill flashing reliable
**Status:** todo
**Depends on:** T-001 (know the programmer hardware)

## Goal
A repeatable, documented way to flash and debug both Blue Pills, with no "erase in CubeProgrammer first" ritual.

## Done when
- [ ] Real chip identity known for both boards (genuine STM32 or a clone, and which one)
- [ ] A working connection method found (try in order):
  1. ST-LINK V2 over SWD, connect under reset (`mode=UR`)
  2. The Nucleo-G474RE ST-LINK V3 as an external programmer (check UM2505)
  3. The ROM UART bootloader (BOOT0=1, USART1 PA9/PA10)
- [ ] OpenOCD config works (with `CPUTAPID` if it's a clone)
- [ ] Wiring documented in `docs/flashing.md` (which programmer pin goes to which board pin)
- [ ] Root cause of the past failure written down

## Probes
Read-only, fine to run:
- `STM32_Programmer_CLI -c port=SWD mode=UR`: connects and prints the device ID, flash size and RDP level

Writes or erases (confirm with the user first):
- `STM32_Programmer_CLI -c port=SWD mode=UR -e all`

## Notes / log
