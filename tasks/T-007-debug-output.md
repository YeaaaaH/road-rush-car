# T-007: Debug output (UART) on both boards
**Status:** todo
**Depends on:** T-006

## Goal
Both boards can print text, so every later driver can be checked with numbers, not guesses.

## Done when
- [ ] Car: LPUART1 or USART2 to the ST-LINK V3 VCP (check which one in UM2505 / the board schematic), 115200 8N1, "hello" in the VS Code Serial Monitor
- [ ] Remote: USART1 or USART2 to a USB-UART adapter (is there one? if not, decide: buy one, or use only the debugger's variable view)
- [ ] Baud-rate math written out for both (`BRR` from the peripheral clock). Note the register difference: F4 USART uses `SR`/`DR`, G4 uses `ISR`/`ICR`/`RDR`/`TDR`
- [ ] A small `printf`-style or `print_int` helper in `common/` (no register access there)
- [ ] Transmit doesn't block the main loop for long (polling is fine for now; note where an interrupt or DMA would help later)

## Notes / log
