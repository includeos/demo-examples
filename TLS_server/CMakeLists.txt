cmake_minimum_required(VERSION 3.0)

#Avoid cmake from test compiling to host
set(CMAKE_TRY_COMPILE_TARGET_TYPE STATIC_LIBRARY)


#service
project (tls_server)

#check if conan is already run outside of project
if (NOT DEFINED CONAN_DEPENDENCIES)
  include(${CMAKE_CURRENT_BINARY_DIR}/conanbuildinfo.cmake OPTIONAL RESULT_VARIABLE HAS_CONAN)
  if (NOT HAS_CONAN)
    message(FATAL_ERROR "missing conanbuildinfo.cmake did you forget to run conan install ?")
  endif()
endif()
conan_basic_setup()


include(os)

set(SOURCES
  service.cpp http.cpp
)


os_add_executable(tls_service "TLS server" ${SOURCES})

# DRIVERS / PLUGINS:

if ("$ENV{PLATFORM}" STREQUAL "x86_solo5")
  os_add_drivers(tls_service solo5net)
else()
  os_add_drivers(tls_service
    virtionet     # Virtio networking
    vmxnet3
  )
endif()
os_add_plugins(tls_service autoconf vfs)
os_add_stdout(tls_service default_stdout)

# Build memdisk content
os_diskbuilder(tls_service drive)
