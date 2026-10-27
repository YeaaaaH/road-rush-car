# T-002: Finish dev environment setup
**Status:** in-progress
**Depends on:** user approval for each install

## Goal
Everything needed to edit, build, flash, debug and model.

## Done when
- [x] VS Code extensions: `ms-vscode.cpptools` 1.34.4, `ms-vscode.cmake-tools` 1.24.42, `marus25.cortex-debug` 1.12.1 (+ its mcu-debug helpers, incl. peripheral-viewer), `ms-vscode.vscode-serial-monitor` 0.13.1. Already installed, found 2026-10-27
- [x] ST drivers in the driver store (2026-10-27): `stlink_dbg_winusb.inf`, `stlink_vcp.inf`, `stlink_bridge_winusb.inf` (2.2.0.0), `stm32bootloader.inf` 1.3.0.0 (the USB DFU driver, needed for the Black Pill)
- [ ] ST-LINK enumerates: Device Manager shows "STMicroelectronics STLink Virtual COM Port" with the Nucleo plugged in
- [x] CMSIS: CMSIS_6 v6.4.0 core + ST `cmsis-device-g4` v1.2.6 + `cmsis-device-f4` v2.6.11, headers only, in `third_party/cmsis/` (2026-10-27). Compile check passed for both chips
- [x] SVD files: official ST `STM32G474.svd`, `STM32F411.svd` in `third_party/svd/` (versions in `third_party/README.md`)
- [ ] FreeCAD 1.x: deferred to C-001
- [ ] Slicer for the user's printer: deferred to C-001 (printer model unknown)
- Dropped: Python + build123d (not needed)
- [x] Git repo initialised in `road-rush-car/` (2026-10-22, branch `main`, with .gitignore and .gitattributes)

## Notes / log
Already installed 2026-10-21: Arm GCC 14.2.Rel1, CMake 4.4.4, Ninja 1.13.2, OpenOCD xPack 0.12.0, CubeProgrammer 2.22.0, CubeMX. Git and VS Code were already present.
