#---Do not build roofit with modules until the issue gets fixed-----------------
if(cxxmodules)
  if(ROOT_ARCHITECTURE MATCHES macosx)
    string(REPLACE "${ROOT_CXXMODULES_FLAGS}" "" CMAKE_CXX_FLAGS ${CMAKE_CXX_FLAGS})
    string(REPLACE "${ROOT_CXXMODULES_FLAGS}" "" CMAKE_C_FLAGS ${CMAKE_C_FLAGS})
  endif()
endif(cxxmodules)

if(NOT CMAKE_PROJECT_NAME STREQUAL ROOT)
  cmake_minimum_required(VERSION 2.8 FATAL_ERROR)
  project(RooFit)
  find_package(ROOT REQUIRED)
  include(${ROOT_USE_FILE})
endif()

if(mathmore OR ROOT_mathmore_FOUND)
  set(ROOT_MATHMORE_LIBRARY MathMore)
endif()

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/roofit/inc) 
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/roofitcore/inc) 
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/roostats/inc) 

add_subdirectory(roofitcore)
add_subdirectory(roofit)
add_subdirectory(roostats)
if(xml OR ROOT_xml_FOUND)
  add_subdirectory(histfactory)
endif()


