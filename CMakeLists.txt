cmake_minimum_required(VERSION 2.8.12)
project(g2o_tutorial_slam2d)

if (POLICY CMP0072)
  set(OpenGL_GL_PREFERENCE LEGACY)
endif()

# add g2o dependencies

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake_modules)
find_package(G2O REQUIRED)
# CSparse
find_package(CSparse  REQUIRED)
include_directories(${G2O_INCLUDE_DIR} ${CSPARSE_INCLUDE_DIR})

message(STATUS "G2O_FOUND: ${G2O_FOUND}")

set(G2O_LIBRARIES
  ${G2O_STUFF_LIBRARY}
  ${G2O_CORE_LIBRARY}
  ${G2O_CLI_LIBRARY}
  ${G2O_SOLVER_CHOLMOD}
  ${G2O_SOLVER_CSPARSE}
  ${G2O_SOLVER_CSPARSE_EXTENSION}
  ${G2O_SOLVER_DENSE}
  ${G2O_SOLVER_PCG}
  ${G2O_SOLVER_SLAM2D_LINEAR}
  ${G2O_SOLVER_STRUCTURE_ONLY}
  ${G2O_SOLVER_EIGEN}
  ${G2O_TYPES_DATA}
  ${G2O_TYPES_ICP}
  ${G2O_TYPES_SBA}
  ${G2O_TYPES_SCLAM2D}
  ${G2O_TYPES_SIM3}
  ${G2O_TYPES_SLAM2D}
  ${G2O_TYPES_SLAM3D})

set(G2O_LIB_TYPE
  ${G2O_TYPES_DATA}
  ${G2O_TYPES_ICP}
  ${G2O_TYPES_SBA}
  ${G2O_TYPES_SCLAM2D}
  ${G2O_TYPES_SIM3}
  ${G2O_TYPES_SLAM2D}
  ${G2O_TYPES_SLAM3D})
# message(STATUS "G2O_LIBRARIES: ${G2O_LIBRARIES}")

find_package(Eigen3 REQUIRED)

add_library(tutorial_slam2d_library SHARED
  edge_se2_pointxy.cpp  se2.h                vertex_point_xy.h
  edge_se2.cpp    edge_se2_pointxy.h    vertex_se2.cpp
  edge_se2.h      vertex_point_xy.cpp  vertex_se2.h
  parameter_se2_offset.h parameter_se2_offset.cpp
  types_tutorial_slam2d.h types_tutorial_slam2d.cpp
  simulator.h simulator.cpp
  g2o_tutorial_slam2d_api.h
)

set_target_properties(tutorial_slam2d_library PROPERTIES OUTPUT_NAME ${LIB_PREFIX}tutorial_slam2d)
set_target_properties(tutorial_slam2d_library PROPERTIES
  VERSION ${G2O_LIB_VERSION}
  SOVERSION ${G2O_LIB_SOVERSION})

target_link_libraries(tutorial_slam2d_library ${G2O_LIBRARIES})
include_directories(${G2O_INCLUDE_DIR} ${EIGEN3_INCLUDE_DIR})

add_executable(tutorial_slam2d
  tutorial_slam2d.cpp
)

set_target_properties(tutorial_slam2d PROPERTIES OUTPUT_NAME tutorial_slam2d)

target_link_libraries(tutorial_slam2d tutorial_slam2d_library fmt)

message(STATUS "PROJECT_SOURCE_DIR: ${PROJECT_SOURCE_DIR}")
add_subdirectory(${PROJECT_SOURCE_DIR}/tutorial_builtin_types)