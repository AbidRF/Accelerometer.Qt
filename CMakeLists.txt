
cmake_minimum_required(VERSION 3.16)

project(AccelerometerVisualizer VERSION 0.1 LANGUAGES CXX)

set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(Qt6 6.2 REQUIRED COMPONENTS Quick)
find_package(Qt6 6.2 REQUIRED COMPONENTS QuickControls2)
find_package(Qt6 6.2 REQUIRED COMPONENTS Quick3D)
find_package(Qt6 6.2 REQUIRED COMPONENTS SerialPort)

qt_add_executable(appAccelerometerVisualizer
    main.cpp
    serialmanager.cpp
    serialmanager.h
    resources.qrc
)

qt_add_qml_module(appAccelerometerVisualizer
    URI AccelerometerVisualizer
    VERSION 1.0
    QML_FILES Main.qml
    SOURCES serialmanager.h serialmanager.cpp
    RESOURCES resources.qrc
)

# Qt for iOS sets MACOSX_BUNDLE_GUI_IDENTIFIER automatically since Qt 6.1.
# If you are developing for iOS or macOS you should consider setting an
# explicit, fixed bundle identifier manually though.
set_target_properties(appAccelerometerVisualizer PROPERTIES
#    MACOSX_BUNDLE_GUI_IDENTIFIER com.example.appAccelerometerVisualizer
    MACOSX_BUNDLE_BUNDLE_VERSION ${PROJECT_VERSION}
    MACOSX_BUNDLE_SHORT_VERSION_STRING ${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}
    MACOSX_BUNDLE TRUE
    WIN32_EXECUTABLE TRUE
)

target_link_libraries(appAccelerometerVisualizer
    PRIVATE Qt6::Quick
    PRIVATE Qt6::QuickControls2
    PRIVATE Qt6::Quick3D
    PRIVATE Qt6::SerialPort
)

include(GNUInstallDirs)
install(TARGETS appAccelerometerVisualizer
    BUNDLE DESTINATION .
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)
