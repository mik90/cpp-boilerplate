cmake_minimum_required(VERSION 3.15)

# Based off of https://github.com/lefticus/cpp_starter_project
project(cpp-boilerplate CXX)
include(cmake/StandardProjectSettings.cmake)
include(cmake/StaticAnalyzers.cmake)
list(APPEND CMAKE_MODULE_PATH ${CMAKE_BINARY_DIR})
list(APPEND CMAKE_PREFIX_PATH ${CMAKE_BINARY_DIR})

add_library(project_options INTERFACE)
target_compile_features(project_options INTERFACE cxx_std_17)
set(CMAKE_CXX_EXTENSIONS OFF)

add_library(project_warnings INTERFACE)
include(cmake/CompilerWarnings.cmake)
set_project_warnings(project_warnings)

option(ENABLE_TESTING "Enable Test Builds" ON)

set(CONAN_EXTRA_REQUIRES "")
set(CONAN_EXTRA_OPTIONS "")

if(ENABLE_TESTING)
  list(APPEND CONAN_EXTRA_REQUIRES gtest/1.11.0)
endif()
include(cmake/RunConan.cmake)

add_subdirectory(src)

if(ENABLE_TESTING)
  find_package(GTest REQUIRED)
  enable_testing()
  message("Configuring tests...")
  add_subdirectory(test)
endif()
