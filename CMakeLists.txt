cmake_minimum_required(VERSION 3.7 FATAL_ERROR)
project(xmoto C CXX)

list(APPEND CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/CMake")

include(CheckCXXCompilerFlag)
include(CheckPrototypeDefinition)
include(CheckSymbolExists)

# packaging
#include(cpack/cpack.cmake)

add_subdirectory(src)

add_subdirectory(bin)
add_subdirectory(extra)
#add_subdirectory(po)

set(CPACK_PACKAGE_NAME "xmoto")
set(CPACK_PACKAGE_VERSION "0.5.12")
#set(CPACK_PACKAGE_VENDOR "")
#set(CPACK_PACKAGE_DESCRIPTION_SUMMARY "")
#set(CPACK_PACKAGE_DESCRIPTION_FILE "${PROJECT_SOURCE_DIR}/README.md")
set(CPACK_RESOURCE_FILE_LICENSE "${PROJECT_SOURCE_DIR}/COPYING")
set(CPACK_RESOURCE_FILE_README "${PROJECT_SOURCE_DIR}/README.md")
set(CPACK_SOURCE_IGNORE_FILES "/\\\\.git/")
if(CMAKE_SYSTEM_NAME STREQUAL "Windows")
    set(CPACK_INCLUDE_TOPLEVEL_DIRECTORY FALSE)
    set(CPACK_GENERATOR "ZIP;NSIS")
endif()
include(CPack)

if(CMAKE_SYSTEM_NAME STREQUAL "Windows")
  install(
    FILES
      "${PROJECT_SOURCE_DIR}/README.md"
      "${PROJECT_SOURCE_DIR}/COPYING"
      "${PROJECT_SOURCE_DIR}/ChangeLog"
    DESTINATION "."
  )
  install(DIRECTORY "${PROJECT_SOURCE_DIR}/mingw_lib/"
      DESTINATION "."
      FILES_MATCHING PATTERN "*.dll"
  )
endif()

