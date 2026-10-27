# T-015: Radio link remote → car
**Status:** todo
**Depends on:** T-012, T-013, T-014

## Goal
The remote sends command packets; the car receives them with Enhanced ShockBurst auto-ack and retransmit.

## Done when
- [ ] Both ends agree: channel, address width and address, data rate (250 kbps or 1 Mbps; slower = longer range), payload size = the command structure from T-012, CRC 2 bytes
- [ ] Remote in PTX, car in PRX; auto-ack and auto-retransmit set (`SETUP_RETR`)
- [ ] IRQ pin used on the car (RX_DR), so the main loop isn't polling SPI
- [ ] Packet rate chosen (e.g. 50 Hz) and the failsafe N from T-012 checked against it
- [ ] Measured: packet loss at 1 m, across the room, through a wall; logged here

## Notes / log
