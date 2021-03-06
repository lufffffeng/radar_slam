cmake_minimum_required(VERSION 2.8.3)
set(CMAKE_CXX_STANDARD 11)

project(radar_slam)

find_package (Eigen3 3.3 REQUIRED NO_MODULE)
find_package(catkin REQUIRED COMPONENTS
  roscpp
  std_msgs
  visualization_msgs
  tf2
  tf2_ros
  ainstein_radar_msgs
  car_data_interface
  piksi_rtk_msgs
)

catkin_package()


include_directories(
 include
 ${catkin_INCLUDE_DIRS}
)

add_executable(gps_base_tf_broadcaster_node src/gps_base_tf_broadcaster.cpp)
add_dependencies(gps_base_tf_broadcaster_node ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})
target_link_libraries(gps_base_tf_broadcaster_node ${catkin_LIBRARIES} Eigen3::Eigen)

add_executable(car_joint_state_pub_node src/car_joint_state_pub_node.cpp)
add_dependencies(car_joint_state_pub_node ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})
target_link_libraries(car_joint_state_pub_node ${catkin_LIBRARIES} Eigen3::Eigen)


#add_executable(base_tf_broadcaster_node src/base_tf_broadcaster.cpp src/car_pose_estimator.cpp)
#add_dependencies(base_tf_broadcaster_node ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})
#target_link_libraries(base_tf_broadcaster_node ${catkin_LIBRARIES} Eigen3::Eigen)

#add_executable(odom_tf_broadcaster_node src/odom_tf_broadcaster.cpp src/geometry_utils.cpp)
#add_dependencies(odom_tf_broadcaster_node ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})
#target_link_libraries(odom_tf_broadcaster_node ${catkin_LIBRARIES} Eigen3::Eigen)

install(TARGETS
  gps_base_tf_broadcaster_node
  car_joint_state_pub_node
#  base_tf_broadcaster_node
#  odom_tf_broadcaster_node
   ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
   LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
   RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

