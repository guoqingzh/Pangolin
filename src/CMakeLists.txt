#######################################################
## Library sources

<<<<<<< HEAD
set( INCDIR "../include/Pangolin")
set( SRCDIR "." )
=======
macro( append_glob list glob )
    file(GLOB files ${glob})
    set(${list} "${${list}};${files}")
endmacro()

>>>>>>> stevenlovegrove/master

## Header only includes / core headers
set( INCDIR "../include/pangolin" )
set( HEADERS
  ${INCDIR}/pangolin.h
  ${INCDIR}/platform.h
)
append_glob(HEADERS ${INCDIR}/utils/*.h*)
append_glob(HEADERS ${INCDIR}/image/*.h*)
append_glob(HEADERS ${INCDIR}/log/*.h*)

<<<<<<< HEAD
## Store list of source files
set( SOURCES
    ${SRCDIR}/file_utils.cpp
    ${SRCDIR}/image_load.cpp
    ${SRCDIR}/video_common.cpp
    )
=======
### Store list of source files
append_glob(SOURCES utils/*.cpp)
append_glob(SOURCES image/*.cpp)
append_glob(SOURCES log/*.cpp)
>>>>>>> stevenlovegrove/master

#######################################################
## User build options

option(BUILD_PANGOLIN_GUI "Build support for Pangolin GUI" ON)
if(BUILD_PANGOLIN_GUI)
<<<<<<< HEAD
  list(APPEND HEADERS
    ${INCDIR}/display.h ${INCDIR}/display_internal.h
    ${INCDIR}/view.h ${INCDIR}/viewport.h
    ${INCDIR}/handler.h ${INCDIR}/handler_enums.h
    ${INCDIR}/handler_glbuffer.h
    ${INCDIR}/opengl_render_state.h
    ${INCDIR}/datalog.h
    ${INCDIR}/glfont.h ${INCDIR}/glpangoglu.h
  )

  list(APPEND SOURCES
    ${SRCDIR}/display.cpp
    ${SRCDIR}/view.cpp
    ${SRCDIR}/viewport.cpp
    ${SRCDIR}/handler.cpp
    ${SRCDIR}/handler_glbuffer.cpp
    ${SRCDIR}/opengl_render_state.cpp
    ${SRCDIR}/datalog.cpp
    ${SRCDIR}/glfont.cpp
    ${SRCDIR}/glpangoglu.cpp
  )

  if(NOT HAVE_GLES OR HAVE_GLES_2)
    list(APPEND HEADERS ${INCDIR}/plotter.h)
    list(APPEND SOURCES ${SRCDIR}/plotter.cpp)
=======
  append_glob(HEADERS ${INCDIR}/gl/*.h*)
  append_glob(HEADERS ${INCDIR}/display/*.h*)
  append_glob(HEADERS ${INCDIR}/handler/*.h*)

  append_glob(SOURCES gl/*.cpp)
  append_glob(SOURCES display/*.cpp)
  append_glob(SOURCES handler/*.cpp)

  if(NOT HAVE_GLES OR HAVE_GLES_2)
    append_glob(HEADERS ${INCDIR}/plot/*.h*)
    append_glob(SOURCES plot/*.cpp)
>>>>>>> stevenlovegrove/master
  endif()

endif()

option(BUILD_PANGOLIN_VARS "Build support for Pangolin Vars" ON)
if(BUILD_PANGOLIN_VARS)
<<<<<<< HEAD
  list(APPEND HEADERS ${INCDIR}/var/var.h ${INCDIR}/var/varextra.h
    ${INCDIR}/var/varstate.h ${INCDIR}/var/varvalue.h
    ${INCDIR}/var/varvaluegeneric.h ${INCDIR}/var/varvaluet.h
    ${INCDIR}/var/varwrapper.h ${INCDIR}/input_record_repeat.h
  )
  list(APPEND SOURCES ${SRCDIR}/var/vars.cpp ${SRCDIR}/input_record_repeat.cpp )

  if(BUILD_PANGOLIN_GUI)
      list(APPEND HEADERS ${INCDIR}/widgets.h )
      list(APPEND SOURCES ${SRCDIR}/widgets.cpp )
=======
  append_glob(HEADERS ${INCDIR}/var/*.h*)
  append_glob(SOURCES var/*.cpp)

  if(BUILD_PANGOLIN_GUI)
      list(APPEND HEADERS ${INCDIR}/display/widgets/widgets.h )
      list(APPEND SOURCES display/widgets/widgets.cpp )
>>>>>>> stevenlovegrove/master
  endif()
endif()

option(BUILD_PANGOLIN_VIDEO "Build support for Pangolin Video Utilities" ON)
if(BUILD_PANGOLIN_VIDEO)
  # Generic video includes
  append_glob(HEADERS ${INCDIR}/video/*.h*)
  append_glob(SOURCES video/*.cpp)

  # Generic video drivers
  list(APPEND HEADERS
    ${INCDIR}/video/drivers/test.h
    ${INCDIR}/video/drivers/images.h
    ${INCDIR}/video/drivers/video_splitter.h
    ${INCDIR}/video/drivers/pvn_video.h
    ${INCDIR}/video/drivers/pango_video.h
    ${INCDIR}/video/drivers/pango_video_output.h
    ${INCDIR}/video/drivers/debayer.h
    ${INCDIR}/video/drivers/shift.h
    ${INCDIR}/video/drivers/mirror.h
    ${INCDIR}/video/drivers/unpack.h
    ${INCDIR}/video/drivers/join.h
    ${INCDIR}/video/drivers/thread.h
  )
  list(APPEND SOURCES
<<<<<<< HEAD
    ${SRCDIR}/threadedfilebuf.cpp
    ${SRCDIR}/video.cpp
    ${SRCDIR}/video_splitter.cpp
    ${SRCDIR}/video_output.cpp
    ${SRCDIR}/video_recorder.cpp
    ${SRCDIR}/video_record_repeat.cpp
    ${SRCDIR}/video/pvn_video.cpp
    ${SRCDIR}/video/test.cpp
    ${SRCDIR}/video/images.cpp
=======
    video/drivers/test.cpp
    video/drivers/images.cpp
    video/drivers/video_splitter.cpp
    video/drivers/pvn_video.cpp
    video/drivers/pango_video.cpp
    video/drivers/pango_video_output.cpp
    video/drivers/debayer.cpp
    video/drivers/shift.cpp
    video/drivers/mirror.cpp
    video/drivers/unpack.cpp
    video/drivers/join.cpp
    video/drivers/thread.cpp
>>>>>>> stevenlovegrove/master
  )

  if(UNIX)
    list(APPEND HEADERS ${INCDIR}/video/drivers/shared_memory.h)
    list(APPEND SOURCES video/drivers/shared_memory.cpp)
    if(_LINUX_)
      # Required for shared memory API using some versions of glibc
      list(APPEND LINK_LIBS rt pthread)
    endif()
  endif()

endif()

#######################################################
## Setup required includes / link info

# Project headers trump everything (including any potentially installed Pangolin)
list(APPEND LIB_INC_DIR  "${PROJECT_SOURCE_DIR}/include;${CMAKE_CURRENT_BINARY_DIR}/include" )

if(NOT CPP11_NO_BOOST)
    # Boost is required when c++11 is disabled
    find_package(Boost COMPONENTS thread filesystem system REQUIRED QUIET)
    list(APPEND USER_INC  "${Boost_INCLUDE_DIRS}" )
    list(APPEND LINK_LIBS "${Boost_LIBRARIES}" )
endif()

if(BUILD_PANGOLIN_GUI)
    if( ANDROID  )
        # Android specific display code
<<<<<<< HEAD
        list(APPEND HEADERS ${INCDIR}/display_android.h )
        list(APPEND SOURCES ${SRCDIR}/display_android.cpp )
=======
        list(APPEND HEADERS ${INCDIR}/display/device/display_android.h )
        list(APPEND SOURCES display/device/display_android.cpp )
>>>>>>> stevenlovegrove/master

        if(HAVE_GLES_2)
            list(APPEND LINK_LIBS "-lEGL;-lGLESv2" )
        else()
            list(APPEND LINK_LIBS "-lEGL;-lGLESv1_CM" )
        endif()
    elseif( IOS )
        list(APPEND LINK_LIBS "-framework OpenGLES" )
        list(APPEND HEADERS "${INCDIR}/ios/PangolinAppDelegate.h" "${INCDIR}/ios/PangolinViewController.h" )
        list(APPEND SOURCES ${SRCDIR}/ios/PangolinAppDelegate.mm
            ${SRCDIR}/ios/PangolinViewController.mm )
    else()
        find_package(OpenGL REQUIRED QUIET)
        list(APPEND USER_INC  "${OPENGL_INCLUDE_DIR}" )
        list(APPEND LINK_LIBS "${OPENGL_LIBRARIES}" )

        if(NOT BUILD_EXTERN_GLEW)
            find_package(GLEW REQUIRED QUIET)
        endif()
        if(GLEW_FOUND)
            list(APPEND USER_INC  "${GLEW_INCLUDE_DIR}" )
            list(APPEND LINK_LIBS "${GLEW_LIBRARY}" )
            set(HAVE_GLEW 1)
        endif()
    endif()

    if( HAVE_GLES_2 )
        # Add Pangolins backwards compat layer.
        list(APPEND HEADERS ${INCDIR}/gl2engine.h )
        list(APPEND SOURCES ${SRCDIR}/gl2engine.cpp)
    endif()
endif()

#######################################################
## Find optional dependencies

if(ANDROID)
    # Fix issue with thread local storage on android.
    add_definitions(-fno-data-sections)
    list(APPEND LINK_LIBS android log)
elseif(IOS)
    # Nothing specific in here yet.
else()
<<<<<<< HEAD
    find_package(CUDA QUIET)
    if(CUDA_FOUND AND NOT _CLANG_)
      set(HAVE_CUDA 1)
      cuda_include_directories(${CMAKE_CURRENT_SOURCE_DIR})
      set(CUDA_ATTACH_VS_BUILD_RULE_TO_CUDA_FILE OFF)
      set(CUDA_NVCC_FLAGS "-O3" )
      add_definitions(-DCUDA_BUILD)
      message(STATUS "CUDA Found and Enabled")
    endif()

    find_package(FREEGLUT QUIET)
    find_package(GLUT QUIET)

    if(_OSX_)
      INCLUDE(CheckCXXSourceRuns)
      set(CMAKE_REQUIRED_LIBRARIES ${GLUT_LIBRARY})
      CHECK_CXX_SOURCE_RUNS("#include <GLUT/glut.h>\n int main () {return glutGetProcAddress(\"glutScrollFunc\") ? 0 : -1;};" HAVE_MODIFIED_OSXGLUT)
      if(NOT HAVE_MODIFIED_OSXGLUT)
            message(STATUS "Install modified osxglut for smooth scroll support / pinch / zoom.")
            message(STATUS "(https://github.com/stevenlovegrove/osxglut)")
      endif()
    endif()

    # Prefer OSX_MODIFIED_GLUT > FREEGLUT > GLUT
    if(FREEGLUT_FOUND AND NOT HAVE_MODIFIED_OSXGLUT)
      set(HAVE_FREEGLUT 1)
      list(APPEND USER_INC  ${FREEGLUT_INCLUDE_DIR} )
      list(APPEND LINK_LIBS ${FREEGLUT_LIBRARY} )
    elseif(GLUT_FOUND)
      list(APPEND USER_INC  ${GLUT_INCLUDE_DIR} )
      list(APPEND LINK_LIBS ${GLUT_LIBRARY} )
      if(_OSX_)
        set(HAVE_APPLE_OPENGL_FRAMEWORK 1)
        if(NOT HAVE_MODIFIED_OSXGLUT)
            message(STATUS "Using Apple Framework GLUT.")
            message(STATUS "Install Freeglut or modified osxglut for scroll support.")
        endif()
      endif()
    endif()

    if(FREEGLUT_FOUND OR GLUT_FOUND)
        set(HAVE_GLUT 1)
        list(APPEND HEADERS ${INCDIR}/display_glut.h )
        list(APPEND SOURCES ${SRCDIR}/display_glut.cpp )
        message(STATUS "Glut Found and Enabled")
=======
    if(BUILD_PANGOLIN_GUI)
        if(FORCE_GLUT)
            find_package(FREEGLUT QUIET)
            find_package(GLUT QUIET)

            if(_OSX_)
              INCLUDE(CheckCXXSourceRuns)
              set(CMAKE_REQUIRED_LIBRARIES ${GLUT_LIBRARY})
              CHECK_CXX_SOURCE_RUNS("#include <GLUT/glut.h>\n int main () {return glutGetProcAddress(\"glutScrollFunc\") ? 0 : -1;};" HAVE_MODIFIED_OSXGLUT)
              if(NOT HAVE_MODIFIED_OSXGLUT)
                    message(STATUS "Install modified osxglut for smooth scroll support / pinch / zoom.")
                    message(STATUS "(https://github.com/stevenlovegrove/osxglut)")
              endif()
            endif()

            # Prefer OSX_MODIFIED_GLUT > FREEGLUT > GLUT
            if(FREEGLUT_FOUND AND NOT HAVE_MODIFIED_OSXGLUT)
              set(HAVE_FREEGLUT 1)
              list(APPEND USER_INC  ${FREEGLUT_INCLUDE_DIR} )
              list(APPEND LINK_LIBS ${FREEGLUT_LIBRARY} )
            elseif(GLUT_FOUND)
              list(APPEND USER_INC  ${GLUT_INCLUDE_DIR} )
              list(APPEND LINK_LIBS ${GLUT_LIBRARY} )
              if(_OSX_)
                set(HAVE_APPLE_OPENGL_FRAMEWORK 1)
                if(NOT HAVE_MODIFIED_OSXGLUT)
                    message(STATUS "Using Apple Framework GLUT.")
                    message(STATUS "Install Freeglut or modified osxglut for scroll support.")
                endif()
              endif()
            endif()

            if(FREEGLUT_FOUND OR GLUT_FOUND)
                set(HAVE_GLUT 1)
                list(APPEND HEADERS ${INCDIR}/display/device/display_glut.h )
                list(APPEND SOURCES display/device/display_glut.cpp )
                message(STATUS "Glut Found and Enabled")
            endif()
        elseif(_WIN_)
            list(APPEND SOURCES display/device/display_win.cpp )
        elseif(_OSX_)
            list(APPEND SOURCES display/device/display_osx.mm display/device/PangolinNSApplication.mm display/device/PangolinNSGLView.mm  )
            list(APPEND LINK_LIBS "-framework Cocoa" )
        elseif(_LINUX_)
            find_package(X11 REQUIRED)
            list(APPEND USER_INC ${X11_INCLUDE_DIR})
            list(APPEND SOURCES display/device/display_x11.cpp )
            list(APPEND LINK_LIBS ${X11_LIBRARIES} )
        endif()
>>>>>>> stevenlovegrove/master
    endif()
endif()

if(UNIX)
  append_glob(HEADERS ${INCDIR}/utils/posix/*.h*)
  append_glob(SOURCES utils/posix/*.cpp)
endif()

find_package(PythonLibs QUIET)
if(BUILD_PANGOLIN_GUI AND BUILD_PANGOLIN_VARS AND PYTHONLIBS_FOUND AND NOT _WIN_)
  set(HAVE_PYTHON 1)
  list(APPEND HEADERS
    ${INCDIR}/console/ConsoleInterpreter.h
    ${INCDIR}/console/ConsoleView.h
    ${INCDIR}/python/PyInterpreter.h
    ${INCDIR}/python/PyModulePangolin.h
    ${INCDIR}/python/PyUniqueObj.h
    ${INCDIR}/python/PyVar.h
    ${INCDIR}/python/PyPangoIO.h
  )
  list(APPEND SOURCES
    console/ConsoleView.cpp
    python/PyInterpreter.cpp
    python/PyModulePangolin.cpp
  )
  if(_GCC_)
    set_source_files_properties(python/PyInterpreter.cpp PROPERTIES COMPILE_FLAGS -fno-strict-aliasing)
  endif()
  list(APPEND INTERNAL_INC ${PYTHON_INCLUDE_DIR})
  list(APPEND LINK_LIBS    ${PYTHON_LIBRARY})
  message(STATUS "Python Found and Enabled")
endif()

option(BUILD_PANGOLIN_OCULUS "Build support for Oculus HUD" OFF)
if(BUILD_PANGOLIN_OCULUS)
  find_package(Oculus QUIET)
  if(Oculus_FOUND)
    set(HAVE_OCULUS 1)
    list(APPEND HEADERS ${INCDIR}/hud/oculus_hud.h )
    list(APPEND SOURCES hud/oculus_hud.cpp )
    list(APPEND USER_INC ${Oculus_INCLUDE_DIRS} )
    list(APPEND LINK_LIBS ${Oculus_LIBRARIES} )
    message(STATUS "Oculus Rift Found and Enabled")
  endif()
endif()

find_package(Eigen3 QUIET)
if(EIGEN3_FOUND)
  set(HAVE_EIGEN 1)
  list(APPEND USER_INC  ${EIGEN3_INCLUDE_DIR} )
  message(STATUS "Eigen Found and Enabled")
endif()

find_package(TooN QUIET)
if(TooN_FOUND)
  set(HAVE_TOON 1)
  list(APPEND USER_INC  ${TooN_INCLUDE_DIR} )
  message(STATUS "TooN Found and Enabled")
endif()

find_package(DC1394 QUIET)
if(BUILD_PANGOLIN_VIDEO AND DC1394_FOUND)
  set(HAVE_DC1394 1)
  list(APPEND INTERNAL_INC  ${DC1394_INCLUDE_DIR} )
  list(APPEND LINK_LIBS  ${DC1394_LIBRARY} )
<<<<<<< HEAD
  list(APPEND HEADERS ${INCDIR}/video/firewire.h ${INCDIR}/video/firewire_deinterlace.h )
  list(APPEND SOURCES ${SRCDIR}/video/firewire.cpp ${SRCDIR}/video/firewire_deinterlace.cpp)
=======
  list(APPEND HEADERS ${INCDIR}/video/drivers/firewire.h ${INCDIR}/video/drivers/firewire_deinterlace.h )
  list(APPEND SOURCES video/drivers/firewire.cpp video/drivers/firewire_deinterlace.cpp)
>>>>>>> stevenlovegrove/master
  message(STATUS "libdc1394 Found and Enabled")
endif()

if(BUILD_PANGOLIN_VIDEO AND _LINUX_)
  set(HAVE_V4L 1)
<<<<<<< HEAD
  list(APPEND HEADERS ${INCDIR}/video/v4l.h)
  list(APPEND SOURCES ${SRCDIR}/video/v4l.cpp)
=======
  list(APPEND HEADERS ${INCDIR}/video/drivers/v4l.h)
  list(APPEND SOURCES video/drivers/v4l.cpp)
>>>>>>> stevenlovegrove/master
  message(STATUS "V4L Found and Enabled")
endif()

find_package(FFMPEG QUIET)
if(BUILD_PANGOLIN_VIDEO AND FFMPEG_FOUND)
  set(HAVE_FFMPEG 1)
  list(APPEND INTERNAL_INC  ${FFMPEG_INCLUDE_DIRS} )
  list(APPEND LINK_LIBS ${FFMPEG_LIBRARIES} )
<<<<<<< HEAD
  list(APPEND HEADERS ${INCDIR}/video/ffmpeg.h)
  list(APPEND SOURCES ${SRCDIR}/video/ffmpeg.cpp)
=======
  list(APPEND HEADERS ${INCDIR}/video/drivers/ffmpeg.h)
  list(APPEND SOURCES video/drivers/ffmpeg.cpp)
>>>>>>> stevenlovegrove/master
  message(STATUS "ffmpeg Found and Enabled")
endif()

find_package(OpenNI QUIET)
if(BUILD_PANGOLIN_VIDEO AND OPENNI_FOUND)
  set(HAVE_OPENNI 1)
  if(_LINUX_)
    add_definitions(-Dlinux=1)
  endif()
  list(APPEND INTERNAL_INC  ${OPENNI_INCLUDE_DIRS} )
  list(APPEND LINK_LIBS ${OPENNI_LIBRARIES} )
<<<<<<< HEAD
  list(APPEND HEADERS ${INCDIR}/video/openni.h )
  list(APPEND SOURCES ${SRCDIR}/video/openni.cpp)
=======
  list(APPEND HEADERS ${INCDIR}/video/drivers/openni.h )
  list(APPEND SOURCES video/drivers/openni.cpp)
>>>>>>> stevenlovegrove/master
  message(STATUS "OpenNI Found and Enabled")
endif()

find_package(OpenNI2 QUIET)
if(BUILD_PANGOLIN_VIDEO AND OPENNI2_FOUND)
  set(HAVE_OPENNI2 1)
  if(_LINUX_)
    add_definitions(-Dlinux=1)
  endif()
  list(APPEND INTERNAL_INC  ${OPENNI2_INCLUDE_DIRS} )
  list(APPEND LINK_LIBS ${OPENNI2_LIBRARIES} )
<<<<<<< HEAD
  list(APPEND HEADERS ${INCDIR}/video/openni2.h )
  list(APPEND SOURCES ${SRCDIR}/video/openni2.cpp)
=======
  list(APPEND HEADERS ${INCDIR}/video/drivers/openni2.h )
  list(APPEND SOURCES video/drivers/openni2.cpp)
>>>>>>> stevenlovegrove/master
  message(STATUS "OpenNI2 Found and Enabled")
endif()

find_package(uvc QUIET)
if(BUILD_PANGOLIN_VIDEO AND uvc_FOUND)
  set(HAVE_UVC 1)
  list(APPEND INTERNAL_INC  ${uvc_INCLUDE_DIRS} )
  list(APPEND LINK_LIBS ${uvc_LIBRARIES} )
<<<<<<< HEAD
  list(APPEND HEADERS ${INCDIR}/video/uvc.h )
  list(APPEND SOURCES ${SRCDIR}/video/uvc.cpp)
=======
  list(APPEND HEADERS ${INCDIR}/video/drivers/uvc.h )
  list(APPEND SOURCES video/drivers/uvc.cpp)
  if(_WIN_)
    find_package(pthread REQUIRED QUIET)
    list(APPEND LINK_LIBS ${pthread_LIBRARIES} )

    find_package(libusb1 REQUIRED QUIET)
    list(APPEND LINK_LIBS ${libusb1_LIBRARIES} )
  endif()
>>>>>>> stevenlovegrove/master
  message(STATUS "libuvc Found and Enabled")
endif()

find_package(DepthSense QUIET)
if(BUILD_PANGOLIN_VIDEO AND DepthSense_FOUND)
  set(HAVE_DEPTHSENSE 1)
  list(APPEND INTERNAL_INC  ${DepthSense_INCLUDE_DIRS} )
  list(APPEND LINK_LIBS ${DepthSense_LIBRARIES} )
<<<<<<< HEAD
  list(APPEND HEADERS ${INCDIR}/video/depthsense.h )
  list(APPEND SOURCES ${SRCDIR}/video/depthsense.cpp)
=======
  list(APPEND HEADERS ${INCDIR}/video/drivers/depthsense.h )
  list(APPEND SOURCES video/drivers/depthsense.cpp)
>>>>>>> stevenlovegrove/master
  message(STATUS "DepthSense Found and Enabled")
endif()

find_package(TeliCam QUIET)
if(BUILD_PANGOLIN_VIDEO AND TeliCam_FOUND)
  set(HAVE_TELICAM 1)
  list(APPEND INTERNAL_INC ${TeliCam_INCLUDE_DIRS} )
  list(APPEND LINK_LIBS ${TeliCam_LIBRARIES} )
  list(APPEND HEADERS ${INCDIR}/video/drivers/teli.h )
  list(APPEND SOURCES video/drivers/teli.cpp )
  message(STATUS "TeliCam Found and Enabled" )
endif()

find_package(Pleora QUIET)
if(BUILD_PANGOLIN_VIDEO AND Pleora_FOUND)
  set(HAVE_PLEORA 1)
  list(APPEND INTERNAL_INC ${Pleora_INCLUDE_DIRS} )
  list(APPEND LINK_LIBS ${Pleora_LIBRARIES} )
  list(APPEND HEADERS ${INCDIR}/video/drivers/pleora.h )
  list(APPEND SOURCES video/drivers/pleora.cpp )
  if(_GCC_)
    # Suppress warnings generated from Pleora SDK.
    set_source_files_properties(video/drivers/pleora.cpp PROPERTIES COMPILE_FLAGS -Wno-unknown-pragmas)
    set_source_files_properties(video/video.cpp PROPERTIES COMPILE_FLAGS -Wno-unknown-pragmas)
  endif()
  message(STATUS "Pleora Found and Enabled" )
endif()

if(NOT BUILD_EXTERN_LIBPNG)
  find_package(PNG QUIET)
endif()
if(PNG_FOUND)
  # (ZLIB is also found by FindPNG.cmake as its dependency)
  set(HAVE_PNG 1)
  list(APPEND INTERNAL_INC ${PNG_INCLUDE_DIR} )
  list(APPEND LINK_LIBS ${PNG_LIBRARY} ${ZLIB_LIBRARY} )
  message(STATUS "libpng Found and Enabled")
endif()

if(NOT BUILD_EXTERN_LIBJPEG)
  find_package(JPEG QUIET)
endif()
if(JPEG_FOUND)
  set(HAVE_JPEG 1)
  list(APPEND INTERNAL_INC ${JPEG_INCLUDE_DIR} )
  list(APPEND LINK_LIBS ${JPEG_LIBRARY} )
  message(STATUS "libjpeg Found and Enabled")
endif()

find_package(TIFF QUIET)
if(TIFF_FOUND)
  set(HAVE_TIFF 1)
  list(APPEND INTERNAL_INC ${TIFF_INCLUDE_DIR} )
  list(APPEND LINK_LIBS ${TIFF_LIBRARY} )
  message(STATUS "libtiff Found and Enabled")
endif()

find_package(OpenEXR QUIET)
if(OpenEXR_FOUND)
  set(HAVE_OPENEXR 1)
  list(APPEND INTERNAL_INC ${OpenEXR_INCLUDE_DIR} )
  list(APPEND LINK_LIBS ${OpenEXR_LIBRARY} )
  message(STATUS "libopenexr Found and Enabled")
endif()


#######################################################
## Embed resource binary files

include(EmbedBinaryFiles)

if(BUILD_PANGOLIN_GUI)
    embed_binary_files( "_embed_/fonts/*.ttf" "${CMAKE_CURRENT_BINARY_DIR}/fonts.c" )
    list(APPEND SOURCES "${CMAKE_CURRENT_BINARY_DIR}/fonts.c" )
endif()

#######################################################
## Create config.h file for inclusion in library

configure_file(
  "config.h.in"
  "${CMAKE_CURRENT_BINARY_DIR}/../include/${LIBRARY_NAME}/PangolinConfig.h"
)

#######################################################

set( REQUIRED_INCLUDE_DIRS "${INTERNAL_INC} ${USER_INC}" CACHE INTERNAL "REQUIRED_INCLUDE_DIRS" )
set( REQUIRED_LIBRARIES "${LINK_LIBS}" CACHE INTERNAL "REQUIRED_LIBRARIES" )
set( PANGOLIN_SRCS "${SOURCES}" CACHE INTERNAL "PANGOLIN_SRCS" )
set( PANGOLIN_HDRS "${HEADERS}" CACHE INTERNAL "PANGOLINE_HDRS" )

