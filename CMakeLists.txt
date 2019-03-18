cmake_minimum_required(VERSION 2.8.3)
project(random_numbers)

find_package(catkin REQUIRED)

catkin_package(
  LIBRARIES ${PROJECT_NAME}
  INCLUDE_DIRS include
  )

find_package(Boost REQUIRED date_time system thread)
include_directories(${Boost_INCLUDE_DIR})

include_directories(include)

add_library(${PROJECT_NAME}
  src/random_numbers.cpp)

target_link_libraries(${PROJECT_NAME} ${Boost_LIBRARIES})

if(WIN32)
  install(TARGETS ${PROJECT_NAME}
        RUNTIME DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
        CONFIGURATIONS ${CMAKE_BUILD_TYPE}
        ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
        LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION})
else()
  install(TARGETS ${PROJECT_NAME}
        ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
        LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION})
endif()

install(DIRECTORY include/${PROJECT_NAME}/
        DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION})
