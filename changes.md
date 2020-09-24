# Purpose

List down any changes or issues noticed in the readme content across the various repositories.

### 1. General


### 2. quick-feather-dev-board
- [ ] 1. pinouts of the HDK should be covered in the readme, basic diagram with the pinouts
- [ ] 2. major pins, used in the example applications (UART) should be on the readme
- [x] 3. detailed information can be left to the User Guide PDF as is


### 3. quicklogic-fpga-toolchain
- [ ] 1. Recommend Docker to install the toolchain ( for both installer or the compile from sources methods) - The basic Dockerfile(s) are already in the repo
- [ ] 2. Add Docker entrypoint script to enable ability to launch container to build specific FPGA design, produce output and exit and remove container, in combination with parameters, bind mounts.
- [ ] 3. Add Docker example invocations of the container to build FPGA design (ENV, bind volumes, arguments etc. )
    We can effectively decouple the Symbiflow tooling from the local system, so that there won't be any possible conflicts, conda issues, as well as possible conflicts with other versions of Symbiflow that may be installed for ice40/ecp5 etc.  
    We can also have multiple versions of Quicklogic tooling at the same time (for testing or comparison etc.) as well.  
    I have used this flow, with aosp Docker images, so as to have separate environments for Android 6/7/8+ as well as different chipsets.  
    We can invoke a single command which will spin up the container, build the kernel/Android images, and exit, and the host system can wait for container to exit, and then proceed to flash new images.  
    

**references**:  
- https://www.attosol.com/using-docker-for-distributing-command-line-tools/
- https://spin.atomicobject.com/2015/11/30/command-line-tools-docker/  
(will try this out similar to aosp setup I use for this purpose and update)
- https://medium.com/@AndreSand/building-android-with-docker-8dbf717f54d4  
- https://hub.docker.com/r/mingc/android-build-box/  


### 4. qorc-sdk  
- [ ] 1. GCC Arm Embedded Toolchain: remove the ppa, as it is deprecated.  
    In the ppa: https://launchpad.net/gcc-arm-embedded  
    The announcement states that it is deprecated, and we should use the ARM developer website. It is valid upto Ubuntu 14.04, but the toolchain version is pretty outdated, also does not cover other distros (many use Arch/Manjaro too).  
    Basic steps would be:  
    1. Download tarball from: https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm/downloads  
    Current stable version is `9-2020-q2-update`
    2. Extract the tarball to, say, /usr/share/  
    ` sudo tar xvjf gcc-arm-none-eabi-9-2020-q2-update-x86_64-linux.tar.bz2 -C /usr/share/`
    3. Add the /usr/share/gcc-arm-none-eabi-your-version/bin/ to PATH (only for current session)  
    `export PATH=/usr/share/gcc-arm-none-eabi-9-2020-q2-update/bin/:$PATH`
    4. If the user wants it be permanent, it can be added to the .bashrc or .profile
    5. There may be unmet dependencies depending on system configuration, such as the `libncurses` missing, which is more to do with the ARM toolchain than specific to us.  
    We can list "known issues" separately to deal with problems as and when reported.
    6. Windows can also be supported for M4 applications, do we need to add info here?

- [ ] 2. Serial Port Terminal Application
  -  in most modern Linux systems, the USB Serial listing will be `ttyACMxx` due to the USB-CDC class
  -  `ttySxx` when native serial port of PC, `ttyUSBxx` when usb-uart converter, `ttyACMxx` when USB CDC
  - example images seem to show only `ttySxx`, not sure why.
  
- [ ] 3. qf_apps
  - each qf_app should contain its own readme, which has the description of the application.
  - we can move the Build, Flash, Run steps for each app here instead of having everything in the main qorc-sdk readme and there is a link from the main readme to the qf_app readmes
  - for example, the fpga/advanced fpga apps, an extra UART connection is needed, if the information is contained in each app readme, it would be more structured
 
- [ ] 4. Cloning the qorc-sdk repo
  - the repo should be cloned with --recursive, as the it affects the path used by "qf-initial-binaries" rather than the repo name "qf-initial-bins", s3_gateware etc.
  update the steps to mention this

- [ ] 5. QORC SDK Structure
  - the qorc-sdk readme should have a brief description of the contents of the various directories, so that users have clarity.
  - for example, s3_gateware, gateware, and freertos_gateware, serve different purposes, but can be explained
  - reason for separate qf_testapps and qf_apps as well.

-  [ ] 6. Create New Application
   - Have  not tried this out yet, will try out and see if we can add a "tutorial" example for this

- [ ] 7. Adding "make flash" target
  - we can add a "make flash" target to automatically pick and invoke the qfprog with appropriate args
  - It might be useful when there are more file types to be flashed (appfee/appfpga etc.)


### 5. TinyFPGAPrgammer

- [ ] 1. Repeat of info between qorc-sdk and TinyFPGAProgrammer readme with differing steps
  - can move all the steps to TinyFPGAProgrammer readme and organize with a bit more clarity
    1. clone repo recursively
       `git clone --recursive https://github.com/QuickLogic-Corp/TinyFPGA-Programmer-Application.git`
    2. dependency on the tinyfpgab python module, so install it
       `pip3 install tinyfpgab`
    3. running without any params(as in readme) produces error, and reports GUI mode disabled, can fix it.  
       we should recommend running with --help to verify install ok:
       `python3 tinyfpga-programmer-gui.py --help`
    4. create alias and if needed to be permanent, add to .bashrc or .profile
       `alias qfprog="python3 path-to-git-clone-dir/TinyFPGA-Programmer-Application/tinyfpga-programmer-gui.py"`

- [ ] 2. Flash Programmer starts working, even though QF is not in programming mode
  - If we run the flash programmer when QF is in normal mode, it starts and gets stuck at readback:
    ```
    qfprog --port /dev/ttyACM0 --m4app output/bin/qf_helloworldsw.bin
            CLI mode
            ports =  ['/dev/ttyACM0 (QuickFeather)'] 1
            Using port  /dev/ttyACM0 (QuickFeather)
            Programming m4 application with  output/bin/qf_helloworldsw.bin
            Erasing designated flash pages
            Erase  64.0 KiB ( 0xd8 ) at  0x80000
            Erase  32.0 KiB ( 0x52 ) at  0x90000
            Erase  4.0 KiB ( 0x20 ) at  0x98000
            Erase  4.0 KiB ( 0x20 ) at  0x99000
            Erase  4.0 KiB ( 0x20 ) at  0x9a000
            Erase  4.0 KiB ( 0x20 ) at  0x9b000
            Erase  4.0 KiB ( 0x20 ) at  0x9c000
            Writing  binary
            Write  114976  bytes
            [XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX]
            Verifying  binary
            FastREAD 0x0B ( 114976 )
            [^CTraceback (most recent call last):             ]
    ```
   This looks like it can be fixed, or noted that it doesn't cause any problems.

- [ ] 3. Leaving QF in programming mode for a longer time
  - After entering programming mode, I got into some other stuff, so it was in programming mode for ~20 mins.
  - Then when I tried to flash, it didn't go through. Not sure if this is a problem, but can be looked at.



