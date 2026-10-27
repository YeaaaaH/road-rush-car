# T-013: Joysticks on the remote (ADC)
**Status:** todo
**Depends on:** T-007, T-008

## Goal
The remote reads both KY-023 joysticks (4 axes, 2 buttons) as clean, calibrated numbers.

## Done when
- [ ] Joysticks powered from **3.3 V**, not 5 V (the ADC input range is 0…VREF+; RM0383 ADC, DS10314 electrical limits)
- [ ] ADC1 in scan mode over the 4 channels, sample time chosen for the pot's source impedance (~10 kΩ)
- [ ] DMA moves the results into an array, so the CPU doesn't poll each channel (RM0383, DMA2 stream/channel table for ADC1)
- [ ] Buttons on GPIOs with pull-up, debounced in software
- [ ] Calibration: centre and end points measured; dead zone around centre; output scaled to the command range from T-012
- [ ] Values printed over the debug UART while moving the sticks

## Notes / log
