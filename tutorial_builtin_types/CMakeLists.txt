

add_executable(tutorial_slam2d_w_builtinTypes
  tutorial_slam2d.cpp
  simulator.cpp
  simulator.hpp
)

target_link_libraries(tutorial_slam2d_w_builtinTypes ${G2O_LIBRARIES} fmt)
