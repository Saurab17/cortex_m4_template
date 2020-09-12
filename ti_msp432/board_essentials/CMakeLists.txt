# Need to make Object type library for proper linking.
# Doesn't work when statically linked and files packed to .a library
add_library(board_essentials OBJECT
            src/interrupts_msp432p401r_gcc.c
            src/startup_msp432p401r_gcc.c
            src/system_msp432p401r.c)

target_include_directories(board_essentials PUBLIC 
                        ${CMAKE_CURRENT_SOURCE_DIR}/include
                        ${CMAKE_CURRENT_SOURCE_DIR}/include/CMSIS)