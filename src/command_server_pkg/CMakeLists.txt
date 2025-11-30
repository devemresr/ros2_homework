cmake_minimum_required(VERSION 3.8)
project(command_server_pkg)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# Find dependencies
find_package(ament_cmake REQUIRED)
find_package(rosidl_default_generators REQUIRED)
find_package(rclpy REQUIRED)

# Generate service interfaces
rosidl_generate_interfaces(${PROJECT_NAME}
  "srv/ComputeCommand.srv"
)

# Install Python scripts
install(PROGRAMS
  command_server_pkg/command_server.py
  DESTINATION lib/${PROJECT_NAME}
  RENAME command_server
)

ament_package()
