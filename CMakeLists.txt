cmake_minimum_required(VERSION 3.16)
project(svgviewer LANGUAGES CXX)

set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTORCC ON)

find_package(Qt6 REQUIRED COMPONENTS Core Gui Svg SvgWidgets Widgets)

add_executable(${PROJECT_NAME} src/main.cpp
    src/exportdialog.cpp include/exportdialog.h
    src/mainwindow.cpp include/mainwindow.h
    src/svgview.cpp include/svgview.h
    res/bubbles.qrc res/cubic.qrc res/spheres.qrc)
target_include_directories(${PROJECT_NAME} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)

set_target_properties(${PROJECT_NAME} PROPERTIES
    WIN32_EXECUTABLE FALSE
    MACOSX_BUNDLE TRUE)

target_link_libraries(${PROJECT_NAME} PUBLIC
    Qt::Core
    Qt::Gui
    Qt::Svg
    Qt::SvgWidgets
    Qt::Widgets)

if (TARGET Qt::OpenGL AND TARGET Qt::OpenGLWidgets)
    target_compile_definitions(${PROJECT_NAME} PUBLIC USE_OPENGLWIDGETS)
    target_link_libraries(${PROJECT_NAME} PUBLIC Qt::OpenGL Qt::OpenGLWidgets)
endif()

