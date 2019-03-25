cmake_minimum_required(VERSION 3.0)

#Avoid cmake from test compiling to host
set(CMAKE_TRY_COMPILE_TARGET_TYPE STATIC_LIBRARY)

project (mender_demo)
if (NOT DEFINED CONAN_DEPENDENCIES)
  include(${CMAKE_CURRENT_BINARY_DIR}/conanbuildinfo.cmake OPTIONAL RESULT_VARIABLE HAS_CONAN)
  if (NOT HAS_CONAN)
    message(FATAL_ERROR "missing conanbuildinfo.cmake did you forget to run conan install ?")
  endif()
endif()
conan_basic_setup()

include(os)


os_add_executable(mender_demo "IncludeOS Mender Example" service.cpp)
os_add_drivers(mender_demo virtionet vmxnet3)
#include($ENV{INCLUDEOS_PREFIX}/includeos/post.service.cmake)

# Build private key into disk
#nod idea if this is correct
os_diskbuilder(mender_demo disk)
