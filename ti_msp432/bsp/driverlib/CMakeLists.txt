# Need to make Object type library for proper linking.
# Doesn't work when statically linked and files packed to .a library
cmake_minimum_required(VERSION 3.10)

# set the project name and version
project(driverlib)

file(GLOB LIB_SOURCES src/*.c)

add_library(${PROJECT_NAME} OBJECT ${LIB_SOURCES})

target_include_directories(${PROJECT_NAME} PUBLIC 
                        ${CMAKE_CURRENT_SOURCE_DIR}/include)

target_link_libraries(${PROJECT_NAME} board_essentials)