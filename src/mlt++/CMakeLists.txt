
set( TARGET_NAME mlt++ )

set( MLT_MLTPP_INCLUDE_FILES
  Mlt.h
  MltAnimation.h
  MltConsumer.h
  MltDeque.h
  MltEvent.h
  MltFactory.h
  MltField.h
  MltFilter.h
  MltFilteredConsumer.h
  MltFilteredProducer.h
  MltFrame.h
  MltGeometry.h
  MltMultitrack.h
  MltParser.h
  MltPlaylist.h
  MltProducer.h
  MltProfile.h
  MltProperties.h
  MltPushConsumer.h
  MltRepository.h
  MltService.h
  MltTokeniser.h
  MltTractor.h
  MltTransition.h
  )

set( MLT_MLTPP_SOURCE_FILES
  MltAnimation.cpp
  MltConsumer.cpp
  MltDeque.cpp
  MltEvent.cpp
  MltFactory.cpp
  MltField.cpp
  MltFilter.cpp
  MltFilteredConsumer.cpp
  MltFilteredProducer.cpp
  MltFrame.cpp
  MltGeometry.cpp
  MltMultitrack.cpp
  MltParser.cpp
  MltPlaylist.cpp
  MltProducer.cpp
  MltProfile.cpp
  MltProperties.cpp
  MltPushConsumer.cpp
  MltRepository.cpp
  MltService.cpp
  MltTokeniser.cpp
  MltTractor.cpp
  MltTransition.cpp
  )

add_compile_options(-D_USE_MATH_DEFINES)

add_library( ${TARGET_NAME} SHARED ${MLT_MLTPP_INCLUDE_FILES} ${MLT_MLTPP_SOURCE_FILES} )

target_link_libraries( ${TARGET_NAME} mlt mltcore )

target_include_directories( ${TARGET_NAME} PRIVATE
  ${CMAKE_SOURCE_DIR}/src
  )

add_custom_command (TARGET ${TARGET_NAME} POST_BUILD
  COMMAND mkdir -p ${DEST_LIBRARY_DIR} && ln -sf $<TARGET_FILE:${TARGET_NAME}> ${DEST_LIBRARY_DIR}/$<TARGET_FILE_NAME:${TARGET_NAME}>
  WORKING_DIRECTORY ${DEST_LIBRARY_DIR})