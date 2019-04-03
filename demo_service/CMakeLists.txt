cmake_minimum_required(VERSION 3.0)

#Avoid cmake from test compiling to host
set(CMAKE_TRY_COMPILE_TARGET_TYPE STATIC_LIBRARY)

project (demo_service)
if (NOT DEFINED CONAN_DEPENDENCIES)
  include(${CMAKE_CURRENT_BINARY_DIR}/conanbuildinfo.cmake OPTIONAL RESULT_VARIABLE HAS_CONAN)
  if (NOT HAS_CONAN)
    message(FATAL_ERROR "missing conanbuildinfo.cmake did you forget to run conan install ?")
  endif()
endif()
conan_basic_setup()

include(os)

set(SOURCES
  service.cpp
)

os_add_executable(demo "IncludeOS Demo Service" ${SOURCES})

# DRIVERS / PLUGINS:

if ("$ENV{PLATFORM}" STREQUAL "x86_solo5")
  os_add_drivers(demo solo5net)
else()
  os_add_drivers(demo
    virtionet     # Virtio networking
    vmxnet3
    boot_logger   # Display boot information
    # Use "boot --drivers ." to see other drivers
    # virtioblk # Virtio block device
    # ... Others from src/drivers
  )
endif()

os_add_stdout(demo default_stdout)
os_add_plugins(demo autoconf)
