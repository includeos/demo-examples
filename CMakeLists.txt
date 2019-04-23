cmake_minimum_required(VERSION 3.0)

if (NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Release)
endif()

set(EXAMPLES
  256_color_vga
  acorn
  demo_service
  http_client
  IRCd
  LiveUpdate
  microLB
  router
  scoped_profiler
  snake
  starlight
  STREAM
  syslog
  tcp
  TCP_perf
  TLS_server
  transfer
  UDP_perf
  #TODO
  #userspace_demo
  vlan
  websocket
)
if (PROTOBUF)
  list(APPEND EXAMPLES protobuf)
endif()

if(NOT EXISTS "${CMAKE_BINARY_DIR}/conan.cmake")
   message(STATUS "Downloading conan.cmake from https://github.com/conan-io/cmake-conan")
   file(DOWNLOAD "https://github.com/conan-io/cmake-conan/raw/v0.13/conan.cmake"
                 "${CMAKE_BINARY_DIR}/conan.cmake")
endif()

include(${CMAKE_BINARY_DIR}/conan.cmake)

if (CONAN_PROFILE)
  set(CONANPROFILE PROFILE ${CONAN_PROFILE})
endif()

foreach(example ${EXAMPLES})
  if (EXISTS  ${CMAKE_CURRENT_SOURCE_DIR}/${example}/conanfile.txt)
    set(OLD_DIR ${CMAKE_CURRENT_BINARY_DIR})
    set(CMAKE_CURRENT_BINARY_DIR ${OLD_DIR}/${example})
    file(MAKE_DIRECTORY ${OLD_DIR}/${example})
    #clear any old libs from last pass.. this is a ugly hack
    set(CONAN_LIBS "")
    conan_cmake_run(
      CONANFILE ${example}/conanfile.txt
      ${CONANPROFILE}
    )
    set(CMAKE_CURRENT_BINARY_DIR ${OLD_DIR})
  endif()
  #we cant add the subdir unless conan install is already run
  #because the CMakeLists.txt needs coanbuildinfo.cmake which is needed to find os.cmake
  add_subdirectory(${example} ${example})
endforeach()
