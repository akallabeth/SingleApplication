set(QAPPLICATION_CLASS QApplication CACHE STRING "Inheritance class for SingleApplication")
find_package(Qt5 COMPONENTS Widgets REQUIRED)

add_executable(calculator
	button.h
	calculator.h
	button.cpp
	calculator.cpp
	main.cpp
	)

target_link_libraries(calculator ${PROJECT_NAME} Qt5::Widgets)
