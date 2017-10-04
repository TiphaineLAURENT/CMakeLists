cmake_minimum_required(VERSION 2.6) # CMAKE version required to run cmake

#Configuration du projet
project(Hello) # Name of library
set(LIBRARY_OUTPUT_PATH ${CMAKE_SOURCE_DIR}/lib/${CMAKE_BUILD_TYPE}) # Set library output path

#Inclusion des en-têtes publics
include_directories(${CMAKE_SOURCE_DIR}/include/libhello) # Headers folder

#Configuration de la bibliothèque
file(
  GLOB_RECURSE # Search recursively files
  source_files # Store files in "source_files" variable
  src/* # Search in src folder
  include/* # Search in include folder
  )

add_library(
  hello_shared # Create a library named "hello_shared"
  SHARED # Make a shared library (.so)
  ${source_files} # From "source_files"
  )

add_library(
  hello_static # Create a library named "hello_static"
  STATIC # Make a static library (.a)
  ${source_files} # From "source_files"
  )

#add_subdirectory(test) # Add a folder containing an other CMakeLists.txt
#add_custom_command(
#  OUTPUT ${CMAKE_SOURCE_DIR}/test/bin/test_hello # Create a output file
#  COMMAND make -C test # Command to create the output file
#  COMMENT Generating test binary # Comment to write before executing command
#  )

enable_testing() # Enable testing
add_test(
  NAME Testing # Name of the test
  COMMAND make -C test test # Command to test
  )
#add_test(NAME Testing
#  WORKING_DIRECTORY test
#  COMMAND ./bin/test_hello
#  )
