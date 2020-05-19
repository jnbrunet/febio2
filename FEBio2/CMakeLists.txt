cmake_minimum_required(VERSION 3.1)
project(FEBio2)

file(GLOB SOURCE_FILES ${PROJECT_SOURCE_DIR}/*.cpp)
file(GLOB HEADER_FILES ${PROJECT_SOURCE_DIR}/*.h)

find_package( OpenMP REQUIRED)

add_executable(${PROJECT_NAME} ${SOURCE_FILES} ${HEADER_FILES})

target_include_directories(${PROJECT_NAME} PUBLIC "$<BUILD_INTERFACE:${CMAKE_SOURCE_DIR}/>")
target_include_directories(${PROJECT_NAME} PUBLIC "$<INSTALL_INTERFACE:include>")

target_link_libraries(${PROJECT_NAME} PUBLIC -Wl,--start-group FECore FEBioLib FEBioPlot FEBioMech FEBioMix FEBioXML NumCore FEBioOpt -Wl,--end-group OpenMP::OpenMP_CXX dl)

if (LINUX)
    target_compile_definitions(${PROJECT_NAME} PRIVATE LINUX)
endif ()

configure_file(${CMAKE_SOURCE_DIR}/build/bin/febio.xml ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/febio.xml COPYONLY)
