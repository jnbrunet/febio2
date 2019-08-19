cmake_minimum_required(VERSION 3.1)
project(FEBio2)

file(GLOB SOURCE_FILES ${PROJECT_SOURCE_DIR}/*.cpp)
file(GLOB HEADER_FILES ${PROJECT_SOURCE_DIR}/*.h)

#find_package( OpenMP REQUIRED)

add_executable(${PROJECT_NAME} ${SOURCE_FILES} ${HEADER_FILES})

target_include_directories(${PROJECT_NAME} PUBLIC "$<BUILD_INTERFACE:${CMAKE_SOURCE_DIR}/>")
target_include_directories(${PROJECT_NAME} PUBLIC "$<INSTALL_INTERFACE:include>")
target_include_directories(${PROJECT_NAME} PUBLIC "/usr/local/opt/libomp/include")

target_link_libraries(${PROJECT_NAME} PUBLIC FECore FEBioMech FEBioMix FEBioOpt FEBioPlot FEBioXML NumCore FEBioLib /usr/local/opt/libomp/lib/libomp.dylib)

configure_file(${CMAKE_SOURCE_DIR}/build/bin/febio.xml ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/febio.xml COPYONLY)
