cmake_minimum_required(VERSION 2.8)

set(CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/src/core/cmake ${CMAKE_CURRENT_SOURCE_DIR}/src/core/cmake/solar ${CMAKE_MODULE_PATH})
include(ForceOutBuild)
include(ForceLatinPaths)

project(AXRExamples)

# Options
option(AXR_ALL_WARNINGS "Display as many warnings as possible" OFF)
option(AXR_BUILD_CORE "Builds the core library" ON)
set(AXR_BUILD_EXTENSIONS "QT;COCOA" CACHE STRING "Builds extension libraries for toolkit integration")

#include_directories(SYSTEM ${SDL_INCLUDE_DIR})

add_subdirectory(src/core)
add_subdirectory(src)
