# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is an embedded C project for the S32K144 microcontroller, featuring a hello world LED/GPIO demonstration application. The project uses NXP's S32 Design Studio IDE and S32 SDK framework.

## Architecture

**Target Platform**: NXP S32K144 Cortex-M4 microcontroller
**Build System**: Eclipse CDT with ARM GCC toolchain
**SDK**: S32 SDK S32K1xx RTM 3.0.0
**IDE**: S32 Design Studio v2.2

### Project Structure

```
hello_world_s32k144/
├── Sources/main.c              # Application entry point
├── Generated_Code/             # Processor Expert generated code
│   ├── Cpu.c/h                # CPU initialization 
│   ├── clockMan1.c/h          # Clock manager configuration
│   └── pin_mux.c/h            # Pin multiplexing configuration
├── SDK/                       # S32 SDK platform drivers
│   └── platform/
│       ├── devices/           # Device-specific headers/startup
│       └── drivers/           # Hardware abstraction layer
├── Debug_FLASH/               # Build output directory
│   └── makefile              # Generated build configuration
└── Documentation/             # Generated API documentation
```

### Key Components

- **Processor Expert Integration**: Code generation system for peripheral configuration
- **Clock Manager**: System clock configuration and management
- **Pin Multiplexing**: GPIO and peripheral pin assignment
- **SDK Drivers**: Hardware abstraction for clocks, pins, interrupts

## Build Commands

### Primary Build
```bash
cd hello_world_s32k144/Debug_FLASH
make all
```

### Clean Build
```bash
cd hello_world_s32k144/Debug_FLASH
make clean
```

### Size Analysis
```bash
cd hello_world_s32k144/Debug_FLASH
arm-none-eabi-size --format=berkeley hello_world_s32k144.elf
```

## Hardware Configuration

**Default Target**: EVB (Evaluation Board)
- LEDs: PORTD pins 15, 16
- CAN Control: PORTB pin 13 (STB), PORTA pin 6 (EN)

**Alternative Target**: Custom board (uncomment `#define EVB`)
- LEDs: PORTC pins 0, 1

## Development Notes

- The project uses Processor Expert for code generation - avoid modifying generated code directly
- Peripheral configuration should be done through the PE components
- The main application loop demonstrates GPIO toggling for CAN transceiver control
- Build artifacts are generated in `Debug_FLASH/` directory
- Linker script located at: `C:\NXP\S32DS_ARM_v2.2\S32DS\software\S32SDK_S32K1xx_RTM_3.0.0\platform\devices\S32K144\linker\gcc\S32K144_64_flash.ld`

## Debugging

Debug configurations available in `Debug_Configurations/`:
- `hello_world_s32k144_debug_flash_jlink.launch` - Flash debugging with J-Link
- `hello_world_s32k144_debug_ram_jlink.launch` - RAM debugging with J-Link  
- `hello_world_s32k144_debug_ram_pemicro.launch` - RAM debugging with PEMicro

## GitHub Integration Notes

- Repository: https://github.com/KYUNGHUN-HWANG/test3.git
- Use appropriate authentication when pushing
- Configure HTTP buffer for large pushes: `git config http.postBuffer 524288000`
- For push errors, create smaller commits with incremental changes