project(torrent-file-editor)
cmake_minimum_required(VERSION 2.8.11)
include_directories(${CMAKE_SOURCE_DIR} ${CMAKE_BINARY_DIR})
find_package(Qt4 REQUIRED)
find_package(QJSON REQUIRED)

include(${QT_USE_FILE})

configure_file(translations.qrc.in translations.qrc COPYONLY)

set(TRANSLATIONS
  ${CMAKE_SOURCE_DIR}/translations/torrentfileeditor_en.ts
  ${CMAKE_SOURCE_DIR}/translations/torrentfileeditor_ru.ts)

set(HEADERS
  ${CMAKE_SOURCE_DIR}/mainwindow.h
  ${CMAKE_SOURCE_DIR}/bencode.h
  ${CMAKE_SOURCE_DIR}/datewidget.h
  ${CMAKE_SOURCE_DIR}/lineeditwidget.h
  ${CMAKE_SOURCE_DIR}/urledit.h
  ${CMAKE_SOURCE_DIR}/folderedit.h
  ${CMAKE_SOURCE_DIR}/aboutdlg.h)

set(FORMS 
  ${CMAKE_SOURCE_DIR}/mainwindow.ui
  ${CMAKE_SOURCE_DIR}/aboutdlg.ui)

set(SOURCES
  ${CMAKE_SOURCE_DIR}/main.cpp
  ${CMAKE_SOURCE_DIR}/mainwindow.cpp
  ${CMAKE_SOURCE_DIR}/bencode.cpp
  ${CMAKE_SOURCE_DIR}/datewidget.cpp
  ${CMAKE_SOURCE_DIR}/lineeditwidget.cpp
  ${CMAKE_SOURCE_DIR}/urledit.cpp
  ${CMAKE_SOURCE_DIR}/folderedit.cpp
  ${CMAKE_SOURCE_DIR}/aboutdlg.cpp)

set(RESOURCES
  ${CMAKE_BINARY_DIR}/translations.qrc
  resources.qrc)

QT4_ADD_TRANSLATION(QM ${TRANSLATIONS})

qt4_add_resources(QRC_SOURCES ${RESOURCES})
qt4_wrap_cpp(MOC_SOURCES ${HEADERS})
qt4_wrap_ui(UI_SOURCES ${FORMS})

add_executable(${PROJECT_NAME} WIN32 ${QM} ${HEADERS} ${SOURCES} ${MOC_SOURCES} ${QRC_SOURCES} ${UI_SOURCES})
target_link_libraries(${PROJECT_NAME} ${QT_LIBRARIES} ${QJSON_LIBRARIES})

add_subdirectory(translations)