cmake_minimum_required(VERSION 3.21)
project(SlintUiTest LANGUAGES CXX)

SET(SLINT_FEATURE_BACKEND_QT OFF)

#Set CMake variables to disable rpath

#set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(CMAKE_BUILD_WITH_INSTALL_RPATH TRUE) 
set(CMAKE_INSTALL_RPATH_USE_LINK_PATH FALSE)
SET(CMAKE_INSTALL_RPATH "$ORIGIN/../lib:$ORIGIN/")

include(FetchContent)
FetchContent_Declare(
    Slint
    GIT_REPOSITORY https://github.com/slint-ui/slint.git
    # `release/1` will auto-upgrade to the latest Slint >= 1.0.0 and < 2.0.0
    # `release/1.0` will auto-upgrade to the latest Slint >= 1.0.0 and < 1.1.0
    GIT_TAG release/1
    SOURCE_SUBDIR api/cpp
)
FetchContent_MakeAvailable(Slint)

SET_TARGET_PROPERTIES(Slint PROPERTIES NO_SONAME 1)

SET (MAINFOLDER ${PROJECT_SOURCE_DIR})

IF("${TARGET}" STREQUAL "")
   message(WARNING "TARGET not set please add -DTRAGET to command line Suported Target are Linux, Windows, PI (crosscompile)")
   SET(TARGET ${CMAKE_SYSTEM_NAME})
   message(STATUS "TRAGET is set to ${TARGET}")
ENDIF()

SET (EXECUTABLE_OUTPUT_PATH "${MAINFOLDER}/bin/${TARGET}")
SET (LIBRARY_OUTPUT_PATH "${MAINFOLDER}/lib/${TARGET}")

ADD_SUBDIRECTORY(src)