cmake_minimum_required(VERSION 3.10)

# set the project name and version
project(nortos)

# add the sources 
file(GLOB_RECURSE LIB_SOURCES *.c)

add_library(${PROJECT_NAME} ${LIB_SOURCES})

target_link_libraries(${PROJECT_NAME} drivers driverlib board_essentials)

target_include_directories(${PROJECT_NAME} PUBLIC 
                           ${CMAKE_CURRENT_SOURCE_DIR}
                           ${CMAKE_CURRENT_SOURCE_DIR}/..)