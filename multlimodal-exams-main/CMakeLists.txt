cmake_minimum_required(VERSION 3.14)
project(MultilingualPipeline)

set(CMAKE_CXX_STANDARD 17)

# Include VCPKG
set(CMAKE_TOOLCHAIN_FILE "${CMAKE_CURRENT_SOURCE_DIR}/vcpkg/scripts/buildsystems/vcpkg.cmake" CACHE STRING "VCPKG toolchain file")

# Add include directories
include_directories(
    ${CMAKE_SOURCE_DIR}/vcpkg/installed/arm64-osx/include
    /opt/homebrew/opt/opencv/include/opencv4
    /opt/homebrew/opt/poppler/include
    /opt/homebrew/opt/openssl@3/include
)

# Add library directories
link_directories(
    /opt/homebrew/opt/poppler/lib
    /opt/homebrew/opt/openssl@3/lib
    /opt/homebrew/opt/opencv/lib
)

# Add source files
add_executable(pipeline pipeline.cpp)

# Link necessary libraries
target_link_libraries(pipeline PRIVATE
    pthread
    poppler-cpp
    opencv_core
    opencv_imgcodecs
    ssl
    crypto
)
