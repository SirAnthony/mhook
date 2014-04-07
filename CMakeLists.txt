cmake_minimum_required(VERSION 2.8)
project(mhook)

option(MHOOK_TESTS "Build mhook tests" OFF)
add_definitions(-DUNICODE -D_UNICODE)

set(COMPILER_DEPENDENT_LIBS "")
if(NOT MSVC)
	# Suppress warnings.
	set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wno-pointer-to-int-cast")
	set(COMPILER_DEPENDENT_LIBS ws2_32)
endif()

include_directories("${CMAKE_SOURCE_DIR}")

set(SRC
	disasm-lib/cpu.c
	disasm-lib/disasm.c
	disasm-lib/disasm_x86.c
	disasm-lib/misc.c
	mhook-lib/mhook.cpp
)

# Static lib for linking
add_library(mhook STATIC ${SRC})

# Tests
if(MHOOK_TESTS)	
	set(TESTS_SRC tests/mhook-test.cpp tests/stdafx.cpp)
	add_executable(mhook-tests ${TESTS_SRC})
	target_link_libraries(mhook-tests mhook ${COMPILER_DEPENDENT_LIBS})
endif()