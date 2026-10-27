# T-005: Black Pill: blinky, flashing and debugging
**Status:** todo
**Depends on:** T-003, the Black Pill bought (STM32F411CEU6; ask the seller for both-side photos, soldered pins; 2 pcs recommended)

## Goal
The same edit → build → flash → debug loop on the remote board, with a tested rescue path. Replaces the Blue Pill (decision 2026-10-27).

## Done when
- [ ] Board checked on arrival (read-only): `STM32_Programmer_CLI -c port=SWD` shows device ID **0x431** (F411) and 512 KB flash
- [ ] SWD wiring to the ST-LINK V2 clone documented: SWDIO, SWCLK, GND, 3V3, and **RST → NRST**. Does connect-under-reset (`mode=UR`) work with this clone?
- [ ] USB DFU checked: hold BOOT0, plug USB (or press NRST) → "STM32 BOOTLOADER" in Device Manager; `STM32_Programmer_CLI -c port=USB1` connects. If DFU doesn't show up, retry with BOOT0 held through a power cycle; some boards also need PA10 not floating
- [ ] Blinky on the PC13 LED (active low), GPIO by hand (`RCC->AHB1ENR` on F4, not AHB2ENR as on G4; RM0383)
- [ ] CMake targets `flash-remote` (OpenOCD, `target/stm32f4x.cfg`) and `rescue-remote` (DFU via CubeProgrammer)
- [ ] F5 in Cortex-Debug works as on the Nucleo
- [ ] `docs/flashing.md` extended with the remote board

## Probes
Read-only, fine to run: `STM32_Programmer_CLI -c port=SWD`, `... -c port=SWD mode=UR`, `... -c port=USB1`.
Writes or erases (confirm with the user first): anything with `-e`, `-w`, `-d`, `-ob`.

## Notes / log
- 2026-10-27: the user decided to replace the Blue Pill with a Black Pill (F411) because of past flashing trouble. The Blue Pill stays as a spare, unused.
