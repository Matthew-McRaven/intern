cmake_minimum_required(VERSION 3.10)

project (Intern)

set (INTERN_LIB_NAME intern)

set (PAGE_SIZE 4096 CACHE STRING "Page size for allocations")
option (MMAP_PAGES "Allocate pages with mmap(2)" OFF)
option (INLINE_UNSIGNED "Inline unsigned integers into the ID" OFF)

configure_file (config.h.in intern_config.h)
include_directories (${CMAKE_CURRENT_BINARY_DIR})


set (INTERN_SRC strings.c block.c optimize.c)
set (INTERN_HEADERS strings.h block.h optimize.h)

add_library (intern STATIC ${INTERN_SRC})
# Add current dir as include directory for intern library.
target_include_directories (intern PUBLIC ${CMAKE_CURRENT_SOURCE_DIR} ${CMAKE_CURRENT_BINARY_DIR})

set (CMAKE_C_FLAGS "-std=c99 -Wall -pedantic -g -D_GNU_SOURCE")
set (CMAKE_C_FLAGS_RELEASE "-O3 -march=native")
