cmake_minimum_required(VERSION 2.8.12)

if (${CMAKE_CXX_COMPILER_ID} STREQUAL "GNU")
    set (ALIGN_LOOP "-falign-loops=32")
endif()

set(REL_OPTIONS "-O3 ${ALIGN_LOOP} -Wall -Wextra -Wcast-qual 
                         -Wcast-align -Wshadow -Wstrict-aliasing=1 
                         -Wswitch-enum -Wstrict-prototypes -Wundef")

set(FSE_SRC
    bitstream.h
    error_private.h
    error_public.h
    fse.h
    fseU16.h
    huf.h
    mem.h
    entropy_common.c
    fseU16.c
    fse_compress.c
    fse_decompress.c
    huf_compress.c
    huf_decompress.c
)

add_library(fse SHARED ${FSE_SRC})

target_compile_options(fse PRIVATE "$<$<CONFIG:RELEASE>:${REL_OPTIONS}>")
target_compile_options(fse PRIVATE "$<$<CONFIG:RELWITHDEBINFO>:${REL_OPTIONS}>")


