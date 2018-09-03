cmake_minimum_required(VERSION 3.12)

project(MltFramework)

set(CMAKE_CXX_STANDARD 14)

set (DEST_INCLUDE_DIR ${PROJECT_BINARY_DIR}/include/mlt)
set (DEST_LIBRARY_DIR ${PROJECT_BINARY_DIR}/lib/mlt)

file( MAKE_DIRECTORY ${DEST_INCLUDE_DIR})
file( MAKE_DIRECTORY ${DEST_LIBRARY_DIR})

add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/src/framework)

# modules
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/src/modules)

# Build C++ version
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/src/mlt++)

# Examples
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/src/examples)