# T-006: System clocks and SysTick
**Status:** todo
**Depends on:** T-004, T-005

## Goal
Both chips run at their target speed, set by hand, and there is a millisecond time base for everything after this.

## Done when
- [ ] G474: HSI16 → PLL → **170 MHz**. Before raising the clock: flash wait states (`FLASH->ACR.LATENCY`), Range 1 boost mode (`PWR->CR5.R1MODE`), and the AHB /2 step for the transition (RM0440, RCC and PWR sections)
- [ ] F411: HSE 25 MHz → PLL (M=25, N=200, P=2) → **100 MHz**. Flash 3 wait states, voltage scale 1, APB1 /2 (max 50 MHz) (RM0383, RCC; flash latency table)
- [ ] Clock checked on a pin: MCO output measured with a logic analyzer or scope, or blink period checked against a stopwatch
- [ ] SysTick at 1 kHz on both boards, `millis()` style counter; blinky rewritten with it
- [ ] The timer clock rule written down for later: if the APB prescaler ≠ 1, timers get 2× the APB clock

## Notes / log
