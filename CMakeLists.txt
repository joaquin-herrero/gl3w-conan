cmake_minimum_required(VERSION 3.13)

project(gl3w)

include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
conan_basic_setup(KEEP_RPATHS)

################
# Set RPATHs
################
if(APPLE)
  set(CMAKE_INSTALL_RPATH "@executable_path/../lib")
else()
  set(CMAKE_INSTALL_RPATH "$ORIGIN/../lib")
endif()

set(CMAKE_BUILD_WITH_INSTALL_RPATH ON)


# add and depend on OpenGL
find_package(OpenGL REQUIRED)

# builds a static library from gl3w which can be linked against
add_library(gl3w)
target_sources(gl3w PRIVATE gl3w/src/gl3w.c)
target_include_directories(gl3w PUBLIC gl3w/include)
target_link_libraries(gl3w PUBLIC OpenGL::GL OpenGL::GLU)