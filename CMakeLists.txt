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


# --- Executable: COFFLoader64.exe ---
add_executable(COFFLoader64
    beacon_compatibility.c
    COFFLoader.c
)

target_compile_definitions(COFFLoader64 PRIVATE
    COFF_STANDALONE
    RELEASE
)

# --- Object file: test64.out ---
# This builds test.c to an object file, not a full exe.
add_library(test64 OBJECT test.c)
# Rename the object to test64.out instead of default name.
set_target_properties(test64 PROPERTIES
    OUTPUT_NAME "test64"
    SUFFIX ".out"
)

