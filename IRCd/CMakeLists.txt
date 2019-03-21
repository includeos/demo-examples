cmake_minimum_required(VERSION 3.0)

#Avoid cmake from test compiling to host
set(CMAKE_TRY_COMPILE_TARGET_TYPE STATIC_LIBRARY)

option(REAL_HW "Run on real hardware" OFF)
option(LIVEUPDATE "Enable liveupdate" ON)

#service
project (ircd_example)
if (NOT DEFINED CONAN_DEPENDENCIES)
  include(${CMAKE_CURRENT_BINARY_DIR}/conanbuildinfo.cmake OPTIONAL RESULT_VARIABLE HAS_CONAN)
  if (NOT HAS_CONAN)
    message(FATAL_ERROR "missing conanbuildinfo.cmake did you forget to run conan install ?")
  endif()
endif()
conan_basic_setup()

include(os)

add_subdirectory(ircd)

os_add_executable(ircd_example "IRC service"  service.cpp autoconf.cpp)
os_add_drivers(ircd_example vmxnet3)
os_add_plugins(ircd_example autoconf)
os_add_stdout(ircd_example default_stdout)
os_link_libraries(ircd_example ircd)
