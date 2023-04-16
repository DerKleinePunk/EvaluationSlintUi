cmake_minimum_required(VERSION 3.21)
project(memory LANGUAGES CXX)

SET(SLINT_FEATURE_BACKEND_QT=OFF)

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

SET (MAINFOLDER ${PROJECT_SOURCE_DIR})

IF("${TARGET}" STREQUAL "")
   message(WARNING "TARGET not set please add -DTRAGET to command line Suported Target are Linux, Windows, PI (crosscompile)")
   SET(TARGET ${CMAKE_SYSTEM_NAME})
   message(STATUS "TRAGET is set to ${TARGET}")
ENDIF()

SET (EXECUTABLE_OUTPUT_PATH "${MAINFOLDER}/bin/${TARGET}")
SET (LIBRARY_OUTPUT_PATH "${MAINFOLDER}/lib/${TARGET}")

ADD_SUBDIRECTORY(src)