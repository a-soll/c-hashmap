cmake_minimum_required(VERSION 3.0)
set(CMAKE_C_COMPILER ${CMAKE_C_COMPILER})
set(CMAKE_CXX_COMPILER ${CMAKE_CXX_COMPILER})

project(c-hashmap VERSION 1.0)
include(GNUInstallDirs)

add_library(c-hashmap SHARED bucket.c)
add_library(c-hashmap-static STATIC bucket.c)

configure_file(c-hashmap.pc.in c-hashmap.pc @ONLY)

set_target_properties(c-hashmap PROPERTIES VERSION ${PROJECT_VERSION})
set_target_properties(c-hashmap PROPERTIES PUBLIC_HEADER bucket.h)
set_target_properties(c-hashmap-static PROPERTIES OUTPUT_NAME ${PROJECT_NAME})

install(TARGETS c-hashmap PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR} LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR})
