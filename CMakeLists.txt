cmake_minimum_required(VERSION 3.0)

if (NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Release)
endif()

set(EXAMPLES
  256_color_vga

  acorn
  demo_service
#missing certs bundle..
#  http_client
#missing pmr (HAL)
#  IRCd
#  LiveUpdate
  #missing lua
#  lua5
# unknown wrong libc ?
#  mender
# waiting for conan package
#  microLB
  protobuf

  router
  scoped_profiler
  snake

  # TODO make a conan package instead of git-subdirectory
  #SQlite
  starlight
  STREAM
  syslog
  tcp
  TCP_perf
  TLS_server
  #TODO wait for hal
  #transfer
  UDP_perf
  #TODO
  #userspace_demo
  vlan
  #TODO wait for hal
  #websocket
)

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
