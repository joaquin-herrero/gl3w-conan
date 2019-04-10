cmake_minimum_required(VERSION 3.12)

# Required for OSX rpaths
# https://cmake.org/cmake/help/v3.13/policy/CMP0068.html
if( COMMAND cmake_policy )
  cmake_policy( SET CMP0068 OLD )
endif( COMMAND cmake_policy )

project(gl3w)

include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
conan_basic_setup()

# add and depend on OpenGL
find_package(OpenGL REQUIRED)

# builds a static library from gl3w which can be linked against
add_library(gl3w)
target_sources(gl3w PRIVATE gl3w/src/gl3w.c)
target_include_directories(gl3w PUBLIC gl3w/include)
target_link_libraries(gl3w PUBLIC OpenGL::GL OpenGL::GLU)