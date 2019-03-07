cmake_minimum_required(VERSION 3.0)

#service
project(router_service C CXX)

#check if conan is already run outside of project
if (NOT DEFINED CONAN_DEPENDENCIES)
  include(${CMAKE_CURRENT_BINARY_DIR}/conanbuildinfo.cmake OPTIONAL RESULT_VARIABLE HAS_CONAN)
  if (NOT HAS_CONAN)
    message(FATAL_ERROR "missing conanbuildinfo.cmake did you forget to run conan install ?")
  endif()
endif()
conan_basic_setup()

include(os)
# Source file

os_add_executable(scoped_profiler_example "Scoped Profiler Example" service.cpp)
# Human-readable name of your service
os_add_drivers(scoped_profiler_example
  virtionet
)
