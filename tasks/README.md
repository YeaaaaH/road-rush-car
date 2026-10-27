# Technical tasks

One file per task: `T-NNN-short-name.md` for firmware and electronics, `C-NNN-short-name.md` for the chassis (CAD and printing). The status is kept in the file and mirrored in the tables below.

Statuses: `todo` · `in-progress` · `blocked` · `done`

## Firmware and electronics

Each task builds only on something already tested.

| ID | Task | Status | Depends on |
|---|---|---|---|
| T-001 | [Collect the BOM](T-001-bom.md) | done | — |
| **A. Tools and flashing** | | | |
| T-002 | [Finish dev environment setup](T-002-dev-env.md) | todo | user approval |
| T-003 | [Firmware project skeleton (build only)](T-003-skeleton.md) | todo | T-002 |
| T-004 | [Nucleo: blinky, flashing and debugging](T-004-nucleo-blinky.md) | todo | T-003 |
| T-005 | [Black Pill: blinky, flashing and debugging](T-005-blackpill-blinky.md) | todo | T-003, Black Pill bought |
| **B. Chip setup** | | | |
| T-006 | [System clocks and SysTick](T-006-clocks.md) | todo | T-004, T-005 |
| T-007 | [Debug output (UART) on both boards](T-007-debug-output.md) | todo | T-006 |
| T-008 | [Pin map for car and remote](T-008-pin-map.md) | todo | T-004, T-005 |
| **C. Car, stage 1a (phone over BLE)** | | | |
| T-009 | [Safe car power: BMS, charger, switch, fuse](T-009-car-power.md) | todo | — (before T-010) |
| T-010 | [Motors: PWM and direction through the L298N](T-010-motors.md) | todo | T-007, T-008, T-009 |
| T-011 | [BLE module: identify it and receive phone data](T-011-ble-module.md) | todo | T-007, T-008 |
| T-012 | [Command protocol and failsafe (stage 1a done)](T-012-commands-failsafe.md) | todo | T-010, T-011 |
| **D. Remote and radio, stage 1b** | | | |
| T-013 | [Joysticks on the remote (ADC)](T-013-joysticks.md) | todo | T-007, T-008 |
| T-014 | [nRF24L01+ driver (SPI) on both boards](T-014-nrf24-driver.md) | todo | T-007, T-008 |
| T-015 | [Radio link remote → car](T-015-radio-link.md) | todo | T-012, T-013, T-014 |
| T-016 | [Integration: the car drives from the remote (stage 1b done)](T-016-integration.md) | todo | T-015 |

## Chassis (parallel track)

| ID | Task | Status | Depends on |
|---|---|---|---|
| C-001 | [Motor bracket in FreeCAD (first CAD part)](C-001-motor-bracket.md) | todo | FreeCAD installed |

## Task file template
```markdown
# T-NNN: Title
**Status:** todo
**Depends on:** ...

## Goal
## Done when
- [ ] ...
## Notes / log
```
