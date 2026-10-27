# T-002: Finish dev environment setup
**Status:** todo
**Depends on:** user approval for each install

## Goal
Everything needed to edit, build, flash, debug and model.

## Done when
- [ ] VS Code extensions: `ms-vscode.cpptools`, `ms-vscode.cmake-tools`, `marus25.cortex-debug`, `ms-vscode.vscode-serial-monitor`
- [ ] ST-LINK driver confirmed (Device Manager shows "STMicroelectronics STLink Virtual COM Port" with the Nucleo plugged in)
- [ ] CMSIS: ARM CMSIS Core + ST `cmsis-device-g4` + `cmsis-device-f4` (vendored into the project, versions recorded)
- [ ] SVD files: `STM32G474.svd`, `STM32F411.svd`
- [ ] FreeCAD 1.x
- [ ] Slicer for the user's printer
- [ ] Optional: Python + build123d (only for Claude's own geometry checks)
- [x] Git repo initialised in `road-rush-car/` (2026-10-22, branch `main`, with .gitignore and .gitattributes)

## Notes / log
Already installed 2026-10-21: Arm GCC 14.2.Rel1, CMake 4.4.4, Ninja 1.13.2, OpenOCD xPack 0.12.0, CubeProgrammer 2.22.0, CubeMX. Git and VS Code were already present.
