# ControlBench

An independently usable real-time control-system project and the primary physical device under test for HILForge.

## Languages

- C for low-level startup, HAL boundaries, and interrupt-facing code.
- C++17 where the selected MCU toolchain supports it for application modules and strong types.
- CMake and linker scripts for builds.
- YAML for configuration and CI.

## Suggested structure

```text
controlbench/
├── app/                 # Tasks and application state machines
├── bsp/                 # Board-specific pins and peripherals
├── cmake/               # MCU toolchains and helper functions
├── config/              # FreeRTOS and product configuration
├── drivers/             # ADC, PWM, encoder, motor, watchdog
├── include/controlbench/
├── platform/            # Pico first; STM32 later
├── src/
├── tests/               # Host unit and target integration tests
├── .gitignore
├── ARCHITECTURE.md
├── CMakeLists.txt
└── README.md
```

## Potential libraries and packages

- FreeRTOS Kernel
- Raspberry Pi Pico SDK for the initial board
- STM32Cube HAL/LL and CMSIS when moving to STM32
- CMSIS-DSP for control or signal-processing routines when useful
- Embedded Template Library (ETL) for bounded embedded containers
- Unity/Ceedling or CppUTest for firmware unit tests
- nanopb only if Protobuf is later justified
- littlefs only if persistent local configuration is required

Avoid adding all libraries initially. The MVP needs the board SDK, FreeRTOS, CMake, and a host-side test framework.

## Independent demonstration

Run the controller with a simulated plant or inexpensive sensor/actuator, then report loop period, jitter, missed deadlines, CPU usage, and injected-fault recovery over UART.

## Integration

- CANWorks supplies the versioned CAN contract.
- HILForge flashes, stimulates, and verifies the device.
- LinuxEdge consumes its telemetry through CANWorks.

