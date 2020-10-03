cmake_minimum_required(VERSION 3.10)

# set the project name and version
project(app)

# Set the source files
file(GLOB SOURCES *.c)

set(EXECUTABLE ${PROJECT_NAME}.out)
add_executable(${EXECUTABLE} ${SOURCES})

target_link_libraries(${EXECUTABLE} freertos drivers driverlib display)

target_include_directories(${EXECUTABLE} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

# Generate and display code sizes
add_custom_command(TARGET ${EXECUTABLE} POST_BUILD
    COMMAND size ${BIN_DIRECTORY}/${EXECUTABLE}
    COMMENT "Generating build size...")