# Bill of materials

Status as of 2026-10-27. "Have" means the part is on hand; "buy" means it still has to be bought.
Photos: `C:\embedded\road-rush-car-components\` (2026-10-27).

## Car

| # | Part | Qty | Status | Notes |
|---|---|---|---|---|
| 1 | NUCLEO-G474RE (MB1367C) | 1 | have | Car MCU. On-board ST-LINK V3 + VCP |
| 2 | L298N dual H-bridge module (red, 2× 220 µF / 35 V on board) | 1 | have | Bipolar output stage: ~2–3 V drop (L298 datasheet, V_CEsat). Has an on-board 78M05 and a 5 V-enable jumper |
| 3 | Micro gear motors, N20 size (metal gearbox) | 2 | have | From the photo. Rated voltage, gear ratio, current: read the label or measure |
| 4 | Panasonic NCR18650B Li-ion | 2 | have | 3400 mAh, 3.6 V nominal, usually **unprotected**. 2S = 7.2 V nominal, 8.4 V full, ~6.0 V cutoff |
| 5 | 2× 18650 holder, side by side | 1 | have | Probably 2S: check with a multimeter |
| 6 | Electrolytic capacitor 1000 µF / 16 V | 2 | have | Bulk capacitance on the motor rail (16 V > 8.4 V, OK) |
| 7 | Wheel, rubber tyre with treads, white hub, D-shaped hole | 2 | have | The D-hole fits the N20 3 mm D-shaft. Diameter and width to measure |
| 7a | Caster (third, support) wheel | 1 | have | Type, full height and mounting holes to measure |
| 8 | BLE module ZS-040, likely HM-10 / CC2541 | 1 | have | Phone control for motor tests. Identity to confirm, see T-007 |
| 9 | nRF24L01+, plain version (PCB antenna, 16 MHz crystal) | 1 | have | Receiver side of the remote link (pair with Remote #3) |
| 10 | Dupont / hook-up wires | set | have | |
| 11 | Wooden test plate | 1 | have | Temporary rig only: Nucleo, battery holder, L298N and both motors mounted and wired. The car pulls to one side on it because the plate and motor mounts are uneven. To be replaced by the 3D-printed chassis |

## Remote

| # | Part | Qty | Status | Notes |
|---|---|---|---|---|
| 1 | Blue Pill STM32F103C8T6 | 1 | have | Replaceable if T-002 can't make flashing reliable. 8 MHz HSE + 32.768 kHz LSE crystals, 4-pin SWD header, BOOT0/BOOT1 jumpers. Chip says STM32F103C8T6 with an ST logo, but markings can be faked: read the IDCODE (T-002) |
| 2 | Analog joystick KY-023 | 2 | have | Board labelled +5V, but power it from **3.3 V** so the outputs stay inside the ADC range. 2 joysticks = 4 ADC channels + 2 buttons |
| 3 | nRF24L01+, plain version (PCB antenna, 16 MHz crystal) | 1 | have | Transmitter side. Plain version: ~12 mA TX at 0 dBm, range tens of metres in the open |
| 4 | ST-LINK V2 clone (green aluminium case) | 1 | have | Has an RST pin (pin 1). Header: 1 RST, 2 SWCLK, 3 SWIM, 4 SWDIO, 5/6 GND, 7/8 3.3 V, 9/10 5 V. On some clones RST is not connected for SWD: test it |

## Missing or unknown

- Battery protection (2S BMS), a Li-ion charger, a power switch, a fuse
- Remote power source (USB power bank, battery + regulator?)
- 10 µF capacitors for the nRF24 VCC (one per module)
- Sensors: none listed yet
- Motor specs, wheel size, 3D printer model and filament
