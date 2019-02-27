cmake_minimum_required(VERSION 3.1.2)
project(conan-libpqxx)

include("${CMAKE_BINARY_DIR}/conanbuildinfo.cmake")
conan_basic_setup()

if (BUILD_SHARED_LIBS AND WIN32)
    list(APPEND CXX_SOURCES "${CMAKE_SOURCE_DIR}/source_subfolder/win32/libpqxx.cxx")
endif()

if (BUILD_SHARED_LIBS)
    target_compile_definitions(${PROJECT_NAME} PUBLIC -DPQXX_SHARED)
endif()

if (WIN32)
    target_compile_definitions(${PROJECT_NAME} PUBLIC WIN32 _MBCS _WINDOWS PQXX_INTERNAL NOMINMAX)
endif()

if (WIN32)
    target_link_libraries(${PROJECT_NAME} PRIVATE ws2_32)
endif()

set_property(TARGET ${PROJECT_NAME} PROPERTY CXX_STANDARD 14)

add_subdirectory(source_subfolder)
