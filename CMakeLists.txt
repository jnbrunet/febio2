cmake_minimum_required(VERSION 3.1)
project(FEBio2)

## Default build type
if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE "RelWithDebInfo")
endif()

# CMAKE TOOLS
list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_LIST_DIR}/CMake")

# COMPILER FLAGS
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++14")

if ("${CMAKE_CXX_COMPILER} ${CMAKE_CXX_COMPILER_ARG1}" MATCHES ".*[cC][lL][aA][nN][gG]")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fcolor-diagnostics")
else()
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fdiagnostics-color")
endif()

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

add_subdirectory(FECore)
add_subdirectory(NumCore)
add_subdirectory(FEBioLib)
add_subdirectory(FEBioXML)
add_subdirectory(FEBioMech)
add_subdirectory(FEBioPlot)
add_subdirectory(FEBioOpt)
add_subdirectory(FEBioMix)
add_subdirectory(FEBioHeat)
add_subdirectory(FEBioFluid)
add_subdirectory(FEBio2)