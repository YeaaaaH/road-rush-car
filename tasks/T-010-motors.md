# T-010: Motors: PWM and direction through the L298N
**Status:** todo
**Depends on:** T-007, T-008, T-009

## Goal
Each motor can be driven forward, backward and stopped at a set speed from firmware. Wheels off the ground first.

## Done when
- [ ] PWM on two channels of one timer (ENA/ENB), frequency chosen and justified (audible whine vs L298N switching losses; start around 1–20 kHz and listen)
- [ ] PSC/ARR worked out from the real timer clock (see the ×2 rule in T-006)
- [ ] Direction on IN1–IN4; brake vs coast understood (both INs equal + EN high = brake; EN low = coast; L298 datasheet truth table)
- [ ] Test sequence over the debug UART: each motor forward / back / stop at a few duty values, wheels off the ground
- [ ] Differential drive mix in `common/`: (throttle, steering) → (left, right), clamped
- [ ] Trim value per motor to correct a small speed mismatch (not a skewed axle: that's the chassis' job)
- [ ] Measured: motor current at a few duty values (multimeter in series), recorded for T-009

## Notes / log
