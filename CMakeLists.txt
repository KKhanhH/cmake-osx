cmake_minimum_required(VERSION 3.25)
project("test")
add_executable(test main.cpp)

find_package(SDL2 REQUIRED)
find_package(glm REQUIRED)
find_package(OpenAL REQUIRED)
find_package(ZLIB REQUIRED)
find_package(OggVorbis REQUIRED)
find_package(WebP REQUIRED)
find_package(avcpp CONFIG REQUIRED)
find_package(Vulkan REQUIRED)

target_link_libraries(test 
  SDL2::SDL2
  SDL2::SDL2main
  ${OPENAL_LIBRARY}
  ${SDL2_LIBRARIES}
  ZLIB::ZLIB
  ogg::ogg
  Vorbis::Vorbis
  vorbis::vorbisfile
  ${WebP_LIBRARIES}
  avcpp::avcpp
  avcpp::FFmpeg
  ${Vulkan_LIBRARIES}
)

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
