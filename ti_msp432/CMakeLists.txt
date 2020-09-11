cmake_minimum_required(VERSION 3.10)

# set the project name and version
project(cortex_m4_template VERSION 1.0)

# Set the source files
set(SOURCES main.c)

#Cmake Cross compilation for arm microcontrollers
set(CMAKE_SYSTEM_NAME Generic)
set(CMAKE_SYSTEM_PROCESSOR arm)
set(CMAKE_CROSSCOMPILING 1)

set(GCC_PATH
    ${CMAKE_CURRENT_SOURCE_DIR}/cross_compiler/gcc-arm-none-eabi-5_3-2016q1/bin)
set(CMAKE_C_COMPILER ${GCC_PATH}/arm-none-eabi-gcc CACHE PATH "" FORCE)

#Board specific CFlags and Linker Flags
set(DEVICE MSP432P401R)
set(LDSCRIPT ${CMAKE_CURRENT_SOURCE_DIR}/msp432p401r.lds)
# set(CMAKE_C_FLAGS "-mcpu=cortex-m4 -march=armv7e-m -mthumb -mfloat-abi=hard \
# -mfpu=fpv4-sp-d16 -D__${DEVICE}__ -DTARGET_IS_MSP432P4XX \ 
# -ffunction-sections -fdata-sections -Wall -MD -std=c99 \
# -specs=nosys.specs")
set(CMAKE_C_FLAGS "-mcpu=cortex-m4 -march=armv7e-m -mthumb -mfloat-abi=hard -D__${DEVICE}__ -DTARGET_IS_MSP432P4XX -mfpu=fpv4-sp-d16")
# -D__$(DEVICE)__ -DTARGET_IS_MSP432P4XX -Dgcc -g -gstrict-dwarf -Wall -ffunction-sections -fdata-sections -MD -std=c99)
set(CMAKE_C_FLAGS_RELEASE "-Os")
set(CMAKE_C_FLAGS_DEBUG "-Og -g -gdwarf-3 -gstrict-dwarf")

set(CMAKE_EXE_LINKER_FLAGS "-mcpu=cortex-m4 -march=armv7e-m -mfloat-abi=hard -mfpu=fpv4-sp-d16 -mthumb -D__${DEVICE}__ -DTARGET_IS_MSP432P4XX -Dgcc -g -gstrict-dwarf -Wall -T${LDSCRIPT} -l'c' -l'gcc' -l'nosys'")
# set(CMAKE_EXE_LINKER_FLAGS "--entry ResetISR -Wl,-T\"../tm4c123gh6pm.lds\"")
# LDFLAGS = -mcpu=cortex-m4 -march=armv7e-m -mfloat-abi=hard -mfpu=fpv4-sp-d16 -mthumb -D__$(DEVICE)__ -DTARGET_IS_MSP432P4XX -Dgcc -g -gstrict-dwarf -Wall -T$(LDDIR).lds -l'c' -l'gcc' -l'nosys'

# add the executable
add_subdirectory(board_essentials)


add_executable(${PROJECT_NAME}.elf ${SOURCES})
target_link_libraries(${PROJECT_NAME}.elf board_essentials)