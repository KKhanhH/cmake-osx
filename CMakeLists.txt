cmake_minimum_required(VERSION 3.25)
project("cmake_project_test")
set(CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/modules) 

add_executable(executable_program main.cpp)

find_package(Libatrac9 MODULE REQUIRED) 

target_link_libraries(test 
  ${LIBATRAC9_LIBRARY} 
)

if(WIN32)
  install(TARGETS executable_program RUNTIME DESTINATION .)
  x_vcpkg_install_local_dependencies(TARGETS executable_program DESTINATION .)
else()
  install(TARGETS executable_program RUNTIME_DEPENDENCIES
    RUNTIME DESTINATION .
    FRAMEWORK DESTINATION ./lib
    LIBRARY DESTINATION .
  )
endif()
