cmake_minimum_required(VERSION 3.0)

#check if conan is already run outside of project
if (NOT DEFINED CONAN_DEPENDENCIES)
  include(${CMAKE_CURRENT_BINARY_DIR}/conanbuildinfo.cmake OPTIONAL RESULT_VARIABLE HAS_CONAN)
  if (NOT HAS_CONAN)
    message(FATAL_ERROR "missing conanbuildinfo.cmake did you forget to run conan install ?")
  endif()
endif()
conan_basic_setup()

#service
project (microLB)
include(os)

set(SOURCES
  service.cpp
)

os_add_executable(microlb_example "microLB Service" ${SOURCES})

# DRIVERS / PLUGINS:

if ("$ENV{PLATFORM}" STREQUAL "x86_solo5")
  os_add_drivers(microlb_example solo5net)
else()
  os_add_drivers(microlb_example
    virtionet     # Virtio networking
    vmxnet3
    boot_logger   # Display boot information
    # Use "boot --drivers ." to see other drivers
    # virtioblk # Virtio block device
    # ... Others from src/drivers
  )
endif()

os_add_stdout(microlb_example default_stdout)
#os_add_os_library(microlb liveupdate)
#os_add_os_library(microlb microlb)
# os_add_plugins( ... )
