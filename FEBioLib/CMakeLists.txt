cmake_minimum_required(VERSION 3.10)
project(FEBio2)

add_definitions(${DEF})

include_directories(${INC})

file(GLOB SOURCES "*.cpp")

add_library(febiolib ${SOURCES})
