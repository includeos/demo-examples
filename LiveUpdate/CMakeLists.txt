cmake_minimum_required(VERSION 3.0)

option(REAL_HW "Run on real hardware" OFF)
option(LIVEUPDATE "Enable liveupdate" OFF)

#service
project (liuircd)

if (NOT DEFINED CONAN_DEPENDENCIES)
  include(${CMAKE_CURRENT_BINARY_DIR}/conanbuildinfo.cmake OPTIONAL RESULT_VARIABLE HAS_CONAN)
  if (NOT HAS_CONAN)
    message(FATAL_ERROR "missing conanbuildinfo.cmake did you forget to run conan install ?")
  endif()
endif()
conan_basic_setup()

include(os)

if(TARGET ircd)
  message(STATUS "ircd is already defined")
else()
  add_subdirectory(../IRCd/ircd ircd)
endif()


set(DRIVERS
    vmxnet3
  )

set(STDOUT
  default_stdout
)

include_directories(
  ${CMAKE_CURRENT_BINARY_DIR}
  ../IRCd/ircd
)

SET(SRCS
  service.cpp
  ../IRCd/autoconf.cpp
)

os_add_executable(LiveUpdate_example "IRC service"  ${SRCS})

os_add_drivers(LiveUpdate_example ${DRIVERS})
os_add_stdout(LiveUpdate_example ${STDOUT})


add_custom_command( PRE_BUILD
  OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/motd.h
  COMMAND xxd -i < ${CMAKE_CURRENT_SOURCE_DIR}/ircd.motd > ${CMAKE_CURRENT_BINARY_DIR}/motd.h
  DEPENDS ${CMAKE_CURRENT_SOURCE_DIR}/ircd.motd
  WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
)

add_custom_target(motd DEPENDS ${CMAKE_CURRENT_BINARY_DIR}/motd.h)
add_dependencies(LiveUpdate_example motd)

os_link_libraries(LiveUpdate_example ircd)
