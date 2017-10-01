cmake_minimum_required(VERSION 3.0.2)
project(dsp)

if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE "Release" CACHE STRING "Choose the type of build, options are: Debug Release." FORCE)
endif(NOT CMAKE_BUILD_TYPE)

if(CMAKE_BUILD_TYPE STREQUAL "Debug")
    set(CMAKE_VERBOSE_MAKEFILE ON)
endif()

########################################################################################################################

set(GENERAL_WARNING_FLAGS           "-Wall")
set(GENERAL_DEBUG_FLAGS             "-ggdb -O0 -fno-omit-frame-pointer")
set(GENERAL_PROFILE_FLAGS           "-fprofile-arcs -ftest-coverage -fsanitize=address")
set(GENERAL_RELEASE_FLAGS           "-DNDEBUG -O3 -fomit-frame-pointer -funswitch-loops")
set(GENERAL_COMPILER_FLAGS          "-pipe")

set(CMAKE_CXX_FLAGS_DEFAULT         "-std=gnu++14")
set(CMAKE_C_FLAGS_DEFAULT           "-std=gnu99")
set(CMAKE_EXE_LINKER_FLAGS_DEFAULT  "")
set(CMAKE_EXE_LINKER_FLAGS_DEBUG    "")
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

########################################################################################################################

##### DSP executable files #####
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


##### ladspa_dsp library files #####
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


##### Optional GPL Code #####
set(DSP_REVERB_FILES_C              "${DSP_SOURCE_DIR}/reverb.c")
set(DSP_REVERB_FILES_H              "${DSP_INCLUDE_DIR}/reverb.h")
set(DSP_G2REVERB_FILES_CXX          "${DSP_SOURCE_DIR}/g2reverb.cpp")
set(DSP_G2REVERB_FILES_HPP          "${DSP_INCLUDE_DIR}/g2reverb_cpp.h")

##### Optional sndfile #####
set(DSP_SNDFILE_FILES_C             "${DSP_SOURCE_DIR}/sndfile.c")
set(DSP_SNDFILE_FILES_H             "${DSP_INCLUDE_DIR}/sndfile.h")

##### Optional ffmpeg #####
set(DSP_FFMPEG_FILES_C              "${DSP_SOURCE_DIR}/ffmpeg.c")
set(DSP_FFMPEG_FILES_H              "${DSP_INCLUDE_DIR}/ffmpeg.h")

##### Optional fftw #####
set(DSP_FFTW3_FILES_C               "${DSP_SOURCE_DIR}/resample.c"
                                    "${DSP_SOURCE_DIR}/fir.c"
)
set(DSP_FFTW3_FILES_H               "${DSP_INCLUDE_DIR}/resample.h"
                                    "${DSP_INCLUDE_DIR}/fir.h"
)

##### Optional zita convolver #####
set(DSP_ZITA_CONVOLVER_FILES_CXX    "${DSP_SOURCE_DIR}/zita_convolver.cpp")
set(DSP_ZITA_CONVOLVER_FILES_HPP    "${DSP_INCLUDE_DIR}/zita_convolver.h")

##### Optional alsa #####
set(DSP_ALSA_FILES_C                "${DSP_SOURCE_DIR}/alsa.c")
set(DSP_ALSA_FILES_H                "${DSP_INCLUDE_DIR}/alsa.h")

##### Optional ao #####
set(DSP_AO_FILES_C                  "${DSP_SOURCE_DIR}/ao.c")
set(DSP_AO_FILES_H                  "${DSP_INCLUDE_DIR}/ao.h")

##### Optional mad #####
set(DSP_MAD_FILES_C                 "${DSP_SOURCE_DIR}/mp3.c")
set(DSP_MAD_FILES_H                 "${DSP_INCLUDE_DIR}/mp3.h")

##### Optional pulse #####
set(DSP_PULSE_FILES_C               "${DSP_SOURCE_DIR}/pulse.c")
set(DSP_PULSE_FILES_H               "${DSP_INCLUDE_DIR}/pulse.h")


##### Optional codecs #####
set(DSP_CODECS_FILES_C              "${DSP_SOURCE_DIR}/codec.c"
                                    "${DSP_SOURCE_DIR}/sampleconv.c"
)
set(DSP_CODECS_FILES_H              "${DSP_INCLUDE_DIR}/codec.h"
                                    "${DSP_INCLUDE_DIR}/sampleconv.h"
)

########################################################################################################################

##### ladspa_dsp library #####
if (NOT DISABLE_LADSPA_DSP)
    set(ladspa_dsp_files ${DSP_LADSPA_DSP_FILES_C} ${DSP_LADSPA_DSP_FILES_H})
    set(ladspa_definitions "PIC" "__LADSPA_FRONTEND__" "__SYMMETRIC_IO__")
    set(ladspa_libs "")
    set(INCLUDE_CODECS FALSE)

    if (NOT DISABLE_GPL_CODE)
        list(APPEND ladspa_dsp_files ${DSP_REVERB_FILES_C} ${DSP_REVERB_FILES_H} ${DSP_G2REVERB_FILES_CXX} ${DSP_G2REVERB_FILES_HPP})
        list(APPEND ladspa_definitions "__ENABLE_GPL_CODE__")
    endif (NOT DISABLE_GPL_CODE)

    if (NOT DISABLE_FFTW3 AND HAVE_FFTW3)
        list(APPEND ladspa_dsp_files ${DSP_FFTW3_FILES_C} ${DSP_FFTW3_FILES_H})
        list(APPEND ladspa_definitions "__HAVE_FFTW3__")
        set(INCLUDE_CODECS TRUE)
    endif (NOT DISABLE_FFTW3 AND HAVE_FFTW3)

    if (NOT DISABLE_ZITA_CONVOLVER AND HAVE_ZITA_CONVOLVER)
        list(APPEND ladspa_dsp_files ${DSP_ZITA_CONVOLVER_FILES_CXX} ${DSP_ZITA_CONVOLVER_FILES_HPP})
        list(APPEND ladspa_definitions "__HAVE_ZITA_CONVOLVER__")
        set(INCLUDE_CODECS TRUE)
    endif (NOT DISABLE_ZITA_CONVOLVER AND HAVE_ZITA_CONVOLVER)

    if (INCLUDE_CODECS)
        if (NOT DISABLE_SNDFILE AND HAVE_SNDFILE)
            list(APPEND ladspa_dsp_files ${DSP_SNDFILE_FILES_C} ${DSP_SNDFILE_FILES_H})
            list(APPEND ladspa_definitions "__HAVE_SNDFILE__")
        endif (NOT DISABLE_SNDFILE AND HAVE_SNDFILE)

        if (NOT DISABLE_FFMPEG AND HAVE_FFMPEG)
            list(APPEND ladspa_dsp_files ${DSP_FFMPEG_FILES_C} ${DSP_FFMPEG_FILES_H})
            list(APPEND ladspa_definitions "__HAVE_FFMPEG__")
        endif (NOT DISABLE_FFMPEG AND HAVE_FFMPEG)

        list(APPEND ladspa_dsp_files ${DSP_CODECS_FILES_C} ${DSP_CODECS_FILES_H})
    endif (INCLUDE_CODECS)

    add_library(ladspa_dsp_object OBJECT ${ladspa_dsp_files})
    target_compile_definitions(ladspa_dsp_object PRIVATE ${ladspa_definitions})
    set_property(TARGET ladspa_dsp_object PROPERTY POSITION_INDEPENDENT_CODE TRUE)

    add_library(ladspa_dsp_shared SHARED $<TARGET_OBJECTS:ladspa_dsp_object>)

    if (NOT ${ladspa_libs} STREQUAL "")
        target_link_libraries(ladspa_dsp ${ladspa_libs})
    endif (NOT ${ladspa_libs} STREQUAL "")

endif (NOT DISABLE_LADSPA_DSP)

##### dsp executable #####
if (NOT DISABLE_DSP)
    set(dsp_files ${DSP_BASE_FILES_C} ${DSP_BASE_FILES_H})
    set(dsp_definitions "")
    set(dsp_libs "m")

    if (NOT DISABLE_GPL_CODE)
        list(APPEND dsp_files ${DSP_REVERB_FILES_C} ${DSP_REVERB_FILES_H} ${DSP_G2REVERB_FILES_CXX} ${DSP_G2REVERB_FILES_HPP})
        list(APPEND dsp_definitions "__ENABLE_GPL_CODE__")
    endif (NOT DISABLE_GPL_CODE)

    if (NOT DISABLE_SNDFILE AND HAVE_SNDFILE)
        list(APPEND dsp_files ${DSP_SNDFILE_FILES_C} ${DSP_SNDFILE_FILES_H})
        list(APPEND dsp_definitions "__HAVE_SNDFILE__")
    endif (NOT DISABLE_SNDFILE AND HAVE_SNDFILE)

    if (NOT DISABLE_FFMPEG AND HAVE_FFMPEG)
        list(APPEND dsp_files ${DSP_FFMPEG_FILES_C} ${DSP_FFMPEG_FILES_H})
        list(APPEND dsp_definitions "__HAVE_FFMPEG__")
    endif (NOT DISABLE_FFMPEG AND HAVE_FFMPEG)

    if (NOT DISABLE_FFTW3 AND HAVE_FFTW3)
        list(APPEND dsp_files ${DSP_FFTW3_FILES_C} ${DSP_FFTW3_FILES_H})
        list(APPEND dsp_definitions "__HAVE_FFTW3__")
    endif (NOT DISABLE_FFTW3 AND HAVE_FFTW3)

    if (NOT DISABLE_ZITA_CONVOLVER AND HAVE_ZITA_CONVOLVER)
        list(APPEND dsp_files ${DSP_ZITA_CONVOLVER_FILES_CXX} ${DSP_ZITA_CONVOLVER_FILES_HPP})
        list(APPEND dsp_definitions "__HAVE_ZITA_CONVOLVER__")
    endif (NOT DISABLE_ZITA_CONVOLVER AND HAVE_ZITA_CONVOLVER)

    if (NOT DISABLE_ALSA AND HAVE_ALSA)
        list(APPEND dsp_files ${DSP_ALSA_FILES_C} ${DSP_ALSA_FILES_H})
        list(APPEND dsp_definitions "__HAVE_ALSA__")
    endif (NOT DISABLE_ALSA AND HAVE_ALSA)

    if (NOT DISABLE_AO AND HAVE_AO)
        list(APPEND dsp_files ${DSP_AO_FILES_C} ${DSP_AO_FILES_H})
        list(APPEND dsp_definitions "__HAVE_AO__")
    endif (NOT DISABLE_AO AND HAVE_AO)

    if (NOT DISABLE_MAD AND HAVE_MAD)
        list(APPEND dsp_files ${DSP_MAD_FILES_C} ${DSP_MAD_FILES_H})
        list(APPEND dsp_definitions "__HAVE_MAD__")
    endif (NOT DISABLE_MAD AND HAVE_MAD)

    if (NOT DISABLE_PULSE AND HAVE_PULSE)
        list(APPEND dsp_files ${DSP_PULSE_FILES_C} ${DSP_PULSE_FILES_H})
        list(APPEND dsp_definitions "__HAVE_PULSE__")
    endif (NOT DISABLE_PULSE AND HAVE_PULSE)

    add_executable(dsp ${dsp_files})
    target_compile_definitions(dsp PRIVATE ${dsp_definitions})

    if (NOT ${dsp_libs} STREQUAL "")
        target_link_libraries(dsp ${dsp_libs})
    endif (NOT ${dsp_libs} STREQUAL "")

endif (NOT DISABLE_DSP)
