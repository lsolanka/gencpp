cmake_minimum_required(VERSION 2.8.3)

include(cmake/HunterGate.cmake)
HunterGate(
    URL "https://github.com/lsolanka/hunter/archive/v0.19.210-3.tar.gz"
    SHA1 "6983937f6aa3f600c48f9040d2cbacafce0b8c45"
)

project(gencpp)

hunter_add_package(ros-catkin)
hunter_add_package(ros-genmsg)

find_package(catkin REQUIRED COMPONENTS genmsg)

catkin_package(
  CATKIN_DEPENDS genmsg
  CFG_EXTRAS gencpp-extras.cmake
)

add_subdirectory(scripts)

file(WRITE ${CATKIN_DEVEL_PREFIX}/${GENMSG_LANGS_DESTINATION}/gencpp "C++")
install(FILES ${CATKIN_DEVEL_PREFIX}/${GENMSG_LANGS_DESTINATION}/gencpp
  DESTINATION ${GENMSG_LANGS_DESTINATION})

catkin_python_setup()
