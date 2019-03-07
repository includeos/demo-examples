cmake_minimum_required(VERSION 3.0)

#service
project (tcpperf)

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
    service.cpp # ...add more here
)

os_add_executable(tcp_perf_service "TCP benchmarking" ${SOURCES})

if ("$ENV{PLATFORM}" STREQUAL "x86_solo5")
  os_add_drivers(tcp_perf_service
      solo5net
      #solo5blk
    )
else()
  os_add_drivers(tcp_perf_service
    virtionet
    vmxnet3
    e1000
    boot_logger
  )
endif()

os_add_stdout(tcp_perf_service default_stdout)
os_add_plugins(tcp_perf_service autoconf)
