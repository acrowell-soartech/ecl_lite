##############################################################################
# Cmake
##############################################################################

cmake_minimum_required(VERSION 3.5)
project(ecl_converters_lite)

##############################################################################
# Find Packages
##############################################################################

find_package(ament_cmake_ros REQUIRED)
find_package(ecl_build REQUIRED)
find_package(ecl_config REQUIRED)

##############################################################################
# Project Configuration
##############################################################################

ecl_enable_cxx14_compiler()

##############################################################################
# Header Library
##############################################################################

add_library(${PROJECT_NAME} INTERFACE)
target_include_directories(
  ${PROJECT_NAME}
  INTERFACE
    $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
)
target_link_libraries(${PROJECT_NAME} INTERFACE ecl_config::ecl_config)

install(TARGETS ${PROJECT_NAME} EXPORT ${PROJECT_NAME}
   RUNTIME DESTINATION bin
   ARCHIVE DESTINATION lib
   LIBRARY DESTINATION lib
   INCLUDES DESTINATION include
)

##############################################################################
# Sources
##############################################################################

add_subdirectory(include)
add_subdirectory(src)

##############################################################################
# Exports
##############################################################################

ament_export_interfaces(${PROJECT_NAME})
ament_export_dependencies(ecl_config)
ament_package()
