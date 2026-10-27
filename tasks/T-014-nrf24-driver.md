# T-014: nRF24L01+ driver (SPI) on both boards
**Status:** todo
**Depends on:** T-007, T-008

## Goal
Each board talks to its nRF24L01+ over SPI and can read and write its registers reliably. No radio link yet.

## Done when
- [ ] Power: module on 3.3 V with a 10 µF capacitor right at its VCC/GND pins
- [ ] SPI set up by hand on both chips: mode 0 (CPOL=0, CPHA=0), MSB first, ≤ 8 MHz (nRF24L01+ datasheet, SPI timing); CSN by GPIO
- [ ] Register read works: `STATUS` reads 0x0E after power-up; `CONFIG` reads its reset value
- [ ] Register write + read-back works (e.g. `RF_CH`, `SETUP_AW`)
- [ ] One driver API shape for both boards; the register-level part separate per chip, the nRF24 logic (register map, commands) in `common/`
- [ ] Checked with a logic analyzer if anything looks wrong (CSN, SCK, MOSI, MISO)

## Notes / log
