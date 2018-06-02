aux_source_directory (. SRC_LIST)

message(${SRC_LIST})

# add external libraries
find_package(OpenCV REQUIRED)
# ADD BY Liyao
include_directories(${PROJECT_SOURCE_DIR}/../FaceDetection/include)
include_directories(${PROJECT_SOURCE_DIR}/../FaceAlignment/include)
set(fi_required_libs ${OpenCV_LIBS})
list(APPEND fi_required_libs ${PROJECT_SOURCE_DIR}/../FaceDetection/build/libseeta_facedet_lib.so)
list(APPEND fi_required_libs ${PROJECT_SOURCE_DIR}/../FaceAlignment/build/libseeta_fa_lib.so)
# ENDOFADD

enable_testing ()
foreach (f ${SRC_LIST})
  string(REGEX REPLACE "[.]cpp" ".bin" BIN ${f})
  add_executable(${BIN} ${f})
# CHANGE BY Liyao
  # - target_link_libraries(${BIN} viplnet ${OpenCV_LIBS})
  target_link_libraries(${BIN} viplnet ${fi_required_libs})
# ENDOFCHANGE
endforeach ()

