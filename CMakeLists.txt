cmake_minimum_required(VERSION 3.24)
project(CoffLoader VERSION 1.0.0 LANGUAGES C)

set(DEFAULT_BUILD_TYPE "Release")

if(WIN32)
        set(CMAKE_C_FLAGS_RELEASE "/MT")
        set(CMAKE_CXX_FLAGS_RELEASE "/MT")
endif()

set(SOURCE_FILES
beacon_compatibility.c
COFFLoader.c
)

add_library(${PROJECT_NAME} STATIC ${SOURCE_FILES})
set_property(TARGET ${PROJECT_NAME} PROPERTY MSVC_RUNTIME_LIBRARY "MultiThreaded")
target_include_directories(${PROJECT_NAME} PUBLIC ./)