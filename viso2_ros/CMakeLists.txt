cmake_minimum_required(VERSION 2.8.3)
project(viso2_ros)

find_package(catkin REQUIRED
    COMPONENTS
    roscpp
    tf
    message_generation
    libviso2
    image_transport
    image_geometry
    cv_bridge
    )

find_package(Boost REQUIRED
    COMPONENTS
    signals
    )
find_package(OpenCV REQUIRED)
find_package(PCL REQUIRED)

add_message_files(
    FILES
    VisoInfo.msg
    )

generate_messages(
    DEPENDENCIES
        std_msgs
)

catkin_package(
    CATKIN_DEPENDS
    message_generation
)

include_directories(
    ${catkin_INCLUDE_DIRS}
    ${OpenCV_INCLUDE_DIRS}
    ${Boost_INCLUDE_DIRS}
    ${PCL_INCLUDE_DIRS}
    )

add_executable(stereo_odometer
  src/stereo_odometer.cpp)
target_link_libraries(stereo_odometer
    ${catkin_LIBRARIES}
    ${OpenCV_LIBRARIES}
    ${Boost_LIBRARIES}
    ${PCL_LIBRARIES}
    )
add_dependencies(stereo_odometer viso2_ros_gencpp)

add_executable(mono_odometer
  src/mono_odometer.cpp)
target_link_libraries(mono_odometer
    ${catkin_LIBRARIES}
    ${OpenCV_LIBRARIES}
    )

install(
    TARGETS
      stereo_odometer
      mono_odometer
    ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
    LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
    RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)


