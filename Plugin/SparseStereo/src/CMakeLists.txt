cmake_minimum_required(VERSION 3.10)

PROJECT(SparseStereo)
MESSAGE(${PROJECT_NAME} ":")

MESSAGE(${PROJECT_NAME} " Begin")

SET(ROOT ${CMAKE_CURRENT_SOURCE_DIR})

SET(CMAKE_CXX_FLAGS "-std=c++11 ${CMAKE_CXX_FLAGS}")
SET(RW_ROOT ~/RobWork/RobWork)
set(CMAKE_VERBOSE_MAKEFILE false)
SET(CMAKE_BUILD_TYPE Release)

MESSAGE("-- Build types: " ${CMAKE_BUILD_TYPE})
SET(RobWork_DIR ${RW_ROOT}/cmake) 

FIND_PACKAGE(RobWork REQUIRED)
find_package(OpenCV REQUIRED)
find_package(PCL 1.4 REQUIRED)

include_directories(${PCL_INCLUDE_DIRS} ${ROBWORK_INCLUDE_DIRS} ${ROBWORKSTUDIO_INCLUDE_DIRS})
link_directories(${PCL_LIBRARY_DIRS} ${ROBWORK_LIBRARY_DIRS} ${ROBWORKSTUDIO_LIBRARY_DIRS})
add_definitions(${PCL_DEFINITIONS})
add_definitions(-DQT_NO_KEYWORDS)

INCLUDE_DIRECTORIES( ${ROBWORK_INCLUDE_DIRS} )
LINK_DIRECTORIES( ${ROBWORK_LIBRARY_DIRS} )

SET(SrcFiles main.cpp sparseStereo.cpp sparseStereo.hpp)

ADD_EXECUTABLE(SparseStereo ${SrcFiles})
TARGET_LINK_LIBRARIES(SparseStereo ${ROBWORK_LIBRARIES} ${PCL_LIBRARIES} ${OpenCV_LIBS})

MESSAGE(${PROJECT_NAME} " completed!")
