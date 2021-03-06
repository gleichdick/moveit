if (CATKIN_ENABLE_TESTING)
  find_package(moveit_resources REQUIRED)
  find_package(rostest REQUIRED)
  find_package(eigen_conversions REQUIRED)

  add_executable(test_cleanup test_cleanup.cpp)
  target_link_libraries(test_cleanup moveit_move_group_interface)

  add_rostest_gtest(moveit_cpp_test moveit_cpp_test.test moveit_cpp_test.cpp)
  target_link_libraries(moveit_cpp_test moveit_cpp ${catkin_LIBRARIES})

  add_rostest_gtest(subframes_test subframes_test.test subframes_test.cpp)
  target_link_libraries(subframes_test moveit_move_group_interface
	                     ${catkin_LIBRARIES} ${eigen_conversions_LIBRARIES})

  catkin_add_gtest(test_serialize_msg_python test_serialize_msg_python.cpp)
  target_link_libraries(test_serialize_msg_python
                        ${Boost_LIBRARIES} ${PYTHON_LIBRARIES} ${catkin_LIBRARIES})

  add_rostest(python_move_group.test)
  add_rostest(python_move_group_ns.test)
  add_rostest(robot_state_update.test)
  add_rostest(cleanup.test)
endif()
