cmake_minimum_required(VERSION 3.25)
project("test")
add_executable(test main.cpp)

find_package(SDL2)
target_link_libraries(test SDL2::SDL2 SDL2::SDL2main) 
if(WIN32)
  install(TARGETS test RUNTIME DESTINATION .)
  x_vcpkg_install_local_dependencies(TARGETS test DESTINATION .)
  else()
  install(TARGETS test RUNTIME_DEPENDENCIES DIRECTORIES ${VCPKG_INSTALLED_DIR}
    RUNTIME DESTINATION .
    FRAMEWORK DESTINATION ./lib
    LIBRARY DESTINATION .
  )
endif()