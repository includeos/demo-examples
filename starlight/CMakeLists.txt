cmake_minimum_required(VERSION 3.0)

#service
project (service)

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

os_add_executable(starlight "Starlight Mode 13h" ${SOURCES})
