cmake_minimum_required(VERSION 3.0.2)
project(command)

find_package(catkin REQUIRED COMPONENTS
  message_generation
  rospy
  roscpp
  std_msgs
)

add_message_files(
  FILES
  HardwareCommand.msg
  HardwareState.msg
)

add_service_files(
  FILES
  MakeStop.srv
)

generate_messages(
  DEPENDENCIES
  std_msgs
)

catkin_package(
  INCLUDE_DIRS include
  CATKIN_DEPENDS message_runtime rospy roscpp std_msgs
#  DEPENDS system_lib
)

include_directories(
  include
  ${catkin_INCLUDE_DIRS}
)

add_library(${PROJECT_NAME}
  src/hardware_command.cpp
)

add_executable(${PROJECT_NAME}_node src/hardware_command.cpp)
add_dependencies(${PROJECT_NAME}_node ${catkin_EXPORTED_TARGETS})

target_link_libraries(${PROJECT_NAME}_node
  ${catkin_LIBRARIES}
)

install(PROGRAMS
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)

