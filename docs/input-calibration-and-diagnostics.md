# Input Calibration and Diagnostics

Precision controls are only fair while physical intent maps consistently to game input. Treat calibration and subsystem health as production game-design concerns.

## Calibration contract

For every precision input define:
- neutral/center
- min/max range
- dead zone
- response curve
- invalid/out-of-range condition
- reset/recalibrate path
- fallback input

Relevant inputs include touch virtual sticks, gyro, analog gamepads, steering, aiming and rhythm/audio timing offsets.

## Calibration health

A debug view should make drift visible rather than forcing testers to describe controls as merely “weird”. Useful readings include raw and normalized axis values, detected center, dead-zone boundary, touch origin/current point, gyro bias, timestamp/input age and device/input source.

## Maintenance principle

If a mechanic depends heavily on a special capability, provide a cheap health check and a degraded fallback. Optional haptics, gyro or controller support must not make the core game unrecoverable when unavailable.

## Diagnostic separation

Provide dedicated checks for input, audio, network, save/version and procedural/replay state. Diagnose these before changing difficulty or content because infrastructure faults can masquerade as balance problems.

## QA matrix

Test fresh launch, long session, orientation change, background/resume, device rotation, controller reconnect, multi-touch interruption, OS gesture collision and thermal/load pressure. Compare success/miss/correction rates, not only whether an event was received.

## Reset domains

Keep settings reset, calibration reset, save/progression reset, diagnostics/audits clear and competitive-record deletion as separate operations. Label exactly what survives each reset.