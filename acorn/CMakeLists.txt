cmake_minimum_required(VERSION 3.1.2)

#service
project (acorn)
if (NOT DEFINED CONAN_DEPENDENCIES)
  include(${CMAKE_CURRENT_BINARY_DIR}/conanbuildinfo.cmake OPTIONAL RESULT_VARIABLE HAS_CONAN)
  if (NOT HAS_CONAN)
    message(FATAL_ERROR "missing conanbuildinfo.cmake did you forget to run conan install ?")
  endif()
endif()

conan_basic_setup()

include(os)
include(dependencies.cmake)

set(SOURCES
  service.cpp fs/acorn_fs.cpp
)

os_add_config(acorn "${CMAKE_CURRENT_SOURCE_DIR}/config.json")

os_add_executable(acorn "Acorn Web Appliance" ${SOURCES})

#TODO conanify bucket ?
os_include_directories(acorn PRIVATE "app/" ${BUCKET_DIR})


# Make sure bucket is downloaded before service is built
os_add_dependencies(acorn bucket)

# DRIVERS / PLUGINS:

if ("$ENV{PLATFORM}" STREQUAL "x86_solo5")
  os_add_drivers(acorn solo5net)
else()
  os_add_drivers(acorn
    virtionet     # Virtio networking
    vmxnet3
  )
endif()
os_add_plugins(acorn autoconf)
os_add_stdout(acorn default_stdout)

#imported from the conanfile.txt
#os_add_os_library(acorn mana)

# Build memdisk content
os_diskbuilder(acorn disk1)
