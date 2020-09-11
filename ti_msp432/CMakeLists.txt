cmake_minimum_required(VERSION 3.10)

# set the project name and version
project(cortex_template VERSION 1.0)

# add the executable
add_subdirectory(board_essentials)
add_executable(main main.cpp)