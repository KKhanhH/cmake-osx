cmake_minimum_required(VERSION 3.25)
project("osx_project_test")
set(CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/modules) 

add_executable(test main.cpp)

find_package(Libatrac9 MODULE REQUIRED) 

target_link_libraries(test 
  ${LIBATRAC9_LIBRARY} 
)

if(WIN32)
  install(TARGETS osx_project_test RUNTIME DESTINATION .)
  x_vcpkg_install_local_dependencies(TARGETS osx_project_test DESTINATION .)
else()
  install(TARGETS osx_project_test RUNTIME_DEPENDENCIES
    RUNTIME DESTINATION .
    FRAMEWORK DESTINATION ./lib
    LIBRARY DESTINATION .
  )
endif()
