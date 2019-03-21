cmake_minimum_required(VERSION 3.0)

#Avoid cmake from test compiling to host
set(CMAKE_TRY_COMPILE_TARGET_TYPE STATIC_LIBRARY)


project(protobuf_test_service C CXX)
#check if conan is already run outside of project
if (NOT DEFINED CONAN_DEPENDENCIES)
  include(${CMAKE_CURRENT_BINARY_DIR}/conanbuildinfo.cmake OPTIONAL RESULT_VARIABLE HAS_CONAN)
  if (NOT HAS_CONAN)
    message(FATAL_ERROR "missing conanbuildinfo.cmake did you forget to run conan install ?")
  endif()
endif()
conan_basic_setup()

find_package(Protobuf REQUIRED)
protobuf_generate_cpp(PROTO_SRCS PROTO_HDRS person.proto)

include(os)
include_directories(${CMAKE_CURRENT_BINARY_DIR})
os_add_executable(protobuf_test_service "Google's protobuf runtime library test" service.cpp ${PROTO_SRCS} ${PROTO_HDRS})
os_add_stdout(protobuf_test_service default_stdout)
