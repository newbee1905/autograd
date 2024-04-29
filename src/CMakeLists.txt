get_filename_component(APP autograd NAME)
add_executable(${APP} main.cc)
add_library(kd lib.cc)
target_link_libraries(${APP} kd)
