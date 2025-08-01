# Setup Cmake Version
cmake_minimum_required(VERSION 3.25)

# Setup compiler settings
set(CMAKE_CXX_STANDARD              17)
set(CMAKE_C_STANDARD                11)
set(CMAKE_CXX_STANDARD_REQUIRED     ON)
set(CMAKE_CXX_EXTENSIONS            ON)

# Set project version
set(PROJ_VER_MAJOR                  1)
set(PROJ_VER_MINOR                  0)
set(PROJ_VER_PATCH                  0)

# Get the workspace directory name dynamically
get_filename_component(PROJ_NAME ${CMAKE_SOURCE_DIR} NAME)

# Core project settings
project(
    ${PROJ_NAME}
    VERSION ${PROJ_VER_MAJOR}.${PROJ_VER_MINOR}.${PROJ_VER_PATCH}
    LANGUAGES C ASM CXX
    DESCRIPTION "${PROJ_NAME} - A CMake based project"
)

# Enable compile command to ease indexing with e.g. clangd
set(CMAKE_EXPORT_COMPILE_COMMANDS TRUE)

# Set the project path and executable name
set(PROJ_PATH                   ${CMAKE_SOURCE_DIR}) 
set(EXECUTABLE                  ${CMAKE_PROJECT_NAME})

# Use file(GLOB ...) to include all .c files in the src directory
file(GLOB SRC_FILES            "${PROJ_PATH}/src/*.c")

message("Project name: "        ${CMAKE_PROJECT_NAME})
message("Project version: "     ${CMAKE_PROJECT_VERSION})
message("Build type: "          ${CMAKE_BUILD_TYPE})

# List of source files to compile
set(SOURCES_SRCS                ${SRC_FILES})

# Include directories
set(INCLUDE_PATH                ${PROJ_PATH}/include)

# Executable files
add_executable(${EXECUTABLE} ${SOURCES_SRCS})

# Include paths
target_include_directories(${EXECUTABLE} PUBLIC ${INCLUDE_PATH})

# Compiler options
target_compile_options(${EXECUTABLE} 
    PUBLIC 
        -fdiagnostics-color=always       # Enable colorized diagnostics
        -Wall                            # Enable all warnings
        -Wextra                          # Enable extra warnings
        -std=c17                         # Specify C Language Standard
)
