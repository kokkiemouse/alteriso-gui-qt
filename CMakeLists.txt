cmake_minimum_required(VERSION 3.5)

project(alteriso-gui-qt LANGUAGES CXX)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# QtCreator supports the following variables for Android, which are identical to qmake Android variables.
# Check http://doc.qt.io/qt-5/deployment-android.html for more information.
# They need to be set before the find_package(Qt5 ...) call.

#if(ANDROID)
#    set(ANDROID_PACKAGE_SOURCE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/android")
#    if (ANDROID_ABI STREQUAL "armeabi-v7a")
#        set(ANDROID_EXTRA_LIBS
#            ${CMAKE_CURRENT_SOURCE_DIR}/path/to/libcrypto.so
#            ${CMAKE_CURRENT_SOURCE_DIR}/path/to/libssl.so)
#    endif()
#endif()

find_package(Qt5 COMPONENTS Widgets REQUIRED)
find_package(Threads)

if(ANDROID)
  add_library(alteriso-gui-qt SHARED
    main.cpp
    mainwindow.cpp
    mainwindow.h
    mainwindow.ui
    main_mainwindow_interface.h
    main_mainwindow_interface.cpp
    build_setting.cpp
    build_setting.h
    log_manager.h
    log_manager.cpp
    ${TS_FILES}
  )
else()
  add_executable(alteriso-gui-qt
    main.cpp
    mainwindow.cpp
    mainwindow.h
    mainwindow.ui
    main_mainwindow_interface.h
    main_mainwindow_interface.cpp
    main.cpp
    build_setting.cpp
    build_setting.h
    log_manager.h
    log_manager.cpp
    ${TS_FILES}
  )
endif()

target_link_libraries(alteriso-gui-qt PRIVATE Qt5::Widgets ${CMAKE_THREAD_LIBS_INIT} )
