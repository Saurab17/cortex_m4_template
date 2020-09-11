add_library(board_essentials
            src/interrupts_msp432p401r_gcc.c
            src/startup_msp432p401r_gcc.c
            src/system_msp432p401r.c)

target_include_directories(board_essentials PUBLIC 
                        ${CMAKE_CURRENT_SOURCE_DIR}/include
                        ${CMAKE_CURRENT_SOURCE_DIR}/include/CMSIS)