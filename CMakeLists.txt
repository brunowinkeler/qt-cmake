cmake_minimum_required(VERSION 3.5.1)

project(helloworld)

# Find includes in the build directories
set(CMAKE_INCLUDE_CURRENT_DIR ON)

# Turn on automatic invocation of the MOC & UIC
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)
#set (CMAKE_PREFIX_PATH "C:\\Qt\\Qt5.10.1\\5.10.1\\msvc2017_64\\lib\\cmake")

# Add a compiler flag
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall")

# Make this a GUI application on Windows
if(WIN32)
  set(CMAKE_WIN32_EXECUTABLE ON)
endif()

# Find the QtWidgets library
find_package(Qt5 REQUIRED COMPONENTS Widgets)

# Generate rules for building source files from the resources
#qt5_add_resources(QRCS resources.qrc)

# Tell CMake to create the helloworld executable
add_executable(helloworld mainwindow.h main.cpp mainwindow.cpp mainwindow.ui)

# Add the Qt5 Widgets for linking
target_link_libraries(helloworld Qt5::Widgets)