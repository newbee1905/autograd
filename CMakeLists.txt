cmake_minimum_required(VERSION 3.10...3.29)

project(
	autograd
  VERSION 1.0
  LANGUAGES CXX
)

set(CMAKE_GENERATOR Ninja)

# update submodules
add_custom_target(update_dependencies
	COMMAND ${PROXY} git submodule foreach git pull
	WORKING_DIRECTORY ${CMAKE_CURRENT_LIST_DIR}
)

# cpp compiler settings
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED TRUE)
set(CMAKE_CXX_EXTENSIONS OFF)

# cpp flags
set(CMAKE_CXX_FLAGS_DEBUG_INIT "-Wall")
set(CMAKE_CXX_FLAGS_RELEASE_INIT "-Wall")

set(CMAKE_CXX_FLAGS_DEBUG "-Og")
set(CMAKE_CXX_FLAGS_RELEASE "-D_REENTRANT -mavx2 -mbmi2 -O3 -flto=auto")

# adding deps
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/deps/fmt)
link_libraries(fmt::fmt)

# configure project structure
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)
add_subdirectory(src)

