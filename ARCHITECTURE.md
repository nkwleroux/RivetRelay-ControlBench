# ControlBench Architecture

## Components

- **Acquisition task:** samples sensors through ADC, encoder, SPI, or I2C.
- **Control task:** executes a fixed-period PID or other deterministic loop.
- **Actuation layer:** updates PWM or simulated outputs.
- **Communication task:** UART diagnostics and optional CANWorks frames.
- **Diagnostics task:** timing statistics, memory use, and health reporting.
- **Safety/watchdog:** detects missed deadlines, stalled tasks, and invalid inputs.

## Boundaries

Application logic depends on abstract driver interfaces. Board-specific code remains in `bsp/` and `platform/`. The control loop must run without CANWorks, HILForge, LinuxEdge, or SecureFleet.

## Data flow

```text
sensor -> acquisition -> control -> actuator
                     \-> diagnostics -> UART/CAN
```

