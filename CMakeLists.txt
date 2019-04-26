cmake_minimum_required (VERSION 2.6)
project (Tutorial)
# The version number.
set (Tutorial_VERSION_MAJOR 1)
set (Tutorial_VERSION_MINOR 0)

set (CMAKE_INSTALL_PREFIX ${PROJECT_BINARY_DIR})

# configure a header file to pass some of the CMake setting
# to the source code
configure_file (
	"${PROJECT_SOURCE_DIR}/TutorialConfig.h.in"
	"${PROJECT_BINARY_DIR}/TutorialConfig.h"
)

# should we use our own math functions?
option (USE_MYMATH 
        "Use tutorial provided math implementation" ON) 

# add the binary tree to the search path for include files
# so that well find TutorialConfig.h
include_directories("${PROJECT_BINARY_DIR}")

if (USE_MYMATH)
	include_directories("${PROJECT_SOURCE_DIR}/MathFunctions")
	add_subdirectory("${PROJECT_SOURCE_DIR}/MathFunctions")
	set (EXTRA_LIBS ${EXTRA_LIBS} MathFunctions)
endif (USE_MYMATH)


#add the exectutable
add_executable(Tutorial tutorial.cxx)
target_link_libraries(Tutorial ${EXTRA_LIBS})

