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
add_subdirectory(third_party_libs)

add_library(${PROJECT_NAME} INTERFACE)

target_link_libraries(${PROJECT_NAME} INTERFACE board drivers grlib display third_party_libs)

target_include_directories(${PROJECT_NAME} INTERFACE ${CMAKE_CURRENT_SOURCE_DIR})