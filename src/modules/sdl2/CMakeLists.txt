
set( TARGET_NAME mltsdl2 )

FIND_PACKAGE(SDL2 REQUIRED)

set(MLT_SDL2_SRC
  common.c
  consumer_sdl2.c
  consumer_sdl2_audio.c
  factory.c
  )

add_library( ${TARGET_NAME} SHARED ${MLT_SDL2_SRC})

target_link_libraries( ${TARGET_NAME} PRIVATE
  ${SDL2_LIBRARIES}
  mlt
)

target_include_directories( ${TARGET_NAME} PRIVATE
  ${SDL2_INCLUDE_DIRS}
  ${CMAKE_SOURCE_DIR}/src
)

add_compile_options(-D_USE_MATH_DEFINES)

add_custom_command (TARGET ${TARGET_NAME} POST_BUILD
  COMMAND mkdir -p ${DEST_LIBRARY_DIR} && ln -sf $<TARGET_FILE:${TARGET_NAME}> ${DEST_LIBRARY_DIR}/$<TARGET_FILE_NAME:${TARGET_NAME}>
  WORKING_DIRECTORY ${DEST_LIBRARY_DIR})