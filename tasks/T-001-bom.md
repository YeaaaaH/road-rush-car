# T-001: Collect the full BOM
**Status:** done (2026-10-27). The BOM lives in `docs/bom.md`; the open items below moved to the tasks that need them (see the log).
**Depends on:** the user being home with the parts

## Goal
Know exactly which parts exist, so the pin map, power design and chassis can be planned.

## Done when
- [x] `docs/bom.md` lists every part with its model, key specs and quantity (first version 2026-10-27)
- [ ] Motors: rated voltage, current (running and stall), encoders yes/no, dimensions and mounting holes
- [x] Motor driver model: L298N
- [x] Radio: nRF24L01+ (main), BLE ZS-040 (phone tests)
- [ ] BLE module identity confirmed (HM-10 / CC2541, or an HC-05/06 on a ZS-040 board), see T-011
- [x] nRF24L01+ version: plain (PCB antenna), 2 on hand (from the photo)
- [ ] Sensors: model names (none listed yet)
- [x] Car battery: 2× NCR18650B
- [ ] Car power protection: BMS, charger, switch, fuse (to buy), see T-009
- [ ] Remote power source
- [x] Programmer: ST-LINK V2 clone with an RST pin (whether RST works for SWD: test in T-005)
- [ ] USB-UART adapter: yes/no?
- [ ] Motors (N20 size): label text, rated voltage, gear ratio
- [x] Wheels on hand: 2 drive wheels (D-hole for the N20 shaft) + 1 caster
- [ ] Wheels measured: drive wheel diameter and width; caster type, full height and mounting holes
- [ ] 3D printer model and filament
- [x] Region for buying parts: Ukraine (recorded in `CLAUDE.md`)

## Notes / log
Photos next to a ruler are fine for parts with unclear markings.
- 2026-10-27: first list from the user. The NUCLEO-F446RE in an earlier draft was a mistake; the car board is the NUCLEO-G474RE.
- 2026-10-27: closed. Measurements, printer → C-001. Motor label → T-009. BLE identity → T-011. Power, remote power → T-009. USB-UART adapter → T-007 / T-011. (Task numbers after the 2026-10-27 renumbering.) Sensors dropped until there are any.
- 2026-10-27: photos in `../road-rush-car-components/`. Remote gets 2 joysticks; both nRF24L01+ are on hand. The motors are N20-size; a wooden test rig is already wired.
