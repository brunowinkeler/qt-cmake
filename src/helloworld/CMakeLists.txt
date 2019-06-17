# Set of Local Variables for location
set(MODULE_HELLO helloworld)
set(MODULE_HELLO_SRCS ${PROJECT_SOURCE_DIR}/src/${MODULE_HELLO})

# Include the directories that are the reference
include_directories(${MODULE_HELLO_SRCS}/include)
#include_directories(${MODULE_HELLO_SRCS}/ui_templates)

# Collect sources and headers into the variables
file(GLOB MODULE_HEADERS 
        "${MODULE_HELLO_SRCS}/src/*.h"
        "${MODULE_HELLO_SRCS}/src/*.hpp"
        "${MODULE_HELLO_SRCS}/src/*.hxx")
file(GLOB MODULE_SOURCES
        "${MODULE_HELLO_SRCS}/src/*.c"
        "${MODULE_HELLO_SRCS}/src/*.cpp"
        "${MODULE_HELLO_SRCS}/src/*.cxx")
file(GLOB MODULE_UIS
        "${MODULE_HELLO_SRCS}/ui_templates/*.ui")

qt5_wrap_ui(MODULE_GENERATED_UIS ${MODULE_UIS})

# Tell CMake to create the helloworld executable
add_executable(${EXEC_NAME} ${MODULE_HEADERS} ${MODULE_SOURCES} ${MODULE_GENERATED_UIS})

# Add the Qt5 Widgets for linking
target_link_libraries(${EXEC_NAME} Qt5::Widgets)