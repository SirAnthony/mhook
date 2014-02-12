cmake_minimum_required(VERSION 2.8)

add_definitions(-DUNICODE -D_UNICODE)

set(SRC
	disasm-lib/cpu.c
	disasm-lib/disasm.c
	disasm-lib/disasm_x86.c
	disasm-lib/misc.c
	mhook-lib/mhook.cpp
)

set(TESTS_SRC
	mhook-test.cpp
	stdafx.cpp
)    

# Static lib for linking
add_library(mhook STATIC ${SRC})

# Tests
add_executable(mhook-tests ${TESTS_SRC})
target_link_libraries(mhook-tests mhook)