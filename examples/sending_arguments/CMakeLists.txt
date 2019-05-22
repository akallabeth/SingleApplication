set(QAPPLICATION_CLASS QCoreApplication CACHE STRING "Inheritance class for SingleApplication")
find_package(Qt5 COMPONENTS Core REQUIRED)

include_directories(${Qt5_INCLUDE_DIRS})
add_definitions(${Qt5_DEFINITIONS})

add_executable(sending_arguments
	main.cpp
	messagereceiver.cpp
	messagereceiver.h
	main.cpp
	)

target_link_libraries(sending_arguments ${PROJECT_NAME} Qt5::Core)
