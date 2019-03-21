cmake_minimum_required(VERSION 3.0)

option(REAL_HW "Run on real hardware" OFF)
option(LIVEUPDATE "Enable liveupdate" OFF)

#Avoid cmake from test compiling to host
set(CMAKE_TRY_COMPILE_TARGET_TYPE STATIC_LIBRARY)

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

add_custom_command(
  OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/motd.h
  COMMAND xxd -i < ${CMAKE_CURRENT_SOURCE_DIR}/ircd.motd > ${CMAKE_CURRENT_BINARY_DIR}/motd.h
  DEPENDS ${CMAKE_CURRENT_SOURCE_DIR}/ircd.motd
  WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
)

os_add_executable(LiveUpdate_example "IRC service"  ${SRCS} ${CMAKE_CURRENT_BINARY_DIR}/motd.h)

os_add_drivers(LiveUpdate_example ${DRIVERS})
os_add_stdout(LiveUpdate_example ${STDOUT})

os_link_libraries(LiveUpdate_example ircd)
