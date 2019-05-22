cmake_minimum_required(VERSION 3.4)

project(SingleApplication)

set(CMAKE_INCLUDE_CURRENT_DIR ON)
# Instruct CMake to run moc automatically when needed
set(CMAKE_AUTOMOC ON)
# Create code from a list of Qt designer ui files
set(CMAKE_AUTOUIC ON)

set(QAPPLICATION_CLASS QCoreApplication CACHE STRING "Inheritance class for SingleApplication")
set_property(CACHE QAPPLICATION_CLASS PROPERTY STRINGS QApplication QGuiApplication QCoreApplication)

option(WITH_EXAMPLES "Build usage examples" ON)

if (WITH_EXAMPLES)
    add_subdirectory(examples)
endif (WITH_EXAMPLES)

set(QT5_COMPONENTS Network)
find_package(Qt5 COMPONENTS Network REQUIRED)
if(QAPPLICATION_CLASS STREQUAL QApplication)
    list(APPEND QT5_COMPONENTS Widgets)
elseif(QAPPLICATION_CLASS STREQUAL QGuiApplication)
    list(APPEND QT5_COMPONENTS Gui)
else()
    list(APPEND QT5_COMPONENTS Core)
endif()

find_package(Qt5 COMPONENTS ${QT5_COMPONENTS} REQUIRED)
find_package(Qt5LinguistTools REQUIRED)

include_directories(${Qt5_INCLUDE_DIRS})
add_definitions(${Qt5_DEFINITIONS})
add_compile_definitions(QAPPLICATION_CLASS=${QAPPLICATION_CLASS})

add_library(${PROJECT_NAME} STATIC
    singleapplication.cpp
    singleapplication_p.cpp
    )

target_link_libraries(${PROJECT_NAME} PRIVATE Qt5::Network)
if(QAPPLICATION_CLASS STREQUAL QApplication)
    target_link_libraries(${PROJECT_NAME} PRIVATE Qt5::Widgets)
elseif(QAPPLICATION_CLASS STREQUAL QGuiApplication)
    target_link_libraries(${PROJECT_NAME} PRIVATE Qt5::Gui)
else()
    target_link_libraries(${PROJECT_NAME} PRIVATE Qt5::Core)
endif()

if(WIN32)
    target_link_libraries(${PROJECT_NAME} PRIVATE advapi32)
endif()

target_include_directories(${PROJECT_NAME} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
