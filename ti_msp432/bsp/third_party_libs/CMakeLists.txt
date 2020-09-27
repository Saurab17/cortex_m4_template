# Need to make Object type library for proper linking.
# Doesn't work when statically linked and files packed to .a library
cmake_minimum_required(VERSION 3.10)

# set the project name and version
project(third_party_libs)

#add the subdirectories
# add_subdirectory(fatfs)
add_subdirectory(spiffs)