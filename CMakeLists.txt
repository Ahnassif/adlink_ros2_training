cmake_minimum_required(VERSION 3.5)
project(adlink_ros2_training)

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(rcutils REQUIRED)
find_package(std_msgs REQUIRED)
find_package(geometry_msgs REQUIRED)

# adlink_talker
add_executable(adlink_talker src/adlink_talker.cpp)
ament_target_dependencies(adlink_talker rclcpp std_msgs)

# adlink_talker_qos
add_executable(adlink_talker_qos src/adlink_talker_qos.cpp)
ament_target_dependencies(adlink_talker_qos rclcpp std_msgs)

# nonstop_demo
add_executable(nonstop_demo src/nonstop_demo.cpp)
ament_target_dependencies(nonstop_demo rclcpp geometry_msgs)

# pose_subscriber
add_executable(pose_subscriber src/pose_subscriber.cpp)
ament_target_dependencies(pose_subscriber rclcpp geometry_msgs)

# transform_sub
add_executable(transform_sub src/transform_sub.cpp)
ament_target_dependencies(transform_sub rclcpp geometry_msgs)

install(TARGETS
  adlink_talker
  adlink_talker_qos
  nonstop_demo
  pose_subscriber
  transform_sub
  DESTINATION lib/${PROJECT_NAME}
)

ament_package()