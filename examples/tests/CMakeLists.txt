set(EXAMPLE_FILES
    handFromJsonTest.cpp)

foreach(EXAMPLE_FILE ${EXAMPLE_FILES})

  get_filename_component(SOURCE_NAME ${EXAMPLE_FILE} NAME_WE)
  
  if (UNIX AND NOT APPLE)
    set(EXE_NAME "${SOURCE_NAME}.bin")
  elseif (WIN32)
    set(EXE_NAME "${SOURCE_NAME}")
  endif ()

  message(STATUS "Adding Example ${EXE_NAME}")
  add_executable(${EXE_NAME} ${EXAMPLE_FILE})
  target_link_libraries( ${EXE_NAME} openpose ${GLOG_LIBRARY} ${GFLAGS_LIBRARY} ${Caffe_LIBS})
  
  if (WIN32)
    set_property(TARGET ${EXE_NAME} PROPERTY FOLDER "Examples/Tutorial/Tests")
    configure_file(${CMAKE_SOURCE_DIR}/cmake/OpenPose.vcxproj.user 
        ${CMAKE_CURRENT_BINARY_DIR}/${EXE_NAME}.vcxproj.user @ONLY) 
  endif (WIN32)

endforeach()
