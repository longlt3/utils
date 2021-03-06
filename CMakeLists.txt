cmake_minimum_required(VERSION 3.5 FATAL_ERROR)
PROJECT(ahuynq VERSION 0.1)

# print to console
MESSAGE( STATUS "Building with system: " ${CMAKE_SYSTEM_NAME})
# MESSAGE( STATUS "CC: " ${CMAKE_C_COMPILER})
# MESSAGE( STATUS "CXX: " ${CMAKE_CXX_COMPILER})
message(STATUS "CC : ")
execute_process(COMMAND ${CMAKE_C_COMPILER} -v)

message(STATUS "CXX : ")
execute_process(COMMAND ${CMAKE_CXX_COMPILER} -v)

IF(CMAKE_BUILD_TYPE STREQUAL "")
  SET(CMAKE_BUILD_TYPE Debug)
ENDIF()

IF(CMAKE_BUILD_TYPE STREQUAL "Debug")
  # Debug
  SET(CMAKE_C_FLAGS_DEBUG "-g -O0")
  ADD_DEFINITIONS(
    -DLOG_EN
  )
ELSEIF(CMAKE_BUILD_TYPE STREQUAL "Release")
  # Release
  SET(CMAKE_C_FLAGS_DEBUG "-O3")
  # ADD_DEFINITIONS(
  #   -DLOG_EN
  # )
ENDIF()

SET(CMAKE_SKIP_BUILD_RPATH TRUE)

# cxx flags
# SET(CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS_DEBUG} -Wall")
SET(CMAKE_CXX_FLAGS_DEBUG ${CMAKE_C_FLAGS_DEBUG})
SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -Wno-deprecated-declarations -Wno-reorder")

# set environments
SET(PRJ_ROOT ${CMAKE_CURRENT_SOURCE_DIR})

INCLUDE_DIRECTORIES(
	${PRJ_ROOT}
)

set( CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/${CMAKE_BUILD_TYPE} )
set( CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/${CMAKE_BUILD_TYPE} )

ADD_SUBDIRECTORY(libs)
ADD_SUBDIRECTORY(tests)
