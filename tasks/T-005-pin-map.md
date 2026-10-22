# T-005: Pin map for car and remote
**Status:** todo
**Depends on:** T-001

## Goal
Pin assignments for both boards, chosen so that the car's pins also exist on the future small G4 package (e.g. STM32G431CB LQFP48).

## Done when
- [ ] Car: motor PWM timer channels and direction GPIOs, radio UART/SPI, sensors, debug UART (the VCP)
- [ ] Remote: joystick ADC channels, buttons, radio, LED
- [ ] PA13/PA14 (SWD) kept free on both boards
- [ ] 5 V-tolerant (FT) pins checked against the datasheet for any 5 V signal
- [ ] Checked for conflicts in CubeMX (planning only)
- [ ] Written to `docs/pinmap.md` with a wiring table

## Notes / log
