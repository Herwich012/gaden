cmake_minimum_required(VERSION 3.5)
project(gaden_player)

set(CMAKE_BUILD_TYPE "None") 
set(CMAKE_CXX_FLAGS "-std=c++17 ${CMAKE_CXX_FLAGS}")

set(DEBUG OFF)

if(DEBUG)
  add_definitions(-DDEBUG)
  set(CMAKE_CXX_FLAGS "-g ${CMAKE_CXX_FLAGS}")
else()
  set(CMAKE_CXX_FLAGS "-O3 ${CMAKE_CXX_FLAGS}")
endif(DEBUG) 



find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(std_msgs REQUIRED)
find_package(visualization_msgs REQUIRED)
find_package(fmt REQUIRED)

find_package(Boost REQUIRED COMPONENTS iostreams)

find_package(rosidl_default_generators REQUIRED)
rosidl_generate_interfaces(${PROJECT_NAME}
    msg/GasInCell.msg
    srv/GasPosition.srv
    srv/WindPosition.srv
    DEPENDENCIES std_msgs
)
ament_export_dependencies(rosidl_default_runtime)

include_directories(include
../gaden_common/include)

FILE(GLOB_RECURSE MYFILES_CPP "src/*.cpp")
add_executable(player  ${MYFILES_CPP})





# dependency for self-defined messages
if("${ROS_DISTRO}" STREQUAL "foxy")
  rosidl_target_interfaces(player
    ${PROJECT_NAME} "rosidl_typesupport_cpp")
else()
  rosidl_get_typesupport_target(cpp_typesupport_target ${PROJECT_NAME} "rosidl_typesupport_cpp")
  target_link_libraries(player "${cpp_typesupport_target}") 
endif()



ament_target_dependencies(player
    rclcpp
    std_msgs
    visualization_msgs
    Boost
) 
target_link_libraries(player fmt)


install(
  TARGETS player
  DESTINATION lib/${PROJECT_NAME}
)
ament_package()
