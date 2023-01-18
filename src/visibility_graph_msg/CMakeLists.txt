cmake_minimum_required(VERSION 3.19)

project("visibility_graph_msg")

set(VERBOSE ON)
set(CMAKE_VERBOSE_MAKEFILE ON)

set(CMAKE_CXX_STANDARD 17)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Werror")
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -Werror")

# ROS dependencies
#ament_export_dependencies(rosidl_default_runtime)

find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(std_msgs REQUIRED)
find_package(builtin_interfaces REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(rosidl_default_generators REQUIRED)

rosidl_generate_interfaces(${PROJECT_NAME} "./msg/Node.msg" "./msg/Graph.msg" 
	DEPENDENCIES builtin_interfaces std_msgs geometry_msgs)

# Bin folder
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_SOURCE_DIR}/bin")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${CMAKE_SOURCE_DIR}/bin")
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_SOURCE_DIR}/bin")

# Path to shared library folder
set(CMAKE_INSTALL_RPATH "${CMAKE_SOURCE_DIR}/bin")

#ament_target_dependencies(${PROJECT_NAME} rclcpp geometry_msgs std_msgs)

# ROS
ament_package()
#install(DIRECTORY launch DESTINATION share/${PROJECT_NAME})
