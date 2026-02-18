cmake_minimum_required(VERSION 3.30)
project(avoip)

add_library(asio STATIC IMPORTED)
add_library(imgui STATIC IMPORTED)
add_library(sdl STATIC IMPORTED)

add_executable(
  operator
  "src/operator/main.cpp"
)

target_link_libraries(
  operator
  PRIVATE
  asio
  imgui
  sdl
)

if (WIN32)

set_target_properties(
  asio
  PROPERTIES
  IMPORTED_CONFIGURATIONS
  "RELEASE;DEBUG"
  IMPORTED_LOCATION_DEBUG
  "${CMAKE_SOURCE_DIR}/third_party/asio/lib/win32/asio-d.lib"
  IMPORTED_LOCATION_RELEASE
  "${CMAKE_SOURCE_DIR}/third_party/asio/lib/win32/asio.lib"
  INTERFACE_INCLUDE_DIRECTORIES
  "${CMAKE_SOURCE_DIR}/third_party/asio/include"
)

set_target_properties(
  imgui
  PROPERTIES
  IMPORTED_CONFIGURATIONS
  "RELEASE;DEBUG"
  IMPORTED_LOCATION_DEBUG
  "${CMAKE_SOURCE_DIR}/third_party/imgui/lib/win32/imgui-d.lib"
  IMPORTED_LOCATION_RELEASE
  "${CMAKE_SOURCE_DIR}/third_party/imgui/lib/win32/imgui.lib"
  INTERFACE_INCLUDE_DIRECTORIES
  "${CMAKE_SOURCE_DIR}/third_party/imgui/include"
  INTERFACE_LINK_LIBRARIES
  "opengl32"
)

set_target_properties(
  sdl
  PROPERTIES
  IMPORTED_CONFIGURATIONS
  "RELEASE;DEBUG"
  IMPORTED_LOCATION_DEBUG
  "${CMAKE_SOURCE_DIR}/third_party/sdl/lib/win32/sdl-d.lib"
  IMPORTED_LOCATION_RELEASE
  "${CMAKE_SOURCE_DIR}/third_party/sdl/lib/win32/sdl.lib"
  INTERFACE_INCLUDE_DIRECTORIES
  "${CMAKE_SOURCE_DIR}/third_party/sdl/include"
  INTERFACE_LINK_LIBRARIES
  "winmm;setupapi;cfgmgr32;imm32;version"
)

endif ()
