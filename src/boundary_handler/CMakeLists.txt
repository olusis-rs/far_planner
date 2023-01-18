cmake_minimum_required(VERSION 3.8)

project("boundary_handler")

set(CMAKE_CXX_STANDARD 17)

set(CMAKE_BUILD_TYPE Release)
set(BUILD_STATIC_LIBS ON)
set(BUILD_SHARED_LIBS OFF)
set(CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Werror")
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -Werror")

set(visibility_graph_msg_DIR "/home/olusis/Documents/Development/ugv_driver/third_party/far_planner/src/visibility_graph_msg/build/visibility_graph_msg")

find_package(PCL REQUIRED)
find_package(OpenCV REQUIRED)

# ROS dependencies
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(std_msgs REQUIRED)
find_package(sensor_msgs REQUIRED)
find_package(visibility_graph_msg REQUIRED)
find_package(pcl_ros REQUIRED)

#find_package(catkin REQUIRED COMPONENTS
#  roscpp
#  std_msgs
#  sensor_msgs
#  visibility_graph_msg
#  pcl_ros
#)

#catkin_package(
#  CATKIN_DEPENDS
#  roscpp
#  std_msgs
#  sensor_msgs
#  pcl_ros
#)

###########
## Build ##
###########

## Specify additional locations of header files
## Your package locations should be listed before other locations
include_directories(
  ${PCL_INCLUDE_DIRS}
  ${OpenCV_INCLUDE_DIRS}
  "${PROJECT_SOURCE_DIR}/include"
  /usr/local/include # Location when using 'make system_install'
  /usr/include       # More usual location (e.g. when installing using a package)
)

## Specify additional locations for library files
link_directories(
	/home/olusis/Documents/Development/ugv_driver/third_party/far_planner/src/visibility_graph_msg/build/visibility_graph_msg
	/usr/local/lib # Location when using 'make system_install'
	/usr/lib       # More usual location (e.g. when installing using a package)
)

## Depedent cpp files
set(SOURCES ${SOURCES}
)

## Declare executables
add_executable(${PROJECT_NAME} src/graph_extractor.cpp ${SOURCES})
add_dependencies(${PROJECT_NAME} ${${PROJECT_NAME}_EXPORTED_TARGETS})


## Specify libraries to link a library or executable target against
target_link_libraries(${PROJECT_NAME} ${PCL_LIBRARIES} ${OpenCV_LIBS})

ament_package()

install(TARGETS ${PROJECT_NAME} DESTINATION lib/${PROJECT_NAME})
#	ARCHIVE DESTINATION lib/${PROJECT_NAME}
#	LIBRARY DESTINATION lib/${PROJECT_NAME}
#	RUNTIME DESTINATION lib/${PROJECT_NAME}
#)

#install(TARGETS ${PROJECT_NAME}
#  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
#  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
#  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
#)

#install(DIRECTORY launch/
#  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/launch
#)

#install(DIRECTORY launch/
#  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/launch
#)
