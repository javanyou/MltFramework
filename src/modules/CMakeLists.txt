
add_compile_options(-DUSE_SSE -DUSE_SSE2 -O2)
if (!WIN32)
    add_compile_options(-DUSE_MMX)
endif ()

add_subdirectory(avformat)
add_subdirectory(core)
add_subdirectory(sdl2)