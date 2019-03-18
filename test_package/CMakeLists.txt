project(PackageTest)
cmake_minimum_required(VERSION 2.8.12)

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

add_executable(example example.cpp)
target_link_libraries(example ${CONAN_LIBS} ${CMAKE_DL_LIBS})
