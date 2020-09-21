# Arm Cortex-M4 Template
A cross development [CMake](https://cmake.org/) project template for arm cortex-m4 based microcontrollers on `Linux` host.  
The main purpose of this template is to help embedded developers leverage CMake build features. Also,   
with this template, you are free to use your own favorite C/C++ code editor like `VS Code`, `Atom` etc.

## Project Setup
The top-level project directory structure is as follows:  

+ board_essentials
    - This directory contains the [system configuration](https://www.keil.com/pack/doc/CMSIS/Core/html/system_c_pg.html) and [startup](https://www.keil.com/pack/doc/CMSIS/Core/html/startup_c_pg.html) files.  
    It also includes the [CMSIS](https://www.keil.com/pack/doc/CMSIS/Core/html/index.html) header files. 
    - For example, below are the links to support files for popular boards:
        -  [TI MSP432P401R](http://software-dl.ti.com/msp430/msp430_public_sw/mcu/msp430/MSP432GCC/latest/index_FDS.html)
        -  [STLink STM32F4xx Discovery](https://github.com/charleskorn/stm32f4-project-template/tree/master/lib/stm32f4xx)
        -   [Nordic nRF52840](https://www.nordicsemi.com/Software-and-tools/Development-Tools/nRF-MDK/Download#infotabs)

+ bsp
    - This directory to store the board support software from vendor. 
    - Subdirectories:
        -  [driverlib](https://www.ti.com/tool/MSPDRIVERLIB): Software APIs that abstract away the details of the device’s hardware registers.

+ cross_compiler
    - This directory contains the [GNU Arm Embedded Toolchain](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm) to cross-compile your source code  
    and generate binaries for your cortex-m4 microcontroller.

+ CMakeLists.txt
    - Project top level cmake config file.

+ main_*.c
    - The file containing program entry `main()` function. Alternatively, the entire app code along  
    with main_*.c file can be moved in an `app` folder and cmake config files tweaked accordingly.

+ *.ld(s)
    - The linker script for the particular board provided by the vendor.

## Building and Compilation
The final output is generated inside the `bin` subdirectory of build directory. To generate the binary output,  
run following commands while in project directory, for example, in ti_msp432.  
For `debug` build:
```
$ mkdir debug
$ cd debug
$ cmake -DCMAKE_BUILD_TYPE=Debug ..
$ make
```
For `release` build:
```
$ mkdir release
$ cd release
$ cmake -DCMAKE_BUILD_TYPE=Release ..
$ make
```

## Target Flashing
The following tools can be used to flash the binary output into the target microcontroller:  
+ [TI's UniFlash](https://www.ti.com/tool/UNIFLASH)
+ [STM32 ST-LINK utility](https://www.st.com/en/development-tools/stsw-link004.html)
+ [Nordic's nrfjprog](https://www.nordicsemi.com/Software-and-tools/Development-Tools/nRF-Command-Line-Tools#infotabs)


