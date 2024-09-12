cmake_minimum_required(VERSION 3.27)
project(vlcQt VERSION 1.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_library(kd-reports INTERFACE)

target_include_directories(kd-reports
  INTERFACE
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
  $<INSTALL_INTERFACE:include/kd-reports>
)

target_link_directories(kd-reports
  INTERFACE
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/lib>
  $<INSTALL_INTERFACE:lib/kd-reports>
)

target_link_libraries(kd-reports
  INTERFACE
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/lib/kdreports2.lib>
  $<INSTALL_INTERFACE:kdreports2.lib>
)

include(CMakePackageConfigHelpers)
configure_package_config_file(
  "${CMAKE_CURRENT_SOURCE_DIR}/kd-reportsConfig.cmake.in"
  "${CMAKE_CURRENT_BINARY_DIR}/kd-reportsConfig.cmake"
  INSTALL_DESTINATION share/kd-reports
)

install(TARGETS kd-reports
  EXPORT kd-reportsTargets
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
  RUNTIME DESTINATION bin
)

install(DIRECTORY
  "${CMAKE_CURRENT_SOURCE_DIR}/include/KDReports"
  DESTINATION include/kd-reports
)

install(FILES
  "${CMAKE_CURRENT_SOURCE_DIR}/lib/kdreports2.lib"
  DESTINATION lib/kd-reports
)

install(DIRECTORY
  "${CMAKE_CURRENT_SOURCE_DIR}/bin"
  DESTINATION /
)

install(
  EXPORT kd-reportsTargets
  DESTINATION share/kd-reports
  NAMESPACE kd-reports::
)

install(
  FILES
  "${CMAKE_CURRENT_BINARY_DIR}/kd-reportsConfig.cmake"
  DESTINATION share/kd-reports
)