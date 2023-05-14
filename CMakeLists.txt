cmake_minimum_required(VERSION 3.5.0)
project(roboticsgroup_upatras_gazebo_plugins)

find_package(ament_cmake REQUIRED)
find_package(control_toolbox REQUIRED)
find_package(gazebo_dev REQUIRED)
find_package(gazebo_ros REQUIRED)
find_package(rclcpp REQUIRED)

# Default to C99
if(NOT CMAKE_C_STANDARD)
  set(CMAKE_C_STANDARD 99)
endif()

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

include_directories(include)
# include_directories("${control_toolbox_INCLUDE_DIRS}")

link_directories(
  ${gazebo_dev_LIBRARY_DIRS}
  )

# Libraries
add_library(roboticsgroup_upatras_gazebo_mimic_joint_plugin SHARED
  src/mimic_joint_plugin.cpp)
ament_target_dependencies(roboticsgroup_upatras_gazebo_mimic_joint_plugin
  gazebo_dev
  gazebo_ros
  control_toolbox
  rclcpp
  )

# Install
install(TARGETS
    roboticsgroup_upatras_gazebo_mimic_joint_plugin
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
  RUNTIME DESTINATION bin
)

ament_export_include_directories(
  include
  )

ament_export_dependencies(ament_cmake)
ament_export_dependencies(rclcpp)
ament_export_libraries(
  ${PROJECT_NAME}
  roboticsgroup_upatras_gazebo_mimic_joint_plugin
)

# install(DIRECTORY include/${PROJECT_NAME}
#   DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
# )

if(BUILD_TESTING)
  find_package(ament_cmake_gtest REQUIRED)
  find_package(ament_lint_auto REQUIRED)
  ament_lint_auto_find_test_dependencies()
endif()

install(DIRECTORY include/${PROJECT_NAME}/
  DESTINATION include/${PROJECT_NAME}
)

ament_package()




# catkin_package(
#   INCLUDE_DIRS
#     include
#   LIBRARIES
#     roboticsgroup_upatras_gazebo_mimic_joint_plugin
#     roboticsgroup_upatras_gazebo_disable_link_plugin
#   CATKIN_DEPENDS
#     control_toolbox
#     gazebo_ros
#     roscpp
# )

# include_directories(
#   include
#   ${catkin_INCLUDE_DIRS}
#   ${GAZEBO_INCLUDE_DIRS}
# )

# link_directories(${GAZEBO_LIBRARY_DIRS})

# set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${GAZEBO_CXX_FLAGS}")

# add_library(roboticsgroup_upatras_gazebo_mimic_joint_plugin src/mimic_joint_plugin.cpp)
# target_link_libraries(roboticsgroup_upatras_gazebo_mimic_joint_plugin ${catkin_LIBRARIES} ${GAZEBO_LIBRARIES})

# add_library(roboticsgroup_upatras_gazebo_disable_link_plugin src/disable_link_plugin.cpp)
# target_link_libraries(roboticsgroup_upatras_gazebo_disable_link_plugin ${catkin_LIBRARIES} ${GAZEBO_LIBRARIES})

# install(TARGETS
#     roboticsgroup_upatras_gazebo_mimic_joint_plugin
#     roboticsgroup_upatras_gazebo_disable_link_plugin
#   ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
#   LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
#   RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
# )

# install(DIRECTORY include/${PROJECT_NAME}
#   DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
# )

