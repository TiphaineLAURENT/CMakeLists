cmake_minimum_required(VERSION 2.6) # CMAKE version required to run cmake
set(CMAKE_VERBOSE_MAKEFILE ON) # Display makefile command in console
cmake_policy(SET CMP0048 NEW) # Enable VERSION variable in project

#Configuration du projet
project(
  TestHello # Name of project
  VERSION 1.0.0.0 # <major><minor><patch><tweak>
  )
set(EXECUTABLE_OUTPUT_PATH bin/${CMAKE_BUILD_TYPE}) # Output path
add_compile_options(-W -Wall -Wextra -Werror -Wshadow) # Compiler option

#Inclusion de la bibliothèque Hello
message(AUTHOR_WARNING ${CMAKE_SOURCE_DIR}/../include/libhello) # Comment
include_directories(${CMAKE_SOURCE_DIR}/../include/libhello) # Headers folder
link_directories(${CMAKE_SOURCE_DIR}/../lib/${CMAKE_BUILD_TYPE}) # Libs folder

#Configuration de l'exécutable

file(
  GLOB_RECURSE # Get files recursively
  source_files # Store them in "source_files" variable
  src/* # Search in src folder
  )

add_executable(
  test_hello # Create "test_hello" executable
  ${source_files} # From "source_files"
  )

#Configuration de l'édition de liens
target_link_libraries(
  test_hello # Link "test_hello" executable with library
  hello_shared # Name of the library
  )

enable_testing() # Enable testing
add_test(
  NAME Testing # Name of the test
  COMMAND ./bin/test_hello # Command to test
  )
