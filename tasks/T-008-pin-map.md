# T-008: Pin map for car and remote
**Status:** todo
**Depends on:** T-004, T-005 (both boards in hand)

## Goal
Pin assignments for both boards, chosen so that the car's pins also exist on the future small G4 package (e.g. STM32G431CB LQFP48).

## Done when
- [ ] Car: L298N (ENA/ENB on PWM channels of one timer, IN1–IN4 on GPIOs), HM-10 on a UART (not the VCP one), nRF24L01+ on SPI + CE + IRQ, debug UART (the VCP)
- [ ] Car: document what is already wired on the wooden test rig (Nucleo ↔ L298N ↔ BLE), and keep or change it on purpose
- [ ] Remote (F411): 2× KY-023 on 4 ADC channels (ADC1 inputs are on PA0–PA7, PB0, PB1), 2 buttons on GPIOs with pull-up, nRF24L01+ on SPI + CE + IRQ, debug UART, LED PC13. Watch for overlaps: SPI1 default pins PA5–PA7 are also ADC inputs; PA0 is the board's KEY button
- [ ] **Failsafe requirement noted:** if no valid command arrives (from BLE or nRF24) within N ms, the car stops the motors
- [ ] PA13/PA14 (SWD) kept free on both boards
- [ ] 5 V-tolerant (FT) pins checked against the datasheet for any 5 V signal (DS12288 for G474, DS10314 for F411)
- [ ] Checked for conflicts in CubeMX (planning only)
- [ ] Written to `docs/pinmap.md` with a wiring table

## Notes / log
