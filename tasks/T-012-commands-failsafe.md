# T-012: Command protocol and failsafe (stage 1a done)
**Status:** todo
**Depends on:** T-010, T-011

## Goal
One command format for both links (BLE now, nRF24 later), and a car that stops by itself when commands stop arriving.

## Done when
- [ ] Command structure in `common/`: throttle, steering, buttons, a sequence number; fixed size; a checksum or CRC
- [ ] Text form for the phone (e.g. a short line the BLE terminal can send from its buttons) parsed into the same structure
- [ ] Failsafe: no valid command for N ms → motors stop. N chosen and justified (packet rate × a few missed packets)
- [ ] Failsafe tested: switch the phone's Bluetooth off while driving with the wheels off the ground → motors stop within N ms
- [ ] **Stage 1a done:** the car drives from the phone on the floor

## Notes / log
