
project(external)

option(LSPLT_BUILD_SHARED "Build LSPLT shared library" OFF)
option(USEASAN "Use Address Sanitizer" ON)

add_subdirectory(lsplt/lsplt/src/main/jni)

set(XDL_SOURCE_FILES
    _xDL/xdl/src/main/cpp/xdl.c
    _xDL/xdl/src/main/cpp/xdl_iterate.c
    _xDL/xdl/src/main/cpp/xdl_linker.c
    _xDL/xdl/src/main/cpp/xdl_lzma.c
    _xDL/xdl/src/main/cpp/xdl_util.c
)

add_library(phmap INTERFACE)
target_include_directories(phmap INTERFACE parallel-hashmap)
target_compile_options(phmap INTERFACE -Wno-unused-value)

add_library(xdl STATIC ${XDL_SOURCE_FILES})
target_include_directories(xdl PUBLIC _xDL/xdl/src/main/cpp/include)
