cmake_minimum_required(VERSION 2.8.3)
project(rosconsole_bridge)

find_package(catkin REQUIRED COMPONENTS rosconsole)
find_package(console_bridge REQUIRED)

include_directories(include ${console_bridge_INCLUDE_DIRS} ${catkin_INCLUDE_DIRS})
link_directories(${catkin_LIBRARY_DIRS})

catkin_package(
  INCLUDE_DIRS include
  LIBRARIES ${PROJECT_NAME}
  CATKIN_DEPENDS rosconsole
  DEPENDS console_bridge 
)

add_library(${PROJECT_NAME} src/bridge.cpp)

target_link_libraries(${PROJECT_NAME} ${console_bridge_LIBRARIES} ${catkin_LIBRARIES})

install(
  TARGETS ${PROJECT_NAME}
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
)

install(
  DIRECTORY include/
  DESTINATION include
  FILES_MATCHING PATTERN "*.h"
)
