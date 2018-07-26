# add the source files 
file(GLOB SRCS *.c)
add_library(miracl ${SRCS})

# Files need to be compiled as CXX
set_source_files_properties(${SRCS} PROPERTIES LANGUAGE CXX)

if(CMAKE_COMPILER_IS_GNUCXX)
    set(CMAKE_C_FLAGS "-c -m64")
endif(CMAKE_COMPILER_IS_GNUCXX)
if(MSVC)
	ADD_DEFINITIONS(-D_WIN32_WINNT=0x0601)
	ADD_DEFINITIONS(/MT)
endif(MSVC)

# Set a default build type for single-configuration
# CMake generators if no build type is set.
if(NOT CMAKE_CONFIGURATION_TYPES AND NOT CMAKE_BUILD_TYPE)
   SET(CMAKE_BUILD_TYPE Release)
endif()

# Select flags.
if(CMAKE_COMPILER_IS_GNUCXX)
	SET(CMAKE_CXX_FLAGS_RELEASE "-O3 -DNDEBUG") 	
	SET(CMAKE_CXX_FLAGS_RELWITHDEBINFO " -O2 -g -ggdb -rdynamic")
	SET(CMAKE_CXX_FLAGS_DEBUG  "-O0 -g -ggdb -rdynamic")
endif(CMAKE_COMPILER_IS_GNUCXX)
if(MSVC)
	SET(CMAKE_CXX_FLAGS_RELEASE "-O2") 	
	SET(CMAKE_CXX_FLAGS_RELWITHDEBINFO " -O2 -Zi")
	SET(CMAKE_CXX_FLAGS_DEBUG  "-Od -Zi")
endif(MSVC)

target_include_directories(miracl PUBLIC ../include)
