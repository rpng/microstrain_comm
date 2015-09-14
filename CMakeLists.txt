cmake_minimum_required(VERSION 2.8.3)
project(microstrain_comm)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  sensor_msgs
)

find_package(GTK2)
add_definitions(-DHAVE_GTK)
include_directories(SYSTEM ${GTK2_INCLUDE_DIRS})

catkin_package(
  CATKIN_DEPENDS
    roscpp
    sensor_msgs
)


# Our includes
include_directories(
  include
  ${catkin_INCLUDE_DIRS}
  ${GTK2_LIBRARIES}
  ${PROJECT_SOURCE_DIR}
)

# Files that we need to build
add_executable(${PROJECT_NAME}_node
  src/micro/microstrain_comm.cpp
  src/libbot/ringbuf.c
  src/libbot/rotations.c
  src/libbot/serial.c
  src/libbot/timestamp.c
)

# # pull in the pods macros. See cmake/pods.cmake for documentation
# set(POD_NAME microstrain_comm)
# include(cmake/pods.cmake)

# # automatically build LCM types.  This also defines a number of CMake
# # variables, see cmake/lcmtypes.cmake for details
# include(cmake/lcmtypes.cmake)
# lcmtypes_build()

# # create an executable, and make it public
# add_executable(microstrain_comm src/microstrain_comm.cpp)
# pods_use_pkg_config_packages(microstrain_comm bot2-core lcmtypes_microstrain_comm bot2-param-client)
# pods_install_executables(microstrain_comm)


# # pass through microstrain_comm quaternion as a bot_core_pose_t (for simple visualization)
# add_executable(microstrain_pose src/microstrain_pose.cpp)
# pods_use_pkg_config_packages(microstrain_pose lcmtypes_microstrain_comm)
# pods_install_executables(microstrain_pose)
