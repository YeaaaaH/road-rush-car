# T-016: Integration: the car drives from the remote (stage 1b done)
**Status:** todo
**Depends on:** T-015

## Goal
The joysticks drive the car over nRF24, with the BLE link still available as a fallback.

## Done when
- [ ] Joystick → command → radio → mix → motors, end to end
- [ ] Source selection on the car decided (e.g. nRF24 has priority; BLE used only when no nRF24 packets arrive)
- [ ] Failsafe tested: remote switched off while driving → car stops within N ms
- [ ] Latency felt acceptable; if not, measured (GPIO toggle on send/receive + logic analyzer)
- [ ] **Stage 1b done:** the car drives from the remote on the floor

## Notes / log
