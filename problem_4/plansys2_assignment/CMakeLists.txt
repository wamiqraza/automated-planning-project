cmake_minimum_required(VERSION 3.5)
project(plansys2_assignment)


find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(rclcpp_action REQUIRED)
find_package(plansys2_msgs REQUIRED)
find_package(plansys2_executor REQUIRED)

set(CMAKE_CXX_STANDARD 17)

set(dependencies
    rclcpp
    rclcpp_action
    plansys2_msgs
    plansys2_executor
)

add_executable(back_to_warehouse_action_node src/back_to_warehouse_action_node.cpp)
ament_target_dependencies(back_to_warehouse_action_node ${dependencies})

add_executable(move_for_delivery_action_node src/move_for_delivery_action_node.cpp)
ament_target_dependencies(move_for_delivery_action_node ${dependencies})

add_executable(load_action_node src/load_action_node.cpp)
ament_target_dependencies(load_action_node ${dependencies})

add_executable(unload_action_node src/unload_action_node.cpp)
ament_target_dependencies(unload_action_node ${dependencies})

install(DIRECTORY launch pddl DESTINATION share/${PROJECT_NAME})

install(TARGETS
  back_to_warehouse_action_node
  move_for_delivery_action_node
  load_action_node
  unload_action_node
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
  RUNTIME DESTINATION lib/${PROJECT_NAME}
)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  ament_lint_auto_find_test_dependencies()

  find_package(ament_cmake_gtest REQUIRED)
endif()

ament_export_dependencies(${dependencies})

ament_package()