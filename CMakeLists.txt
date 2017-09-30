cmake_minimum_required(VERSION 3.0.2)
project(dsp)

if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE "Release" CACHE STRING "Choose the type of build, options are: Debug Release." FORCE)
endif(NOT CMAKE_BUILD_TYPE)

if(CMAKE_BUILD_TYPE STREQUAL "Debug")
    set(CMAKE_VERBOSE_MAKEFILE ON)
endif()

set(GENERAL_WARNING_FLAGS           "-Wall")
set(GENERAL_DEBUG_FLAGS             "-ggdb -O0 -fno-omit-frame-pointer")
set(GENERAL_PROFILE_FLAGS           "-fprofile-arcs -ftest-coverage -fsanitize=address")
set(GENERAL_RELEASE_FLAGS           "-DNDEBUG -O3 -fomit-frame-pointer -funswitch-loops")
set(GENERAL_COMPILER_FLAGS          "-pipe")

set(CMAKE_CXX_FLAGS_DEFAULT         "-std=gnu++14")
set(CMAKE_C_FLAGS_DEFAULT           "-std=gnu99")
set(CMAKE_EXE_LINKER_FLAGS_DEFAULT  "")
set(CMAKE_EXE_LINKER_FLAGS_DEBUG    "-rdynamic")
set(CMAKE_EXE_LINKER_FLAGS_PROFILE  "-fprofile-arcs -ftest-coverage -fsanitize=address")
set(CMAKE_EXE_LINKER_FLAGS_RELEASE  "-s")

set(CMAKE_CXX_FLAGS                 "${CMAKE_CXX_FLAGS_DEFAULT} ${GENERAL_COMPILER_FLAGS} ${GENERAL_WARNING_FLAGS}")
set(CMAKE_CXX_FLAGS_DEBUG           "${CMAKE_CXX_FLAGS_DEBUG_DEFAULT} ${GENERAL_DEBUG_FLAGS}")
set(CMAKE_CXX_FLAGS_RELEASE         "${CMAKE_CXX_FLAGS_RELEASE_DEFAULT} ${GENERAL_RELEASE_FLAGS}")
set(CMAKE_C_FLAGS                   "${CMAKE_C_FLAGS_DEFAULT} ${GENERAL_WARNING_FLAGS} ${GENERAL_COMPILER_FLAGS}")
set(CMAKE_C_FLAGS_DEBUG             "${CMAKE_C_FLAGS_DEBUG_DEFAULT} ${GENERAL_DEBUG_FLAGS}")
set(CMAKE_C_FLAGS_RELEASE           "${CMAKE_C_FLAGS_RELEASE_DEFAULT} ${GENERAL_RELEASE_FLAGS}")

set(DSP_SOURCE_DIR                  "${CMAKE_CURRENT_SOURCE_DIR}/src")
set(DSP_INCLUDE_DIR                 "${CMAKE_CURRENT_SOURCE_DIR}/include")
include_directories(AFTER           "${DSP_INCLUDE_DIR}")


set(DSP_BASE_FILES_C                "${DSP_SOURCE_DIR}/dsp.c"
                                    "${DSP_SOURCE_DIR}/effect.c"
                                    "${DSP_SOURCE_DIR}/codec.c"
                                    "${DSP_SOURCE_DIR}/sampleconv.c"
                                    "${DSP_SOURCE_DIR}/util.c"
                                    "${DSP_SOURCE_DIR}/biquad.c"
                                    "${DSP_SOURCE_DIR}/gain.c"
                                    "${DSP_SOURCE_DIR}/crossfeed.c"
                                    "${DSP_SOURCE_DIR}/remix.c"
                                    "${DSP_SOURCE_DIR}/delay.c"
                                    "${DSP_SOURCE_DIR}/noise.c"
                                    "${DSP_SOURCE_DIR}/compress.c"
                                    "${DSP_SOURCE_DIR}/stats.c"
                                    "${DSP_SOURCE_DIR}/null.c"
                                    "${DSP_SOURCE_DIR}/pcm.c"
)

set(DSP_BASE_FILES_H                "${DSP_INCLUDE_DIR}/dsp.h"
                                    "${DSP_INCLUDE_DIR}/effect.h"
                                    "${DSP_INCLUDE_DIR}/codec.h"
                                    "${DSP_INCLUDE_DIR}/sampleconv.h"
                                    "${DSP_INCLUDE_DIR}/util.h"
                                    "${DSP_INCLUDE_DIR}/biquad.h"
                                    "${DSP_INCLUDE_DIR}/gain.h"
                                    "${DSP_INCLUDE_DIR}/crossfeed.h"
                                    "${DSP_INCLUDE_DIR}/remix.h"
                                    "${DSP_INCLUDE_DIR}/delay.h"
                                    "${DSP_INCLUDE_DIR}/noise.h"
                                    "${DSP_INCLUDE_DIR}/compress.h"
                                    "${DSP_INCLUDE_DIR}/stats.h"
                                    "${DSP_INCLUDE_DIR}/null.h"
                                    "${DSP_INCLUDE_DIR}/pcm.h"
)

set(DSP_LADSPA_DSP_FILES_C          "${DSP_SOURCE_DIR}/ladspa_dsp.c"
                                    "${DSP_SOURCE_DIR}/effect.c"
                                    "${DSP_SOURCE_DIR}/util.c"
                                    "${DSP_SOURCE_DIR}/biquad.c"
                                    "${DSP_SOURCE_DIR}/gain.c"
                                    "${DSP_SOURCE_DIR}/crossfeed.c"
                                    "${DSP_SOURCE_DIR}/remix.c"
                                    "${DSP_SOURCE_DIR}/delay.c"
                                    "${DSP_SOURCE_DIR}/noise.c"
                                    "${DSP_SOURCE_DIR}/compress.c"
                                    "${DSP_SOURCE_DIR}/stats.c"
)

set(DSP_LADSPA_DSP_FILES_H          "${DSP_INCLUDE_DIR}/effect.h"
                                    "${DSP_INCLUDE_DIR}/util.h"
                                    "${DSP_INCLUDE_DIR}/biquad.h"
                                    "${DSP_INCLUDE_DIR}/gain.h"
                                    "${DSP_INCLUDE_DIR}/crossfeed.h"
                                    "${DSP_INCLUDE_DIR}/remix.h"
                                    "${DSP_INCLUDE_DIR}/delay.h"
                                    "${DSP_INCLUDE_DIR}/noise.h"
                                    "${DSP_INCLUDE_DIR}/compress.h"
                                    "${DSP_INCLUDE_DIR}/stats.h"
)


set(DSP_G2REVERB_FILES_CXX          "${DSP_SOURCE_DIR}/g2reverb.cpp")
set(DSP_G2REVERB_FILES_HPP          "${DSP_INCLUDE_DIR}/g2reverb_cpp.h")

set(DSP_LADSPA_FILES_C              "${DSP_SOURCE_DIR}/ladspa_host.c")
set(DSP_LADSPA_FILES_H              "${DSP_INCLUDE_DIR}/ladspa_host.h")

set(DSP_SNDFILE_FILES_C             "${DSP_SOURCE_DIR}/sndfile.c")
set(DSP_SNDFILE_FILES_H             "${DSP_INCLUDE_DIR}/sndfile.h")

set(DSP_FFMPEG_FILES_C              "${DSP_SOURCE_DIR}/ffmpeg.c")
set(DSP_FFMPEG_FILES_H              "${DSP_INCLUDE_DIR}/ffmpeg.h")

set(DSP_FFTW_FILES_C                "${DSP_SOURCE_DIR}/resample.c"
                                    "${DSP_SOURCE_DIR}/fir.c")

set(DSP_FFTW_FILES_H                "${DSP_INCLUDE_DIR}/resample.h"
                                    "${DSP_INCLUDE_DIR}/fir.h")

set(DSP_ZITA_CONVOLVER_FILES_CXX    "${DSP_SOURCE_DIR}/zita-convolver.cpp")
set(DSP_ZITA_CONVOLVER_FILES_HPP    "${DSP_INCLUDE_DIR}/zita-convolver.h")

set(DSP_ALSA_FILES_C                "${DSP_SOURCE_DIR}/alsa.c")
set(DSP_ALSA_FILES_H                "${DSP_INCLUDE_DIR}/alsa.h")

set(DSP_AO_FILES_C                  "${DSP_SOURCE_DIR}/ao.c")
set(DSP_AO_FILES_H                  "${DSP_INCLUDE_DIR}/ao.h")

set(DSP_MAD_FILES_C                 "${DSP_SOURCE_DIR}/mp3.c")
set(DSP_MAD_FILES_H                 "${DSP_INCLUDE_DIR}/mp3.h")

set(DSP_PULSE_FILES_C               "${DSP_SOURCE_DIR}/pulse.c")
set(DSP_PULSE_FILES_H               "${DSP_INCLUDE_DIR}/pulse.h")


set(DSP_CODECS_FILES_C              "${DSP_SOURCE_DIR}/codec.c"
                                    "${DSP_SOURCE_DIR}/sampleconv.c"
)

set(DSP_CODECS_FILES_H              "${DSP_INCLUDE_DIR}/codec.h"
                                    "${DSP_INCLUDE_DIR}/sampleconv.h"
)

add_library(ladspa_dsp_object OBJECT ${DSP_LADSPA_DSP_FILES_C} ${DSP_LADSPA_DSP_FILES_H})
set_property(TARGET ladspa_dsp_object PROPERTY POSITION_INDEPENDENT_CODE TRUE)

add_library(ladspa_dsp_static STATIC $<TARGET_OBJECTS:ladspa_dsp_object>)
add_library(ladspa_dsp_shared SHARED $<TARGET_OBJECTS:ladspa_dsp_object>)
