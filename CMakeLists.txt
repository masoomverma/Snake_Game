cmake_minimum_required(VERSION 3.21)
project(Snake_Game LANGUAGES CXX)

# -----------------------------
# C++ Version
# -----------------------------
set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# -----------------------------
# Include directories
# -----------------------------
include_directories(
        include
        libs/include
)

# -----------------------------
# Collect source files
# -----------------------------
file(GLOB_RECURSE SOURCES
        src/*.cpp
)

# -----------------------------
# Build executable
# -----------------------------
add_executable(Snake_Game ${SOURCES})

# -----------------------------
# Find SFML (graphics, window, system, audio)
# -----------------------------
find_package(SFML 2.5 COMPONENTS graphics window system audio REQUIRED)

target_link_libraries(Snake_Game
        sfml-graphics
        sfml-window
        sfml-system
        sfml-audio
)

# -----------------------------
# Copy assets folder to build directory
# -----------------------------
add_custom_command(TARGET Snake_Game POST_BUILD
        COMMAND ${CMAKE_COMMAND} -E copy_directory
        ${CMAKE_SOURCE_DIR}/assets
        $<TARGET_FILE_DIR:Snake_Game>/assets
)
