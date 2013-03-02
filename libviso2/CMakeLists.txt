cmake_minimum_required(VERSION 2.8.3)
project(libviso2)

catkin_package(
    LIBRARIES
        viso2
)

# use sse3 instruction set
SET(CMAKE_CXX_FLAGS "-msse3")

include_directories(include)

add_library(viso2
  src/filter.cpp
  src/matcher.cpp
  src/matrix.cpp
  src/reconstruction.cpp
  src/triangle.cpp
  src/viso.cpp
  src/viso_mono.cpp
  src/viso_stereo.cpp)

install(DIRECTORY include/
    DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
    )

