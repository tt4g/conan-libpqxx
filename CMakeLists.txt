cmake_minimum_required(VERSION 3.1.2)
project(conan-libpqxx)

include("${CMAKE_BINARY_DIR}/conanbuildinfo.cmake")
conan_basic_setup()

set(CMAKE_CXX_STANDARD 14)

add_subdirectory(source_subfolder)

if (WIN32)
    add_definitions(-DWIN32 -D_MBCS -D_WINDOWS -DPQXX_INTERNAL -DNOMINMAX)
endif()
