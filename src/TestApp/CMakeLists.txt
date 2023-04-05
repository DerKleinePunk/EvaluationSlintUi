project("SlintUiTestApp"  LANGUAGES CXX)

MESSAGE(STATUS "Try Build ${PROJECT_NAME}")

## Use all the *.cpp files we found under this folder for the project Find better way for coomen cpp files
FILE(GLOB SRCS "*.cpp" "*/*.cpp")

if(${CMAKE_SYSTEM_NAME} STREQUAL "Windows" )
    SET (project_BIN ${PROJECT_NAME})
else()
    SET (project_BIN ${PROJECT_NAME}.bin)
endif()

add_executable(${project_BIN} ${SRCS})

target_link_libraries(${project_BIN} PRIVATE Slint::Slint)
slint_target_sources(${project_BIN} ../ui/mainWindow.slint)

# On Windows, copy the Slint DLL next to the application binary so that it's found.
if (WIN32)
    add_custom_command(TARGET ${project_BIN} POST_BUILD COMMAND ${CMAKE_COMMAND} -E copy $<TARGET_RUNTIME_DLLS:${project_BIN}> $<TARGET_FILE_DIR:${project_BIN}> COMMAND_EXPAND_LISTS)
endif()