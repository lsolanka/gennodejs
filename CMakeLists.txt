cmake_minimum_required(VERSION 2.8.3)

include(cmake/HunterGate.cmake)
HunterGate(
    URL "https://github.com/lsolanka/hunter/archive/4ecf66e071495981031fdfa99aad576405537266.tar.gz"
    SHA1 "727648f578f3cbcb6ea0e644bd8b0111e56688bc"
    LOCAL
)

project(gennodejs)

hunter_add_package(catkin)
hunter_add_package(genmsg)

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
