cmake_minimum_required(VERSION 2.8.3)
project(baxter_sim_kinematics)

find_package(catkin
  REQUIRED COMPONENTS
  roscpp
  baxter_core_msgs
  sensor_msgs
  tf
  tf_conversions
  kdl_parser
)

find_package(Boost REQUIRED COMPONENTS system)
find_package(Eigen REQUIRED)

catkin_package(
  INCLUDE_DIRS include
  CATKIN_DEPENDS
  std_msgs
  baxter_core_msgs
  sensor_msgs
  LIBRARIES ${PROJECT_NAME}
)

include_directories(include
  ${catkin_INCLUDE_DIRS}
  ${Boost_INCLUDE_DIRS}
  ${EIGEN_INCLUDE_DIRS}
)
 
add_library(${PROJECT_NAME} src/arm_kinematics.cpp)
target_link_libraries(${PROJECT_NAME} ${catkin_LIBRARIES})

add_executable(kinematics src/position_kinematics.cpp)
target_link_libraries(kinematics ${catkin_LIBRARIES} ${PROJECT_NAME})

 add_dependencies(kinematics
  ${catkin_EXPORTED_TARGETS}
  baxter_core_msgs_gencpp
 )