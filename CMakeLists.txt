cmake_minimum_required(VERSION 3.10)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

project(SealPIR VERSION 2.1 LANGUAGES CXX)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)

option(VERBOSE "Trace protocol internal values" ON)
option(DEBUG "Print debug information" OFF)
if(VERBOSE)
    add_definitions(-DVERBOSE)
endif()
if(DEBUG)
    add_definitions(-DDEBUG)
endif()

add_executable(main
	main.cpp
)

add_library(sealpir STATIC
  pir.cpp
  pir_client.cpp
  pir_server.cpp
)

find_package(SEAL 3.2.0 EXACT REQUIRED)

target_link_libraries(main sealpir SEAL::seal)
