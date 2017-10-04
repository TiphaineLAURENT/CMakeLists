cmake_minimum_required(VERSION 3.5.1)

#Configuration du projet
project(TestHello)
set(EXECUTABLE_OUTPUT_PATH bin/${CMAKE_BUILD_TYPE})

#Inclusion de la bibliothèque Hello
message(AUTHOR_WARNING ${CMAKE_SOURCE_DIR}/../include/libhello)
include_directories(${CMAKE_SOURCE_DIR}/../include/libhello)
link_directories(${CMAKE_SOURCE_DIR}/../lib/${CMAKE_BUILD_TYPE})

#Configuration de l'exécutable
file(
  GLOB_RECURSE
  source_files
  src/*
  )

add_executable(
  test_hello
  ${source_files}
  )

#Configuration de l'édition de liens
target_link_libraries(
  test_hello
  hello
  )

enable_testing()
add_test(
  NAME Testing
  COMMAND ./bin/test_hello
  )
