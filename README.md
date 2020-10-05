## Intro

This documentation will help get quickly up to speed with the QORC SDK using the QuickFeather development board. It will cover the basics of the development kit, and how to setup the development environment for the Cortex-M4F core as well as for the FPGA in the EOS S3.

## What You Need

1. Hardware
- QuickFeather Development Board
- USB-UART cable 3.3v

2. M4 Applications
- Build Environment: GCC Arm Embedded Toolchain
  Refer to https://github.com/QuickLogic-Corp/qorc-sdk#toolchain for instructions
- Flash Progammer Tool : TinyFPGAProgammer
  Refer to https://github.com/QuickLogic-Corp/TinyFPGA-Programmer-Application#tinyfpga-programmer-application for instructions
- Serial Port Terminal Application:
  Install an application of your choice, such as PuTTY, GTKTerm etc.
- QORC SDK (point to qorc-sdk readme)
  Clone the qorc-sdk repo: https://github.com/QuickLogic-Corp/qorc-sdk 

3. FPGA Applications
- Build Environment: Quicklogic Symbiflow Toolchain
  Refer to https://github.com/QuickLogic-Corp/quicklogic-fpga-toolchain for instructions


## Development Board

- **Quick Feather Development Board**
  Refer to https://github.com/QuickLogic-Corp/quick-feather-dev-board for details on the board.


## How-To

1. Build, Flash and Run M4 Application (FreeRTOS)
- Basic example "Hello World", refer to https://github.com/QuickLogic-Corp/qorc-sdk#lesson-1a-m4-only--qf_helloworldsw

- Modify basic example, refer to https://github.com/QuickLogic-Corp/qorc-sdk#lesson-1b-m4-only--modify-qf_helloworldsw

2. Build, Flash and Run M4 (FreeRTOS) + FPGA Application
- Note that we have to use the dedicated M4 UART for debug prints, instead of the FPGA based USB IP, because the Application will be loading a different FPGA design
  Refer to **[TODO URL]** for details on how to connect a USB UART board such as PL2303, FT232 etc. based boards

- Basic Example of using FPGA for LED Blink to start with, refer to https://github.com/QuickLogic-Corp/qorc-sdk#lesson-2a-fpga-only--qf_helloworldhw

- Modify the FPGA design of the basic FPGA LED Blink example, refer to https://github.com/QuickLogic-Corp/qorc-sdk#lesson-2b-fpga-only--modify-qf_helloworldhw

- Advanced example with FPGA load by M4 + control from M4 via custom HAL "LED CONTROLLER", refer to https://github.com/QuickLogic-Corp/qorc-sdk#lesson-3-advanced-fpga-m4--fpga-qf_advancedfpga

