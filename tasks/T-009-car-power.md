# T-009: Safe car power: BMS, charger, switch, fuse
**Status:** todo
**Depends on:** nothing to start (buying can begin now); must be **done before T-010** runs the motors from the battery

## Goal
The 2S NCR18650B pack can't be over-discharged, over-charged or shorted, and the car can be switched off.

## Done when
- [ ] Holder wiring checked: 2S (series) or 2P (parallel)
- [ ] Motor label read: rated voltage and gear ratio; stall current measured or taken from the datasheet
- [ ] 2S BMS chosen: continuous current ≥ the motors' combined stall current through the L298N
- [ ] Charger chosen (2S balance charger, or the BMS with a CC/CV 8.4 V supply)
- [ ] Power switch and fuse rated for the stall current
- [ ] MCU power path decided: L298N 5 V regulator vs a separate buck converter → Nucleo (E5V or 5V pin, see UM2505 power section); nRF24 from the 3.3 V rail
- [ ] Remote power source chosen (USB power bank, or a cell + regulator)
- [ ] Power diagram written to `docs/power.md`

## Notes / log
NCR18650B cells are usually sold unprotected. Until a BMS is fitted: never leave the pack connected unattended, and check the cell voltage (stop at ~3.0 V per cell).
