cmake_minimum_required(VERSION 3.10)

# set the project name and version
project(cortex_m4_template VERSION 1.0)

# add the bin directory to the build system
set(BIN_DIRECTORY   ${CMAKE_BINARY_DIR}/bin)
file(MAKE_DIRECTORY ${BIN_DIRECTORY})

# Create Executable (add_executable output) in bin directory
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${BIN_DIRECTORY})

# Set the source files
set(SOURCES main_blinky.c)

#########################.....Compiler Configuration for CMake........###########
set(CMAKE_SYSTEM_NAME Generic)
set(CMAKE_SYSTEM_PROCESSOR arm)
set(CMAKE_CROSSCOMPILING 1)

# set(GCC_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cross_compiler/gcc-arm-none-eabi-5_3-2016q1/bin)
set(GCC_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cross_compiler/gcc-arm-none-eabi-7-2017-q4-major/bin)

set(CMAKE_C_COMPILER ${GCC_PATH}/arm-none-eabi-gcc CACHE PATH "" FORCE)
#################################################################################

########################....Compilation and linking Configuration....############

# Board specific info
set(DEVICE MSP432P401R)
set(LDSCRIPT ${CMAKE_CURRENT_SOURCE_DIR}/msp432p401r.lds)
set(DEVICE_FLAGS    "-D__${DEVICE}__ -DDeviceFamily_MSP432P401x -Dgcc")

# FLAGS Common to all Cortex-M Boards
set(ARM_FLAGS       "-mcpu=cortex-m4 -march=armv7e-m -mthumb -mfloat-abi=hard -mfpu=fpv4-sp-d16")
set(COMPILER_FLAGS  "-Wall -ffunction-sections -fdata-sections -MD -std=c99")
set(DEBUG_FLAGS     "-g -gstrict-dwarf")
set(LINKER_FLAGS    "-T${LDSCRIPT} -l'c' -l'gcc' -l'nosys'")

set(CMAKE_C_FLAGS "${ARM_FLAGS} ${DEVICE_FLAGS} ${COMPILER_FLAGS}")
set(CMAKE_EXE_LINKER_FLAGS "${LINKER_FLAGS}")

set(CMAKE_C_FLAGS_RELEASE "-Os")
set(CMAKE_C_FLAGS_DEBUG "-Og ${DEBUG_FLAGS}")
#################################################################################



# add the libraries
add_subdirectory(bsp)

# add the executable
set(EXECUTABLE ${PROJECT_NAME}.out)
add_executable(${EXECUTABLE}  ${SOURCES} $<TARGET_OBJECTS:bsp>)
target_link_libraries(${EXECUTABLE} bsp)

# Generate and display code sizes
add_custom_command(TARGET ${EXECUTABLE} POST_BUILD
    COMMAND size ${BIN_DIRECTORY}/${EXECUTABLE}
    COMMENT "Generating build size...")