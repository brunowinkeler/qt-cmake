cmake_minimum_required(VERSION 3.5)

set(PROJ_NAME helloworld)
set(EXEC_NAME HelloWorld)

project(${PROJ_NAME})
set(CMAKE_INSTALL_PREFIX "${PROJECT_SOURCE_DIR}/install" CACHE PATH "Default Install Path" FORCE)

if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Release CACHE STRING "Choose the type of build, options are: None Debug Release RelWithDebInfoMinSizeRel." FORCE)
endif()

# Add to path folder containing Find<package>.cmake files
list(APPEND CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake")

# Find includes in the build directories
set(CMAKE_INCLUDE_CURRENT_DIR ON)

# Turn on automatic invocation of the MOC & UIC
set(CMAKE_AUTOMOC ON)
# set(CMAKE_AUTOUIC ON)
# set (CMAKE_PREFIX_PATH "C:\\Qt\\Qt5.10.1\\5.10.1\\msvc2017_64\\lib\\cmake")

# Make this a GUI application on Windows
if(WIN32)
  set(CMAKE_WIN32_EXECUTABLE ON)
  set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS 1)
endif()

# Check if compiler is MSVC or GNU
if(${CMAKE_CXX_COMPILER_ID} STREQUAL "MSVC")
    message(STATUS "Setting MSVC flags")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /EHc /MP")
elseif(${CMAKE_CXX_COMPILER_ID} STREQUAL "GNU")
    message(STATUS "Setting GNU flags")
    set (CMAKE_CXX_STANDARD 11)
    # Executables fail to build with Qt 5 in the default configuration
    # without -fPIE. We add that here.
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -pthread -Wall ${Qt5Widgets_EXECUTABLE_COMPILE_FLAGS}")
endif()

# Find the QtWidgets library
#find_package(Qt5Widgets)
find_package(Qt5 REQUIRED COMPONENTS Widgets)
# The Qt5Widgets_INCLUDES also includes the include directories for
# dependencies QtCore and QtGui
include_directories(${Qt5Widgets_INCLUDES})
# We need add -DQT_WIDGETS_LIB when using QtWidgets in Qt 5.
add_definitions(${Qt5Widgets_DEFINITIONS})

# Generate rules for building source files from the resources
#qt5_add_resources(QRCS resources.qrc)

add_subdirectory(src/helloworld)