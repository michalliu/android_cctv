cmake_minimum_required(VERSION 3.12)

message("CMAKE VERSION: ${CMAKE_VERSION}")

set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/../jniLibs/${ANDROID_ABI})

#include_directories(${PROJECT_SOURCE_DIR}/x264/include)
#find_library(X264 x264 "${PROJECT_SOURCE_DIR}/x264")

file(GLOB MEDIA_ENCODER "*.cpp")
file(GLOB G72X "g72x/*.c")

add_library(X264 STATIC IMPORTED)
set_property(TARGET X264 PROPERTY IMPORTED_LOCATION ${PROJECT_SOURCE_DIR}/x264/${ANDROID_ABI}/libx264.a)

add_library(MediaEncoder SHARED ${MEDIA_ENCODER} ${G72X})
target_link_libraries(MediaEncoder X264)
