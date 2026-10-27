# Third-party files

Copied in unchanged, only the files this project needs. Update on purpose, in a separate commit, and change this table.

| Folder | Source | Version | Commit | License |
|---|---|---|---|---|
| `cmsis/core/` | [ARM-software/CMSIS_6](https://github.com/ARM-software/CMSIS_6) `CMSIS/Core/Include/` (Cortex-M4 files + `m-profile/`) | v6.4.0 | `af1b110e46a1720349f6f125e386e126767699bd` | Apache-2.0 |
| `cmsis/device-g4/` | [STMicroelectronics/cmsis-device-g4](https://github.com/STMicroelectronics/cmsis-device-g4) `Include/` | v1.2.6 | `25664ddc3a7624ae9627ae8c4c672073dc5b2539` | Apache-2.0 |
| `cmsis/device-f4/` | [STMicroelectronics/cmsis-device-f4](https://github.com/STMicroelectronics/cmsis-device-f4) `Include/` | v2.6.11 | `0fa0e489e053fa1ca7790bb40b4d76458f64c55d` | Apache-2.0 |
| `svd/STM32G474.svd` | [modm-io/cmsis-svd-stm32](https://github.com/modm-io/cmsis-svd-stm32) `stm32g4/` (ST's official SVD, line endings normalised) | file v2.9 (G4 pack v3.0) | `e79021accd49bf19bd0b16065f5471fb073ff3ac` | Apache-2.0 |
| `svd/STM32F411.svd` | same repo, `stm32f4/` | file v1.9 (F4 pack v2.0) | same | Apache-2.0 |

Fetched 2026-10-27.

## Usage
- Include paths: `cmsis/core` plus `cmsis/device-g4` (car) or `cmsis/device-f4` (remote).
- Chip define: `-DSTM32G474xx` (car), `-DSTM32F411xE` (remote). It selects the right register header from `stm32g4xx.h` / `stm32f4xx.h`.
- Not copied on purpose: ST's startup files and `system_*.c` templates. The project writes its own startup and clock code (T-003, T-006). The `system_*.h` headers are kept only because the device headers include them.
- SVD files are for the debugger's register view (Cortex-Debug `svdFile`).

## Why not the cmsis-svd-data SVDs
The community copies in `cmsis-svd/cmsis-svd-data` were checked first: the F411 file there declares `fpuPresent=false` and `nvicPrioBits=3`, which is wrong (the F411 has an FPU and 4 priority bits, PM0214). The official ST files declare both correctly.
