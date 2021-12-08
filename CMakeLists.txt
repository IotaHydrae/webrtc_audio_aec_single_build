cmake_minimum_required(VERSION 3.10)

# specify the C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)
# The cross toolchain of cmake could
# defines outside in ENV named CXX

# set the project name
project(demo)

# set(CMAKE_C_COMPILER "/usr/bin/aarch64-linux-gnu-gcc")
# set(CMAKE_CXX_COMPILER "/usr/bin/aarch64-linux-gnu-g++")


# set(CMAKE_C_COMPILER "/usr/bin/arm-linux-gnueabihf-gcc")
# set(CMAKE_CXX_COMPILER "/usr/bin/arm-linux-gnueabihf-g++")

file(GLOB ALL_SRCS 
"${PROJECT_SOURCE_DIR}/webrtc/*.c"

"${PROJECT_SOURCE_DIR}/webrtc/common_audio/resampler/*.c"
"${PROJECT_SOURCE_DIR}/webrtc/common_audio/signal_processing/*.c"
"${PROJECT_SOURCE_DIR}/webrtc/common_audio/vad/*.c"

"${PROJECT_SOURCE_DIR}/webrtc/modules/audio_processing/aec/*.c"
"${PROJECT_SOURCE_DIR}/webrtc/modules/audio_processing/aecm/*.c"
"${PROJECT_SOURCE_DIR}/webrtc/modules/audio_processing/agc/*.c"
"${PROJECT_SOURCE_DIR}/webrtc/modules/audio_processing/ns/*.c"
"${PROJECT_SOURCE_DIR}/webrtc/modules/audio_processing/utility/*.c"
"${PROJECT_SOURCE_DIR}/webrtc/system_wrappers/source/cpu_features.cpp"
)
# add the library
add_library(webrtc_audio_preprocessing SHARED ${ALL_SRCS})

# add the executable
# add_library(webrtc_aec SHARED ${AEC_SRCS})
# add_library(webrtc_aecm SHARED ${AECM_SRCS})
# add_library(webrtc_utility SHARED ${UTIL_SRCS})
# add_library(webrtc_common_sig_proc SHARED ${COMMON_SIG_PROC_SRCS})
# list(APPEND EXTRA_LIBS webrtc_aec webrtc_utility webrtc_aecm webrtc_common_sig_proc)
list(APPEND EXTRA_LIBS webrtc_audio_preprocessing)
# list(APPEND EXTRA_LIBS "${PROJECT_SOURCE_DIR}/build/libwebrtc_audio_preprocessing.so")
add_executable(demo WebRtcAudioTest.cpp)


# add include files
include_directories(
    "${PROJECT_SOURCE_DIR}"
    "${PROJECT_SOURCE_DIR}/webrtc"
    "${PROJECT_SOURCE_DIR}/webrtc/common_audio/include"
    "${PROJECT_SOURCE_DIR}/webrtc/common_audio/resampler/include"
    "${PROJECT_SOURCE_DIR}/webrtc/common_audio/vad/include"
    "${PROJECT_SOURCE_DIR}/webrtc/common_audio/signal_processing/include/"
    "${PROJECT_SOURCE_DIR}/webrtc/modules/audio_processing/aec/include/"
    "${PROJECT_SOURCE_DIR}/webrtc/modules/audio_processing/aecm/include/"
    "${PROJECT_SOURCE_DIR}/webrtc/modules/audio_processing/agc/include/"
    "${PROJECT_SOURCE_DIR}/webrtc/modules/audio_processing/ns/include/"
    "${PROJECT_SOURCE_DIR}/webrtc/modules/audio_processing/utility/"
    "${PROJECT_SOURCE_DIR}/webrtc/system_wrappers/interface/"
    "${PROJECT_SOURCE_DIR}/webrtc/system_wrappers"
)
    
    
target_link_libraries(demo PUBLIC ${EXTRA_LIBS} pthread)
