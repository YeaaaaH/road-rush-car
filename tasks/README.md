# Technical tasks

One file per task: `T-NNN-short-name.md`. The status is kept in the file and mirrored in the table below.

Statuses: `todo` · `in-progress` · `blocked` · `done`

| ID | Task | Status | Depends on |
|---|---|---|---|
| T-001 | [Collect the full BOM](T-001-bom.md) | in-progress | user at home |
| T-002 | [Make Blue Pill flashing reliable](T-002-flash-bluepill.md) | todo | T-001 |
| T-003 | [Finish dev environment setup](T-003-dev-env.md) | todo | user approval |
| T-004 | [Firmware project skeleton + blinky on both boards](T-004-skeleton.md) | todo | T-002, T-003 |
| T-005 | [Pin map for car and remote](T-005-pin-map.md) | todo | T-001 |
| T-006 | [Motor bracket in FreeCAD (first CAD part)](T-006-motor-bracket.md) | todo | T-001, FreeCAD installed |
| T-007 | [Identify the BLE module and talk to it from a phone](T-007-ble-module.md) | todo | user at home |
| T-008 | [Safe car power: BMS, charger, switch, fuse](T-008-car-power.md) | todo | T-001 (stores known) |

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
