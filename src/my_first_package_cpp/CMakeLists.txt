cmake_minimum_required(VERSION 3.8)
project(my_first_package_cpp)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(turtlesim REQUIRED)

# ----------------------------------------------------------------------

# my_first_node_cpp
add_executable(my_first_node_cpp src/my_first_node_cpp.cpp)
target_include_directories(my_first_node_cpp PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
  $<INSTALL_INTERFACE:include/${PROJECT_NAME}>)
target_compile_features(my_first_node_cpp PUBLIC c_std_99 cxx_std_17)  # Require C99 and C++17

install(TARGETS my_first_node_cpp
  DESTINATION lib/${PROJECT_NAME})

# my_publisher_cpp
add_executable(move_turtle src/my_publisher_cpp.cpp)
target_include_directories(move_turtle PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
  $<INSTALL_INTERFACE:include/${PROJECT_NAME}>)
target_compile_features(move_turtle PUBLIC c_std_99 cxx_std_17)

ament_target_dependencies(move_turtle rclcpp geometry_msgs)

install(TARGETS move_turtle
  DESTINATION lib/${PROJECT_NAME})
  
# my_subscription_cpp
add_executable(my_subscription_cpp src/my_subscription_cpp.cpp)
target_include_directories(my_subscription_cpp PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
  $<INSTALL_INTERFACE:include/${PROJECT_NAME}>)
target_compile_features(my_subscription_cpp PUBLIC c_std_99 cxx_std_17)

ament_target_dependencies(my_subscription_cpp rclcpp turtlesim)

install(TARGETS my_subscription_cpp
  DESTINATION lib/${PROJECT_NAME})

# ----------------------------------------------------------------------

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  # the following line skips the linter which checks for copyrights
  # comment the line when a copyright and license is added to all source files
  set(ament_cmake_copyright_FOUND TRUE)
  # the following line skips cpplint (only works in a git repo)
  # comment the line when this package is in a git repo and when
  # a copyright and license is added to all source files
  set(ament_cmake_cpplint_FOUND TRUE)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()
