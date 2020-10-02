cmake_minimum_required(VERSION 3.10)

# set the project name and version
project(freertos)

# add the sources 
file(GLOB_RECURSE LIB_SOURCES *.c)

# foreach(FILE ${LIB_SOURCES})
#     message("${FILE} \n")
# endforeach()


add_library(${PROJECT_NAME} ${LIB_SOURCES})

target_link_libraries(${PROJECT_NAME} drivers driverlib board_essentials)

target_include_directories(${PROJECT_NAME} PUBLIC 
    ${CMAKE_CURRENT_SOURCE_DIR}/FreeRTOS10.3.1/Source/include
    ${CMAKE_CURRENT_SOURCE_DIR}/FreeRTOS10.3.1/Source/portable/GCC/ARM_CM4F)