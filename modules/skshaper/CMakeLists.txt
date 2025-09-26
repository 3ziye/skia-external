cmake_minimum_required(VERSION 3.14)
include(FetchContent)

add_library(skshaper STATIC
    src/SkShaper.cpp
    src/SkShaper_factory.cpp
    src/SkShaper_primitive.cpp
)

target_include_directories(skshaper PUBLIC include utils)
target_compile_definitions(skshaper 
    PUBLIC SK_SHAPER_PRIMITIVE_AVAILABLE
    PRIVATE SKSHAPER_IMPLEMENTATION=1
)

target_link_libraries(skshaper PUBLIC skia)

# expat
FetchContent_Declare(
    expat
    GIT_REPOSITORY https://github.com/libexpat/libexpat.git
    GIT_TAG        R_2_7_2
    SOURCE_SUBDIR  expat
)

set(EXPAT_BUILD_TESTS OFF CACHE BOOL "" FORCE)
set(EXPAT_BUILD_TOOLS OFF CACHE BOOL "" FORCE)
set(EXPAT_BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)
set(EXPAT_SHARED_LIBS OFF CACHE BOOL "" FORCE)
set(EXPAT_BUILD_DOCS OFF CACHE BOOL "" FORCE)

FetchContent_MakeAvailable(expat)
target_link_libraries(skshaper PUBLIC expat)

if(WIN32)
    target_link_libraries(skshaper PUBLIC user32 gdi32 ole32 oleaut32)
elseif(UNIX AND NOT APPLE)
    target_link_libraries(skshaper PUBLIC dl pthread)
endif()

if(APPLE AND SKSHAPER_USE_CORETEXT)
    target_sources(skshaper PRIVATE src/SkShaper_coretext.cpp)
    target_compile_definitions(skshaper PUBLIC SK_SHAPER_CORETEXT_AVAILABLE)
    target_link_libraries(skshaper PUBLIC "-framework ApplicationServices")
endif()

if(TARGET harfbuzz AND SKSHAPER_USE_HARFBUZZ)
    target_sources(skshaper PRIVATE src/SkShaper_harfbuzz.cpp)
    target_compile_definitions(skshaper PUBLIC SK_SHAPER_HARFBUZZ_AVAILABLE)
    target_link_libraries(skshaper PUBLIC harfbuzz)
endif()

if(SKIA_DUILIB_X)
set_target_properties(skshaper PROPERTIES
  ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_CURRENT_LIST_DIR}/../../../../lib"
  ARCHIVE_OUTPUT_DIRECTORY_DEBUG "${CMAKE_CURRENT_LIST_DIR}/../../../../lib/Debug"
  ARCHIVE_OUTPUT_DIRECTORY_RELEASE "${CMAKE_CURRENT_LIST_DIR}/../../../../lib/Release"
)
endif()