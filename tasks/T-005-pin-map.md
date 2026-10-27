# T-005: Pin map for car and remote
**Status:** todo
**Depends on:** T-001

## Goal
Pin assignments for both boards, chosen so that the car's pins also exist on the future small G4 package (e.g. STM32G431CB LQFP48).

## Done when
- [ ] Car: L298N (ENA/ENB on PWM channels of one timer, IN1–IN4 on GPIOs), HM-10 on a UART (not the VCP one), nRF24L01+ on SPI + CE + IRQ, sensors, debug UART (the VCP)
- [ ] Remote: 2× KY-023 (4 ADC channels, 2 buttons on GPIOs with pull-up), nRF24L01+ on SPI + CE + IRQ, LED
- [ ] Car: document what is already wired on the wooden test rig (Nucleo ↔ L298N ↔ BLE), and keep or change it on purpose
- [ ] **Failsafe requirement noted:** if no valid command arrives (from BLE or nRF24) within N ms, the car stops the motors
- [ ] PA13/PA14 (SWD) kept free on both boards
- [ ] 5 V-tolerant (FT) pins checked against the datasheet for any 5 V signal
- [ ] Checked for conflicts in CubeMX (planning only)
- [ ] Written to `docs/pinmap.md` with a wiring table

## Notes / log
