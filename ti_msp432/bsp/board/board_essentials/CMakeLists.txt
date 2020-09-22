# Need to make Object type library for proper linking.
# Doesn't work when statically linked and files packed to .a library
cmake_minimum_required(VERSION 3.10)

# set the project name and version
project(board_essentials)

file(GLOB LIB_SOURCES src/*.c)

add_library(${PROJECT_NAME} OBJECT ${LIB_SOURCES})

target_include_directories(${PROJECT_NAME} PUBLIC 
                        ${CMAKE_CURRENT_SOURCE_DIR}/include
                        ${CMAKE_CURRENT_SOURCE_DIR}/include/CMSIS)