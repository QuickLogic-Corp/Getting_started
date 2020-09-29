# Purpose

Plan the structure of the getting-started documentation, and streamline the content in the different related repositories from which will be linked or assimilated into the documentation.  
This document can be used to be reviewed and collect feedback on the proposed structure and content modifications.  
The proposed getting-started structure and content starts from the next section.

# Structure

## Intro

This documentation will help get quickly up to speed with the QORC SDK using the QuickFeather development board. It will cover the basics of the development kit, and how to setup the development environment for the Cortex-M4F core as well as for the FPGA in the EOS S3.

## EOS S3 Architecture

Explain the basic architecture of the EOS S3 with a block diagram.  
We can either show only in-use blocks (skip FFE) or show those blocks as available but not yet covered with a different color.  
[point to separate repo, if it already has the information.]


## What You Need

1. Hardware
- QuickFeather Development Board
- USB-UART cable 3.3v

2. M4 Applications
- Build Environment: GCC Arm Embedded Toolchain (point to -> qorc-sdk readme)
- Flash Progammer Tool : TinyFPGAProgammer ( point to -> TinyFPGAProgrammer readme)
- Serial Port Terminal Application: putty/gtkterm/others (point to -> qorc-sdk readme)
- QORC SDK (point to qorc-sdk readme)

3. FPGA Applications
- Build Environment: Quicklogic Symbiflow Toolchain (point to -> quicklogic-fpga-toolchain readme)

4. IDE for M4 Application Development (TODO)
- Eclipse + Eclipse Embedded CDT (GNU MCU Tools has now migrated to the Eclipse Foundation) 

5. Debugging M4 Applications (TODO)
- J-Link Base or Edu ( do we support BlackMagic probe or OpenOCD based tools? )

6. Debugging FPGA Designs (TODO)
- Do we target this, if not, can be removed.


## Development Board

- **Quick Feather Development Board**: [ point to quick-feather-development-board with relevant information added ]  




## How-To

1. Build, Flash and Run M4 Application (FreeRTOS)
- cover modifying M4 Application also
- [point to the qf_helloworldsw readme]

2. Build, Flash and Run M4 (FreeRTOS) + FPGA Application
- cover how to use the dedicated M4 UART for debug prints, instead of the USB
- cover basic example (only FPGA loading by M4) - LED BLINK
- cover simple modification to the FPGA design - LED BLINK
- [point to the qf_hellowordhw readme]
- cover advanced example (FPGA load by M4 + control from M4 via custom HAL) - LED CTRL
- [point to the qf_advancedfpga readme]

3. Additional Example for M4 + FPGA practical application (for workshop etc.)
- Use bin2seven FPGA, M4 code interacting with FPGA through the HAL
- input number to M4 via UART, and send binary to FPGA, 7seg LED should reflect the change
- [point to the qf_xxx readme]

4. Build, Flash and Run M4 Application (Baremetal)
- if required, this can be added, can be marked as advanced usage as the user will have to undestand the clock/power domain architecture in detail to really use this way.
- [point to the qf_baremetal readme]

5. Debug M4 Application (TODO)
- use J-Link to load, set breakpoint and run, inspect variables, ram content
- use other probes (BlackMagic or OpenOCD based) if ready and needed
- [point to qorc-sdk debugging readme]

6. Use Eclipse to Create Project, Build and Debug (TODO)
- if ready, include this documentation
- take one example and show, the same would apply for all.
- [point to the qorc-sdk eclipse readme]

7. Debug FPGA Designs (TODO)
- is this needed here ? if it seems relevant to FPGA users, we can add content here.


## Further Info (can be split across categories)


1. [HW]EOS S3 Register Map
2. [HW]EOS S3 IOMUX and description
3. [HW]EOS S3 TRM
4. [HW] Others, for FPGA HM, clocking etc.
5. QORC SDK Flash Memory Map and the Bootloader process
- explain bootloading process
- [point to the qf_bootloader readme]
6. Flash Programming process
- explain the image format, and flash programmer process
- how the bootloader will parse, verify and write to flash
7. QORC SDK Structure (Libraries, Tasks, HAL, FPGA Designs, BSP)
- basic explanation of the structure and content in each directory
- API guides if needed can be added later.
8. Add more if needed.

## Pinned Repos:
1. qorc-sdk
2. quicklogic-fpga-toolchain 
3. TinyFPGA-Programmer-Application 
4. quick-feather-dev-board 
5. TODO
6. TODO

