# Need to make Object type library for proper linking.
# Doesn't work when statically linked and files packed to .a library
cmake_minimum_required(VERSION 3.10)

# set the project name and version
project(display)

# add the sources 
file(GLOB_RECURSE LIB_SOURCES *.c)

#add the subdirectories
add_library(${PROJECT_NAME} OBJECT ${LIB_SOURCES})
target_link_libraries(${PROJECT_NAME} drivers grlib)
target_include_directories(${PROJECT_NAME} PUBLIC 
                            ${CMAKE_CURRENT_SOURCE_DIR}
                            ${CMAKE_CURRENT_SOURCE_DIR}/*)