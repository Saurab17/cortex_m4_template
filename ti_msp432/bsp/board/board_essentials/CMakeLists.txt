cmake_minimum_required(VERSION 3.10)

# set the project name and version
project(board_essentials)

file(GLOB_RECURSE LIB_SOURCES *.c)

add_library(${PROJECT_NAME} ${LIB_SOURCES})

target_include_directories(${PROJECT_NAME} PUBLIC 
                        ${CMAKE_CURRENT_SOURCE_DIR}/..
                        ${CMAKE_CURRENT_SOURCE_DIR}/include
                        ${CMAKE_CURRENT_SOURCE_DIR}/include/CMSIS)