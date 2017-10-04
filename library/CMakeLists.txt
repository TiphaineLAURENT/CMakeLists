cmake_minimum_required(VERSION 2.6)

#Configuration du projet
project(Hello)
set(LIBRARY_OUTPUT_PATH ${CMAKE_SOURCE_DIR}/lib/${CMAKE_BUILD_TYPE})

#Inclusion des en-têtes publics
include_directories(${CMAKE_SOURCE_DIR}/include/libhello)

#Configuration de la bibliothèque
file(
  GLOB_RECURSE
  source_files
  src/*
  include/*
  )

add_library(
  hello_shared
  SHARED
  ${source_files}
  )

add_library(
  hello_static
  STATIC
  ${source_files}
  )

#add_subdirectory(test)
#add_custom_command(OUTPUT ${CMAKE_SOURCE_DIR}/test/bin/test_hello
#  COMMAND make -C test
#  COMMENT Generating test binary
#  )

enable_testing()
add_test(NAME Testing
  COMMAND make -C test test
  )
#add_test(NAME Testing
#  WORKING_DIRECTORY test
#  COMMAND ./bin/test_hello
#  )
