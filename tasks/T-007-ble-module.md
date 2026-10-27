# T-007: Identify the BLE module and talk to it from a phone
**Status:** todo
**Depends on:** the user being home with the module

## Goal
Know which chip is on the ZS-040 board, and have a working phone ↔ module serial link before any car firmware uses it (stage 1a).

## Done when
- [ ] Chip identified from the board: CC2541 (HM-10 class, BLE) or BC417 / similar (HC-05/06, classic Bluetooth)
- [ ] Module VCC range and RX logic level confirmed (the breakout's regulator, and whether RX needs a divider from 5 V; from a 3.3 V MCU it does not)
- [ ] AT test passes over a USB-UART adapter or the Nucleo VCP pass-through (HM-10: `AT` with no line ending → `OK`; default 9600 baud)
- [ ] Phone app chosen that speaks BLE UART (e.g. "Serial Bluetooth Terminal" in BLE mode); text sent from the phone shows up on the UART
- [ ] Results written to `docs/bom.md`

## Notes / log
Clones of HM-10 (e.g. with a different firmware) answer AT commands differently: log the exact replies.
