cmake_minimum_required(VERSION 3.10)

# set the project name and version
project(bsp)

#add the subdirectories
add_subdirectory(board)
add_subdirectory(drivers)
add_subdirectory(display)
add_subdirectory(grlib)
add_subdirectory(third_party_libs)
