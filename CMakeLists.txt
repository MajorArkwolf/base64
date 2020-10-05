project(base64)
add_library(base64 STATIC)
target_sources(base64 PRIVATE
    base64/lib/arch/avx2/codec.c
    base64/lib/arch/generic/codec.c
    base64/lib/arch/neon32/codec.c
    base64/lib/arch/neon64/codec.c
    base64/lib/arch/ssse3/codec.c
    base64/lib/arch/sse41/codec.c
    base64/lib/arch/sse42/codec.c
    base64/lib/arch/avx/codec.c
    base64/lib/lib.c
    base64/lib/codec_choose.c
    base64/lib/tables/tables.c
)
target_include_directories(base64 PUBLIC base64)
target_compile_options(base64 PRIVATE
    $<$<CXX_COMPILER_ID:MSVC>:/arch:AVX2>
    $<$<OR:$<CXX_COMPILER_ID:Clang>,$<CXX_COMPILER_ID:AppleClang>,$<CXX_COMPILER_ID:GNU>>:-mavx2>
)
