cmake_minimum_required(VERSION 3.8)
set(CMAKE_CXX_STANDARD 11)

project(QtSolutions_MFCMigrationFramework)

set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTORCC ON)

get_filename_component(OUTPUT_DIR "install" ABSOLUTE BASE_DIR ${CMAKE_BINARY_DIR})
file(MAKE_DIRECTORY ${OUTPUT_DIR})

find_package(Qt5Core    5 REQUIRED)
find_package(Qt5Gui     5 REQUIRED)
find_package(Qt5Widgets 5 REQUIRED)

add_definitions(-DQT_QTWINMIGRATE_EXPORT)

include_directories(
    ${Qt5Gui_PRIVATE_INCLUDE_DIRS}
    ${CMAKE_CURRENT_SOURCE_DIR}/src
)

set(SRC_LIST_C
    "src/qmfcapp.cpp"
    "src/qwinhost.cpp"
    "src/qwinwidget.cpp"
)

set(SRC_LIST_H
    "src/qmfcapp.h"
    "src/qwinhost.h"
    "src/qwinwidget.h"
)

add_library(${PROJECT_NAME}
    SHARED
    ${SRC_LIST_C}
    ${SRC_LIST_H}
)

target_link_libraries(${PROJECT_NAME}
    Qt5::Core
    Qt5::Gui
    Qt5::Widgets
    user32
)

set_target_properties(${PROJECT_NAME} PROPERTIES DEBUG_POSTFIX "d")
set_target_properties(${PROJECT_NAME} PROPERTIES RUNTIME_OUTPUT_DIRECTORY_DEBUG ${OUTPUT_DIR})
set_target_properties(${PROJECT_NAME} PROPERTIES RUNTIME_OUTPUT_DIRECTORY_RELEASE ${OUTPUT_DIR})
set_target_properties(${PROJECT_NAME} PROPERTIES LIBRARY_OUTPUT_DIRECTORY_DEBUG ${OUTPUT_DIR})
set_target_properties(${PROJECT_NAME} PROPERTIES LIBRARY_OUTPUT_DIRECTORY_RELEASE ${OUTPUT_DIR})
