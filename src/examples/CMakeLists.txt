
set( TARGET_NAME play )

include_directories(${CMAKE_SOURCE_DIR}/src/mlt++)

add_executable( ${TARGET_NAME} play.cpp)

target_link_libraries( ${TARGET_NAME} mlt++ )
target_include_directories( ${TARGET_NAME} PRIVATE
  ${CMAKE_SOURCE_DIR}/src
  )

target_compile_definitions ( ${TARGET_NAME} PRIVATE
  MODULEDIR="${DEST_LIBRARY_DIR}"
  )

set_target_properties( ${TARGET_NAME}
  PROPERTIES
  ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib"
  LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib"
  RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}"
  )