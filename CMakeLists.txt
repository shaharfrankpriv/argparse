cmake_minimum_required(VERSION 3.0)

project(argparse VERSION 0.1.0 LANGUAGES C)

if(NOT CMAKE_C_FLAGS)
	set(CMAKE_C_FLAGS "-O3")
endif()
if(NOT CMAKE_C_FLAGS_DEBUG)
	set(CMAKE_C_FLAGS_DEBUG "-g -ggdb")
endif()

set(sources argparse.c)

#set(lib_dest "lib")
#set(include_dest "include")

option(ARGPARSE_SHARED "Build shared library" ON)
option(ARGPARSE_STATIC "Build static library" ON)

if(ARGPARSE_SHARED)
	add_library(argparse_shared SHARED ${sources})
	target_include_directories(argparse_shared PUBLIC .)
	set_target_properties(argparse_shared PROPERTIES OUTPUT_NAME argparse)
	set_target_properties(argparse_shared PROPERTIES PUBLIC_HEADER argparse.h)
	install(TARGETS argparse_shared)
endif()

if(ARGPARSE_STATIC)
	add_library(argparse STATIC ${sources})
	target_include_directories(argparse PUBLIC .)
	set_target_properties(argparse PROPERTIES PUBLIC_HEADER argparse.h)
	install(TARGETS argparse)
endif()

if(NOT (ARGPARSE_STATIC OR ARGPARSE_SHARED))
	add_library(argparse OBJECT ${sources})
	install(TARGETS argparse)
endif()


