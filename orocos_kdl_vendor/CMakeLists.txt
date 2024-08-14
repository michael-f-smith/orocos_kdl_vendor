cmake_minimum_required(VERSION 3.10)
project(orocos_kdl_vendor)

find_package(ament_cmake REQUIRED)
find_package(ament_cmake_vendor_package REQUIRED)

# Set minimum version to find matching what would be built because PyKDL vendor will require it
find_package(orocos_kdl 1.5.1 QUIET)

ament_vendor(orocos_kdl_vendor
  SATISFIED ${orocos_kdl_FOUND}
  VCS_URL https://github.com/orocos/orocos_kinematics_dynamics.git
  VCS_VERSION db25b7e480e068df068232064f2443b8d52a83c7
  SOURCE_SUBDIR orocos_kdl
  GLOBAL_HOOK
  CMAKE_ARGS
    -DENABLE_TESTS:BOOL=OFF
    -DENABLE_EXAMPLES:BOOL=OFF
  PATCHES patches
)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package(CONFIG_EXTRAS_POST "orocos_kdl_vendor-extras.cmake")
