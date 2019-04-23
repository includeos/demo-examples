cmake_minimum_required(VERSION 3.8.0)

set(CMAKE_TRY_COMPILE_TARGET_TYPE STATIC_LIBRARY)

project (http_client C CXX)

include(${CMAKE_CURRENT_BINARY_DIR}/conanbuildinfo.cmake OPTIONAL RESULT_VARIABLE HAS_CONAN)
if (NOT HAS_CONAN)
  message(FATAL_ERROR "missing conanbuildinfo.cmake did you forget to run conan install ?")
endif()
conan_basic_setup()

include(os)

os_add_executable(http_client "http_client" service.cpp)
os_add_drivers(http_client virtionet vmxnet3 e1000 boot_logger timestamps)
os_add_plugins(http_client autoconf)
os_add_stdout(http_client default_stdout)
os_add_ssl_certificates(http_client)
