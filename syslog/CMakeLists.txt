cmake_minimum_required(VERSION 3.0)

# Service
project (syslogd)

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

os_add_executable(syslog_service "Syslog plugin example" ${SOURCES})

os_add_drivers(syslog_service
  virtionet
)

os_add_stdout(syslog_service default_stdout)
os_add_plugins(syslog_service syslogd)
