
set(TARGET_NAME mltavformat)

find_path( AVCODEC_INCLUDE_DIR libavcodec/avcodec.h )
find_library( AVCODEC_LIBRARY avcodec )

find_path( AVFORMAT_INCLUDE_DIR libavformat/avformat.h )
find_library( AVFORMAT_LIBRARY avformat)

find_path( AVUTIL_INCLUDE_DIR libavutil/avutil.h )
find_library( AVUTIL_LIBRARY avutil)

find_path( SWRESAMPLE_INCLUDE_DIR libswresample/swresample.h)
find_library( SWRESAMPLE_LIBRARY swresample)

find_path( SWSCALE_INCLUDE_DIR libswscale/swscale.h)
find_library( SWSCALE_LIBRARY swscale)

find_path( AVFILTER_INCLUDE_DIR libavfilter/avfilter.h )
find_library( AVFILTER_LIBRARY avfilter)

set(MLT_AVFORMAT_SRC
  common.c
  consumer_avformat.c
  factory.c
  filter_avcolour_space.c
  filter_avdeinterlace.c
  filter_avfilter.c
  filter_swresample.c
  filter_swscale.c
  producer_avformat.c
  )

add_library( ${TARGET_NAME} SHARED ${MLT_AVFORMAT_SRC} )

target_link_libraries( ${TARGET_NAME} PRIVATE
  ${AVCODEC_LIBRARY}
  ${AVFORMAT_LIBRARY}
  ${AVUTIL_LIBRARY}
  ${AVFILTER_LIBRARY}
  ${SWRESAMPLE_LIBRARY}
  ${SWSCALE_LIBRARY}
  mlt
  )

target_include_directories( ${TARGET_NAME} PRIVATE
  ${AVCODEC_INCLUDE_DIR}
  ${AVFORMAT_INCLUDE_DIR}
  ${AVUTIL_INCLUDE_DIR}
  ${AVFILTER_INCLUDE_DIR}
  ${CMAKE_SOURCE_DIR}/src
)

target_compile_definitions( ${TARGET_NAME} PRIVATE -DCODECS -DFILTERS -DAVFILTER -DSWRESAMPLE -DDEVICE)

add_custom_command (TARGET ${TARGET_NAME} POST_BUILD
  COMMAND mkdir -p ${DEST_LIBRARY_DIR} && ln -sf $<TARGET_FILE:${TARGET_NAME}> ${DEST_LIBRARY_DIR}/$<TARGET_FILE_NAME:${TARGET_NAME}>
  WORKING_DIRECTORY ${DEST_LIBRARY_DIR})