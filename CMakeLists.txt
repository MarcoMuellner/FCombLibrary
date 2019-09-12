project(FreqCombinator)

#minimum cmake version shouldn't be too old
cmake_minimum_required(VERSION 3.10)
# Specify the location of the header files

include_directories(cpp_files/include)
include_directories(cpp_files/python_wrapper/include)

#source files
file(GLOB sourceFiles cpp_files/src/*.cpp)

#compiler messages
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O3 -Wall")

# Then those specific for the compiler, for using C++11 support.

if ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "Clang")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -stdlib=libc++ -std=c++11 -Wno-deprecated-register -fPIC")
elseif ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++0x -fPIC")
endif()


add_subdirectory(cpp_files/pybind11)

SET(CMAKE_FIND_LIBRARY_SUFFIXES ".a")
SET(BUILD_SHARED_LIBRARIES OFF)
SET(CMAKE_EXE_LINKER_FLAGS "-static")


pybind11_add_module(FCombLibrary cpp_files/python_wrapper/FreqCombiner.cpp)