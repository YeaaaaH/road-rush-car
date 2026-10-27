# T-002: Make Blue Pill flashing reliable
**Status:** todo
**Depends on:** T-001 (know the programmer hardware)

## Goal
A repeatable, documented way to flash and debug the Blue Pill (the remote), with no "erase in CubeProgrammer first" ritual.

## Done when
- [ ] Real chip identity known (genuine STM32 or a clone, and which one)
- [ ] A working connection method found (try in order):
  1. ST-LINK V2 over SWD, connect under reset (`mode=UR`)
  2. The Nucleo-G474RE ST-LINK V3 as an external programmer (check UM2505)
  3. The ROM UART bootloader (BOOT0=1, USART1 PA9/PA10)
- [ ] OpenOCD config works (with `CPUTAPID` if it's a clone)
- [ ] Wiring documented in `docs/flashing.md` (which programmer pin goes to which board pin)
- [ ] Root cause of the past failure written down

## Exit if it can't be fixed
The user is fine with replacing the Blue Pill. If no method above gives reliable flash + debug, stop and pick another remote board instead of fighting the clone. The choice goes to `docs/decisions.md`; criteria: SWD that just works with the tools we have, 3.3 V logic, enough ADC channels (4) + SPI, buyable where the user shops.

## Probes
Read-only, fine to run:
- `STM32_Programmer_CLI -c port=SWD mode=UR`: connects and prints the device ID, flash size and RDP level

Writes or erases (confirm with the user first):
- `STM32_Programmer_CLI -c port=SWD mode=UR -e all`

## Notes / log
