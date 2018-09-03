
set( TARGET_NAME mltcore)

set( MLT_CORE_INCLUDE_FILES
  )

set( MLT_CORE_SOURCE_FILES
  consumer_multi.c
  consumer_null.c
  factory.c
  filter_audiochannels.c
  filter_audioconvert.c
  filter_audiomap.c
  filter_audiowave.c
  filter_brightness.c
  filter_channelcopy.c
  filter_crop.c
  filter_data_feed.c
  filter_data_show.c
  filter_fieldorder.c
  filter_gamma.c
  filter_greyscale.c
  filter_imageconvert.c
  filter_luma.c
  filter_mirror.c
  filter_mono.c
  filter_obscure.c
  filter_panner.c
  filter_region.c
  filter_rescale.c
  filter_resize.c
  filter_transition.c
  filter_watermark.c
  producer_colour.c
  producer_consumer.c
  producer_hold.c
  producer_loader.c
  producer_melt.c
  producer_noise.c
  producer_timewarp.c
  producer_tone.c
  transition_composite.c
  transition_luma.c
  transition_matte.c
  transition_mix.c
  transition_region.c
  )

file(GLOB SHARE_FILES ${CMAKE_CURRENT_SOURCE_DIR}/*.yml
  ${CMAKE_CURRENT_SOURCE_DIR}/data_fx.properties
  ${CMAKE_CURRENT_SOURCE_DIR}/loader.dict
  ${CMAKE_CURRENT_SOURCE_DIR}/loader.ini)

source_group(share FILES ${SHARE_FILES})

add_library( ${TARGET_NAME} SHARED ${MLT_CORE_SOURCE_FILES} ${MLT_CORE_INCLUDE_FILES} ${SHARE_FILES})

add_dependencies( ${TARGET_NAME} mlt)
target_link_libraries( ${TARGET_NAME} mlt )

target_include_directories( ${TARGET_NAME} PRIVATE
  ${CMAKE_SOURCE_DIR}/src
)

add_custom_command (TARGET ${TARGET_NAME} POST_BUILD
  COMMAND mkdir -p ${DEST_LIBRARY_DIR} && ln -sf $<TARGET_FILE:${TARGET_NAME}> ${DEST_LIBRARY_DIR}/$<TARGET_FILE_NAME:${TARGET_NAME}>
  WORKING_DIRECTORY ${DEST_LIBRARY_DIR})