set(QAPPLICATION_CLASS QCoreApplication CACHE STRING "Inheritance class for SingleApplication")
find_package(Qt5 COMPONENTS Core REQUIRED)

include_directories(${Qt5_INCLUDE_DIRS})
add_definitions(${Qt5_DEFINITIONS})

add_executable(basic
	main.cpp
	)

target_link_libraries(basic ${PROJECT_NAME} Qt5::Core)
