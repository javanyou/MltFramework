
set(TARGET_NAME mlt)

set(MLT_FRAMEWORK_HEADER
  mlt.h
  mlt_cache.h
  mlt_consumer.h
  mlt_deque.h
  mlt_events.h
  mlt_factory.h
  mlt_field.h
  mlt_filter.h
  mlt_frame.h
  mlt_geometry.h
  mlt_log.h
  mlt_multitrack.h
  mlt_pool.h
  mlt_producer.h
  mlt_profile.h
  mlt_properties.h
  mlt_property.h
  mlt_repository.h
  mlt_service.h
  mlt_slices.h
  mlt_tokeniser.h
  mlt_tractor.h
  mlt_transition.h
  mlt_types.h
  mlt_version.h
  )

set(MLT_FRAMEWORK_SRC
  mlt_animation.c
  mlt_cache.c
  mlt_consumer.c
  mlt_deque.c
  mlt_events.c
  mlt_factory.c
  mlt_field.c
  mlt_filter.c
  mlt_frame.c
  mlt_geometry.c
  mlt_log.c
  mlt_multitrack.c
  mlt_parser.c
  mlt_playlist.c
  mlt_pool.c
  mlt_producer.c
  mlt_profile.c
  mlt_properties.c
  mlt_property.c
  mlt_repository.c
  mlt_service.c
  mlt_slices.c
  mlt_tokeniser.c
  mlt_tractor.c
  mlt_transition.c
  mlt_version.c
  )

add_compile_options(-DUSE_SSE -DUSE_SSE2 -O2)

if (!WIN32)
    add_compile_options(-DUSE_MMX)
endif ()

add_library(${TARGET_NAME} SHARED ${MLT_FRAMEWORK_HEADER} ${MLT_FRAMEWORK_SRC})

if(APPLE)
    add_definitions(-DRELOCATABLE)
endif(APPLE)

add_custom_command (TARGET ${TARGET_NAME} POST_BUILD
  COMMAND mkdir -p ${DEST_LIBRARY_DIR} && ln -sf $<TARGET_FILE:${TARGET_NAME}> ${DEST_LIBRARY_DIR}/$<TARGET_FILE_NAME:${TARGET_NAME}>
  WORKING_DIRECTORY ${DEST_LIBRARY_DIR})

install(FILES ${MLT_FRAMEWORK_HEADER} DESTINATION ${DEST_INCLUDE_DIR}/framework)
install(TARGETS mlt DESTINATION  ${DEST_LIBRARY_DIR})
