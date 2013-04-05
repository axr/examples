cmake_minimum_required(VERSION 2.8)

set(AXR_CORE_SOURCE_DIR_REL "../core" CACHE STRING "Path to the AXR core sources (relative)")
set(AXR_CORE_SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/${AXR_CORE_SOURCE_DIR_REL})
if(NOT EXISTS "${AXR_CORE_SOURCE_DIR}" OR NOT IS_DIRECTORY "${AXR_CORE_SOURCE_DIR}")
    message(FATAL_ERROR "Could not find core module at expected path: ${AXR_CORE_SOURCE_DIR}")
endif()

set(AXR_COMMON_SOURCE_DIR_REL "../common" CACHE STRING "Path to the AXR common sources (relative)")
set(AXR_COMMON_SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/${AXR_COMMON_SOURCE_DIR_REL})
if(NOT EXISTS "${AXR_COMMON_SOURCE_DIR}" OR NOT IS_DIRECTORY "${AXR_COMMON_SOURCE_DIR}")
    message(FATAL_ERROR "Could not find common module at expected path: ${AXR_COMMON_SOURCE_DIR}")
endif()

set(CMAKE_MODULE_PATH ${AXR_CORE_SOURCE_DIR}/cmake ${AXR_CORE_SOURCE_DIR}/cmake/solar ${CMAKE_MODULE_PATH})
include(ForceOutBuild)
include(ForceLatinPaths)

project(AXRExamples)

# Options
option(AXR_ALL_WARNINGS "Display as many warnings as possible" OFF)
option(AXR_BUILD_CORE "Builds the core library" ON)
set(AXR_BUILD_EXTENSIONS "QT;COCOA" CACHE STRING "Builds extension libraries for toolkit integration")

#include_directories(SYSTEM ${SDL_INCLUDE_DIR})

add_subdirectory("${AXR_CORE_SOURCE_DIR_REL}" "${CMAKE_BINARY_DIR}/_core")
add_subdirectory(src)
