cmake_minimum_required(VERSION 2.8.3)
project(ca_driver)

find_package(catkin REQUIRED COMPONENTS
  ca_msgs
  diagnostic_msgs
  diagnostic_updater
  geometry_msgs
  nav_msgs
  roscpp
  sensor_msgs
  std_msgs
  tf
)

find_package(Boost REQUIRED system thread)
find_package(libcreate CONFIG REQUIRED)

catkin_package(
  INCLUDE_DIRS include
  CATKIN_DEPENDS
    ca_description
    ca_msgs
    diagnostic_msgs
    diagnostic_updater
    geometry_msgs
    nav_msgs
    roscpp
    sensor_msgs
    std_msgs
    tf
  DEPENDS libcreate
)

include_directories(
  ${catkin_INCLUDE_DIRS}
#  ${Boost_INCLUDE_DIRS}
  include
)


add_executable(${PROJECT_NAME} src/create_driver.cpp)

target_link_libraries(${PROJECT_NAME}
#  create
  libcreate::create
  ${catkin_LIBRARIES}
#  ${Boost_LIBRARIES}
)

install(TARGETS ${PROJECT_NAME}
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

install(DIRECTORY include
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
  FILES_MATCHING PATTERN "*.h"
  PATTERN ".svn" EXCLUDE
)

install(DIRECTORY launch/
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/launch
  PATTERN ".svn" EXCLUDE
)

install(DIRECTORY config/
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/config
  PATTERN ".svn" EXCLUDE
)
