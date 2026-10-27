# T-008: Safe car power: BMS, charger, switch, fuse
**Status:** todo
**Depends on:** T-001 (region and stores known)

## Goal
The 2S NCR18650B pack can't be over-discharged, over-charged or shorted, and the car can be switched off.

## Done when
- [ ] Holder wiring checked: 2S (series) or 2P (parallel)
- [ ] 2S BMS chosen: continuous current ≥ the motors' combined stall current through the L298N
- [ ] Charger chosen (2S balance charger, or the BMS with a CC/CV 8.4 V supply)
- [ ] Power switch and fuse rated for the stall current
- [ ] MCU power path decided: L298N 5 V regulator vs a separate buck converter → Nucleo (E5V or 5V pin, see UM2505 power section); nRF24 from the 3.3 V rail
- [ ] Power diagram written to `docs/power.md`

## Notes / log
NCR18650B cells are usually sold unprotected. Until a BMS is fitted: never leave the pack connected unattended, and check the cell voltage (stop at ~3.0 V per cell).
