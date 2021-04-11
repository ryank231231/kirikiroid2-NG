cmake_minimum_required(VERSION 3.5.0)
project(krkr2)
# include(AndroidNdkModules)
# android_ndk_import_module_cpufeatures()


aux_source_directory(${CMAKE_CURRENT_SOURCE_DIR}/visual LOCAL_SRC_FILES_visual)
list(REMOVE_ITEM LOCAL_SRC_FILES_visual ${CMAKE_CURRENT_SOURCE_DIR}/visual/Resampler.cpp  ${CMAKE_CURRENT_SOURCE_DIR}/visual/LoadJXR.cpp)
aux_source_directory(${CMAKE_CURRENT_SOURCE_DIR}/base/win32 LOCAL_SRC_FILES_base_win32)
list(REMOVE_ITEM LOCAL_SRC_FILES_base_win32 ${CMAKE_CURRENT_SOURCE_DIR}/base/win32/FuncStubs.cpp  ${CMAKE_CURRENT_SOURCE_DIR}/base/win32/SusieArchive.cpp)
aux_source_directory(${CMAKE_CURRENT_SOURCE_DIR}/base LOCAL_SRC_FILES_base)
#list(REMOVE_ITEM LOCAL_SRC_FILES_visual ${CMAKE_CURRENT_SOURCE_DIR}/visual/Resampler.cpp  ${CMAKE_CURRENT_SOURCE_DIR}/visual/LoadJXR.cpp)

aux_source_directory(${CMAKE_CURRENT_SOURCE_DIR}/environ LOCAL_SRC_FILES_environ)
list(REMOVE_ITEM LOCAL_SRC_FILES_environ ${CMAKE_CURRENT_SOURCE_DIR}/environ/MainFormUnit.cpp ${CMAKE_CURRENT_SOURCE_DIR}/environ/XP3ArchiveRepack.cpp)
aux_source_directory(${CMAKE_CURRENT_SOURCE_DIR}/environ/cocos2d LOCAL_SRC_FILES_environ_cocos2d)
#list(REMOVE_ITEM LOCAL_SRC_FILES_environ_cocos2d ${CMAKE_CURRENT_SOURCE_DIR}/environ/cocos2d/CustomFileUtils.cpp ${CMAKE_CURRENT_SOURCE_DIR}/environ/cocos2d/CustomFileUtils.mm)
aux_source_directory(${CMAKE_CURRENT_SOURCE_DIR}/environ/android LOCAL_SRC_FILES_environ_android)
aux_source_directory(${CMAKE_CURRENT_SOURCE_DIR}/environ/linux LOCAL_SRC_FILES_environ_linux)
aux_source_directory(${CMAKE_CURRENT_SOURCE_DIR}/environ/ui LOCAL_SRC_FILES_environ_ui)
aux_source_directory(${CMAKE_CURRENT_SOURCE_DIR}/environ/ui/extension LOCAL_SRC_FILES_environ_ui_ext)
aux_source_directory(${CMAKE_CURRENT_SOURCE_DIR}/extension LOCAL_SRC_FILES_extension)
file(GLOB LOCAL_SRC_FILES_movie ${CMAKE_CURRENT_SOURCE_DIR}/movie/*.cpp )
file(GLOB LOCAL_SRC_FILES_movie_1 ${CMAKE_CURRENT_SOURCE_DIR}/movie/*/*.cpp)
file(GLOB LOCAL_SRC_FILES_msg ${CMAKE_CURRENT_SOURCE_DIR}/msg/*.cpp) 
file(GLOB LOCAL_SRC_FILES_tjs ${CMAKE_CURRENT_SOURCE_DIR}/tjs2/*.cpp) 
file(GLOB LOCAL_SRC_FILES_sound ${CMAKE_CURRENT_SOURCE_DIR}/sound/*.cpp)
file(GLOB LOCAL_SRC_FILES_sound_win32 ${CMAKE_CURRENT_SOURCE_DIR}/sound/win32/*.cpp)
list(REMOVE_ITEM LOCAL_SRC_FILES_sound_win32 ${CMAKE_CURRENT_SOURCE_DIR}/sound/xmmlib.cpp ${CMAKE_CURRENT_SOURCE_DIR}/sound/WaveFormatConverter_SSE.cpp)
file(GLOB LOCAL_SRC_FILES_visual_gl ${CMAKE_CURRENT_SOURCE_DIR}/visual/gl/*.cpp)
file(GLOB LOCAL_SRC_FILES_visual_ogl ${CMAKE_CURRENT_SOURCE_DIR}/visual/ogl/*.cpp) 
aux_source_directory(${CMAKE_CURRENT_SOURCE_DIR}/visual/win32 LOCAL_SRC_FILES_visual_win32)
list(REMOVE_ITEM LOCAL_SRC_FILES_visual_win32
    ${CMAKE_CURRENT_SOURCE_DIR}/visual/win32/GDIFontRasterizer.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/visual/win32/NativeFreeTypeFace.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/visual/win32/TVPSysFont.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/visual/win32/VSyncTimingThread.cpp
    )
aux_source_directory(${CMAKE_CURRENT_SOURCE_DIR}/utils LOCAL_SRC_FILES_utils)
file(GLOB LOCAL_SRC_FILES_utils_encoding ${CMAKE_CURRENT_SOURCE_DIR}/utils/encoding/*.c) 
aux_source_directory(${CMAKE_CURRENT_SOURCE_DIR}/utils/minizip LOCAL_SRC_FILES_utils_minizip)
aux_source_directory(${CMAKE_CURRENT_SOURCE_DIR}/utils/win32 LOCAL_SRC_FILES_utils_win32)
set(LOCAL_SRC_FILES 
    ${LOCAL_SRC_FILES_base}
    ${LOCAL_SRC_FILES_movie_1}
    ${LOCAL_SRC_FILES_environ_ui} 
    ${LOCAL_SRC_FILES_visual_gl}
    ${LOCAL_SRC_FILES_sound}
    ${LOCAL_SRC_FILES_sound_win32}
    ${LOCAL_SRC_FILES_visual_win32}
    ${LOCAL_SRC_FILES_utils}
    ${LOCAL_SRC_FILES_utils_encoding}
    ${LOCAL_SRC_FILES_utils_minizip}
    ${LOCAL_SRC_FILES_utils_win32}
    ${LOCAL_SRC_FILES_visual_ogl}
    ${LOCAL_SRC_FILES_tjs}
    ${LOCAL_SRC_FILES_msg}
    ${CMAKE_CURRENT_SOURCE_DIR}/msg/win32/MsgImpl.cpp             
    ${CMAKE_CURRENT_SOURCE_DIR}/msg/win32/OptionsDesc.cpp
    ${LOCAL_SRC_FILES_environ_cocos2d}
    ${LOCAL_SRC_FILES_movie}
    ${LOCAL_SRC_FILES_extension}
    ${LOCAL_SRC_FILES_environ_ui_ext}
    ${CMAKE_CURRENT_SOURCE_DIR}/environ/win32/SystemControl.cpp
    ${LOCAL_SRC_FILES_environ_android}
    ${LOCAL_SRC_FILES_environ_linux}
    ${LOCAL_SRC_FILES_visual}
    ${LOCAL_SRC_FILES_base_win32}
    ${LOCAL_SRC_FILES_base}
    ${LOCAL_SRC_FILES_environ}
    
)

add_library(krkr2 
    ${LOCAL_SRC_FILES}
)

target_compile_definitions(krkr2 PUBLIC -DTJS_TEXT_OUT_CRLF -D__STDC_CONSTANT_MACROS -DUSE_UNICODE_FSTRING -DTJS_TEXT_OUT_CRLF -D_7ZIP_ST)

target_include_directories(krkr2
    PUBLIC # PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}/base
    ${CMAKE_CURRENT_SOURCE_DIR}/base/win32
    ${CMAKE_CURRENT_SOURCE_DIR}/environ
    ${CMAKE_CURRENT_SOURCE_DIR}/environ/sdl
    ${CMAKE_CURRENT_SOURCE_DIR}/environ/win32
    ${CMAKE_CURRENT_SOURCE_DIR}/msg
    ${CMAKE_CURRENT_SOURCE_DIR}/msg/win32
    ${CMAKE_CURRENT_SOURCE_DIR}/sound
    ${CMAKE_CURRENT_SOURCE_DIR}/sound/win32
    ${CMAKE_CURRENT_SOURCE_DIR}/tjs2
    ${CMAKE_CURRENT_SOURCE_DIR}/extension
    ${CMAKE_CURRENT_SOURCE_DIR}/utils
    ${CMAKE_CURRENT_SOURCE_DIR}/utils/win32
    ${CMAKE_CURRENT_SOURCE_DIR}/visual
    ${CMAKE_CURRENT_SOURCE_DIR}/visual/ARM
    ${CMAKE_CURRENT_SOURCE_DIR}/visual/win32
    ${CMAKE_CURRENT_SOURCE_DIR}/../plugins
    ${CMAKE_CURRENT_SOURCE_DIR}/../../vendor/freetype2/include/linux/
    ${CMAKE_CURRENT_SOURCE_DIR}/../../vendor/freetype2/include/linux/freetype2
    ${CMAKE_CURRENT_SOURCE_DIR}/../../3rd/cocos2d-x
    ${CMAKE_CURRENT_SOURCE_DIR}/../../3rd/cocos2d-x/cocos
    ${CMAKE_CURRENT_SOURCE_DIR}/../../3rd/cocos2d-x/cocos/editor-support
    ${CMAKE_CURRENT_SOURCE_DIR}/../../3rd/cocos2d-x/extensions
    ${CMAKE_CURRENT_SOURCE_DIR}/../../3rd/cocos2d-x/external
    ${CMAKE_CURRENT_SOURCE_DIR}/../../3rd/cocos2d-x/cocos/platform/
    ${CMAKE_CURRENT_SOURCE_DIR}/../../3rd
    ${CMAKE_CURRENT_SOURCE_DIR}/../../3rd/libjpeg-turbo
    ${CMAKE_CURRENT_SOURCE_DIR}/../../3rd/libjpeg-turbo/build
    ${CMAKE_CURRENT_SOURCE_DIR}/../../3rd/jxrlib/jxrgluelib
    ${CMAKE_CURRENT_SOURCE_DIR}/../../3rd/onig/src
    ${CMAKE_CURRENT_SOURCE_DIR}/../../3rd/openal/include
    ${CMAKE_CURRENT_SOURCE_DIR}/../../3rd/oboe/include
    ${CMAKE_CURRENT_SOURCE_DIR}/../../3rd/SDL/include
    ${CMAKE_CURRENT_SOURCE_DIR}/../../3rd/libvorbis/include
    ${CMAKE_CURRENT_SOURCE_DIR}/../../3rd/wvorbis/ogg/include
    ${CMAKE_CURRENT_SOURCE_DIR}/../../3rd/opus/opus/include
    ${CMAKE_CURRENT_SOURCE_DIR}/../../3rd/opusfile/include
    ${CMAKE_CURRENT_SOURCE_DIR}/../../3rd/libarchive
    ${CMAKE_CURRENT_SOURCE_DIR}/../../3rd/libarchive/contrib/android/include
    ${CMAKE_CURRENT_SOURCE_DIR}/../../3rd/jxrlib/image/sys
    ${CMAKE_CURRENT_SOURCE_DIR}/../../3rd/jxrlib/common/include
    ${CMAKE_CURRENT_SOURCE_DIR}/../../3rd/cocos2d-x/external/png/include/android
    ${CMAKE_CURRENT_SOURCE_DIR}/../../3rd/cocos2d-x/external/webp/include/android
    ${CMAKE_CURRENT_SOURCE_DIR}/../../3rd/ffmpeg
    ${CMAKE_CURRENT_SOURCE_DIR}/../../3rd/opencv/include
    ${CMAKE_CURRENT_SOURCE_DIR}/../../3rd/prebuild/opencv/include
    ${CMAKE_CURRENT_SOURCE_DIR}/../../3rd/prebuild/lz4/include
)