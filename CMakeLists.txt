cmake_minimum_required(VERSION 3.9)
project(test_project)

add_executable(test_project src/main.cpp)

target_compile_features(test_project
  PRIVATE
    cxx_std_17
  )

include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
conan_basic_setup()

target_link_libraries(test_project ${CONAN_LIBS})

###############################################################################
# Test
###############################################################################

add_executable(test_project_test test/test.cpp)

find_package(Catch2 2.4.2 REQUIRED CONFIG)

target_link_libraries(test_project_test ${CONAN_LIBS}
Catch2::Catch2)
include(CTest)
include(Catch)
catch_discover_tests(test_project_test)
