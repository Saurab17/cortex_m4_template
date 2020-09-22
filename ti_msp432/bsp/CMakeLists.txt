# Need to make Object type library for proper linking.
# Doesn't work when statically linked and files packed to .a library
cmake_minimum_required(VERSION 3.10)

# set the project name and version
project(bsp)

#add the subdirectories
add_subdirectory(board)
add_subdirectory(drivers)
add_subdirectory(display)
add_subdirectory(grlib)

add_library(${PROJECT_NAME})
target_link_libraries(${PROJECT_NAME} grlib board drivers display)