cmake_minimum_required(VERSION 2.8.3)

include(cmake/HunterGate.cmake)
HunterGate(
    URL "https://github.com/lsolanka/hunter/archive/v0.19.210-3.tar.gz"
    SHA1 "6983937f6aa3f600c48f9040d2cbacafce0b8c45"
)

project(gennodejs)

hunter_add_package(ros-catkin)
hunter_add_package(ros-genmsg)

find_package(catkin REQUIRED COMPONENTS genmsg)

catkin_package(
  CATKIN_DEPENDS genmsg
  CFG_EXTRAS gennodejs-extras.cmake
)

add_subdirectory(scripts)

file(WRITE ${CATKIN_DEVEL_PREFIX}/${GENMSG_LANGS_DESTINATION}/gennodejs "JAVASCRIPT")
install(FILES ${CATKIN_DEVEL_PREFIX}/${GENMSG_LANGS_DESTINATION}/gennodejs
  DESTINATION ${GENMSG_LANGS_DESTINATION})

# drop marker file to prevent rospack from spending time on crawling this folder
#file(WRITE ${CATKIN_DEVEL_PREFIX}/share/nodejs/rospack_nosubdirs "")
#install(FILES ${CATKIN_DEVEL_PREFIX}/share/nodejs/rospack_nosubdirs
#  DESTINATION share/nodejs)

catkin_python_setup()
