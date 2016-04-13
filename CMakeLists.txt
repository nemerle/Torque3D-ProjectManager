project(TorqueProjectManager)
CMAKE_MINIMUM_REQUIRED(VERSION 3.1)
CMAKE_POLICY(SET CMP0020 OLD)
IF(POLICY CMP0043)
    CMAKE_POLICY(SET CMP0043 OLD)
ENDIF()


###############################################################################
# Compiler specific flags section
###############################################################################
IF(CMAKE_CXX_COMPILER MATCHES cl.exe)
    #message(SEND_ERROR "This is a c++11 build it's highly likely it will fail under VisualStudio")
    ADD_DEFINITIONS(-D_CRT_SECURE_NO_WARNINGS -D_CRT_NONSTDC_NO_DEPRECATE -D_SCL_SECURE_NO_WARNINGS)
ELSE()
    SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wextra -std=c++11 -pedantic" )
    SET(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -Wextra" )
    add_definitions(-D__STDC_FORMAT_MACROS) #-D_GLIBCXX_DEBUG
ENDIF()

find_package(Qt5Core)
find_package(Qt5Widgets)
find_package(Qt5Xml)
find_package(Qt5Network)

set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_AUTOUIC ON)
set(CMAKE_INCLUDE_CURRENT_DIR ON)

set(HEADERS
           source/copyDir.h
           source/moduleList.h
           source/moduleListInstance.h
           source/NewProjectPage.h
           source/PlatformCheck.h
           source/ProgressDialog.h
           source/ProgressFinishedDialog.h
           source/projectList.h
           source/projectModuleList.h
           source/ProjectModuleListPage.h
           source/ProjectTree.h
           source/ProjectTreeItem.h
           source/torque3dfrontloader.h)
set(FORMS
         source/NewProjectPage.ui
         source/ProgressDialog.ui
         source/ProgressFinishedDialog.ui
         source/ProjectTreeItem.ui
         source/ProjectModuleList.ui
         source/torque3dfrontloader.ui
)
set(SOURCES
           source/copyDir.cpp
           source/main.cpp
           source/moduleList.cpp
           source/moduleListInstance.cpp
           source/NewProjectPage.cpp
           source/PlatformCheck.cpp
           source/ProgressDialog.cpp
           source/ProgressFinishedDialog.cpp
           source/projectList.cpp
           source/projectModuleList.cpp
           source/ProjectModuleListPage.cpp
           source/ProjectTree.cpp
           source/ProjectTreeItem.cpp
           source/torque3dfrontloader.cpp
)
set(RESOURCES  source/torque3dfrontloader.qrc)

include_directories(source)

add_executable(projectmanager ${RESOURCES} ${FORMS} ${SOURCES} ${HEADERS})
qt5_use_modules(projectmanager Core Widgets Network Xml)
