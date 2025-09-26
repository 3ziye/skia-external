cmake_minimum_required(VERSION 3.16)
project(skia-modules-svg LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_compile_options("$<$<C_COMPILER_ID:MSVC>:/utf-8>")
add_compile_options("$<$<CXX_COMPILER_ID:MSVC>:/utf-8>")

add_definitions(-DUNICODE -D_UNICODE)

if(MSVC)
    add_compile_options(
        $<$<CONFIG:Debug>:/MTd>
        $<$<CONFIG:Release>:/MT>
    )
endif()

option(SKIA_ENABLE_SVG "Enable SVG support" ON)
option(SKIA_USE_EXPAT "Use Expat for XML parsing" ON)
option(SKIA_ENABLE_TOOLS "Enable Skia tools" OFF)

set(SVG_INCLUDE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/include")
set(SVG_SRC_DIR "${CMAKE_CURRENT_SOURCE_DIR}/src")
set(SVG_TESTS_DIR "${CMAKE_CURRENT_SOURCE_DIR}/tests")
set(SVG_UTILS_DIR "${CMAKE_CURRENT_SOURCE_DIR}/utils")

set(SVG_PUBLIC_HEADERS
    ${SVG_INCLUDE_DIR}/SkSVGAttribute.h
    ${SVG_INCLUDE_DIR}/SkSVGAttributeParser.h
    ${SVG_INCLUDE_DIR}/SkSVGCircle.h
    ${SVG_INCLUDE_DIR}/SkSVGClipPath.h
    ${SVG_INCLUDE_DIR}/SkSVGContainer.h
    ${SVG_INCLUDE_DIR}/SkSVGDOM.h
    ${SVG_INCLUDE_DIR}/SkSVGDefs.h
    ${SVG_INCLUDE_DIR}/SkSVGEllipse.h
    ${SVG_INCLUDE_DIR}/SkSVGFe.h
    ${SVG_INCLUDE_DIR}/SkSVGFeBlend.h
    ${SVG_INCLUDE_DIR}/SkSVGFeColorMatrix.h
    ${SVG_INCLUDE_DIR}/SkSVGFeComponentTransfer.h
    ${SVG_INCLUDE_DIR}/SkSVGFeComposite.h
    ${SVG_INCLUDE_DIR}/SkSVGFeDisplacementMap.h
    ${SVG_INCLUDE_DIR}/SkSVGFeFlood.h
    ${SVG_INCLUDE_DIR}/SkSVGFeGaussianBlur.h
    ${SVG_INCLUDE_DIR}/SkSVGFeImage.h
    ${SVG_INCLUDE_DIR}/SkSVGFeLightSource.h
    ${SVG_INCLUDE_DIR}/SkSVGFeLighting.h
    ${SVG_INCLUDE_DIR}/SkSVGFeMerge.h
    ${SVG_INCLUDE_DIR}/SkSVGFeMorphology.h
    ${SVG_INCLUDE_DIR}/SkSVGFeOffset.h
    ${SVG_INCLUDE_DIR}/SkSVGFeTurbulence.h
    ${SVG_INCLUDE_DIR}/SkSVGFilter.h
    ${SVG_INCLUDE_DIR}/SkSVGFilterContext.h
    ${SVG_INCLUDE_DIR}/SkSVGG.h
    ${SVG_INCLUDE_DIR}/SkSVGGradient.h
    ${SVG_INCLUDE_DIR}/SkSVGHiddenContainer.h
    ${SVG_INCLUDE_DIR}/SkSVGIDMapper.h
    ${SVG_INCLUDE_DIR}/SkSVGImage.h
    ${SVG_INCLUDE_DIR}/SkSVGLine.h
    ${SVG_INCLUDE_DIR}/SkSVGLinearGradient.h
    ${SVG_INCLUDE_DIR}/SkSVGMask.h
    ${SVG_INCLUDE_DIR}/SkSVGNode.h
    ${SVG_INCLUDE_DIR}/SkSVGOpenTypeSVGDecoder.h
    ${SVG_INCLUDE_DIR}/SkSVGPath.h
    ${SVG_INCLUDE_DIR}/SkSVGPattern.h
    ${SVG_INCLUDE_DIR}/SkSVGPoly.h
    ${SVG_INCLUDE_DIR}/SkSVGRadialGradient.h
    ${SVG_INCLUDE_DIR}/SkSVGRect.h
    ${SVG_INCLUDE_DIR}/SkSVGRenderContext.h
    ${SVG_INCLUDE_DIR}/SkSVGSVG.h
    ${SVG_INCLUDE_DIR}/SkSVGShape.h
    ${SVG_INCLUDE_DIR}/SkSVGStop.h
    ${SVG_INCLUDE_DIR}/SkSVGText.h
    ${SVG_INCLUDE_DIR}/SkSVGTransformableNode.h
    ${SVG_INCLUDE_DIR}/SkSVGTypes.h
    ${SVG_INCLUDE_DIR}/SkSVGUse.h
    ${SVG_INCLUDE_DIR}/SkSVGValue.h
)

set(SVG_SOURCES
    ${SVG_SRC_DIR}/SkSVGAttribute.cpp
    ${SVG_SRC_DIR}/SkSVGAttributeParser.cpp
    ${SVG_SRC_DIR}/SkSVGCircle.cpp
    ${SVG_SRC_DIR}/SkSVGClipPath.cpp
    ${SVG_SRC_DIR}/SkSVGContainer.cpp
    ${SVG_SRC_DIR}/SkSVGDOM.cpp
    ${SVG_SRC_DIR}/SkSVGEllipse.cpp
    ${SVG_SRC_DIR}/SkSVGFe.cpp
    ${SVG_SRC_DIR}/SkSVGFeBlend.cpp
    ${SVG_SRC_DIR}/SkSVGFeColorMatrix.cpp
    ${SVG_SRC_DIR}/SkSVGFeComponentTransfer.cpp
    ${SVG_SRC_DIR}/SkSVGFeComposite.cpp
    ${SVG_SRC_DIR}/SkSVGFeDisplacementMap.cpp
    ${SVG_SRC_DIR}/SkSVGFeFlood.cpp
    ${SVG_SRC_DIR}/SkSVGFeGaussianBlur.cpp
    ${SVG_SRC_DIR}/SkSVGFeImage.cpp
    ${SVG_SRC_DIR}/SkSVGFeLightSource.cpp
    ${SVG_SRC_DIR}/SkSVGFeLighting.cpp
    ${SVG_SRC_DIR}/SkSVGFeMerge.cpp
    ${SVG_SRC_DIR}/SkSVGFeMorphology.cpp
    ${SVG_SRC_DIR}/SkSVGFeOffset.cpp
    ${SVG_SRC_DIR}/SkSVGFeTurbulence.cpp
    ${SVG_SRC_DIR}/SkSVGFilter.cpp
    ${SVG_SRC_DIR}/SkSVGFilterContext.cpp
    ${SVG_SRC_DIR}/SkSVGGradient.cpp
    ${SVG_SRC_DIR}/SkSVGImage.cpp
    ${SVG_SRC_DIR}/SkSVGLine.cpp
    ${SVG_SRC_DIR}/SkSVGLinearGradient.cpp
    ${SVG_SRC_DIR}/SkSVGMask.cpp
    ${SVG_SRC_DIR}/SkSVGNode.cpp
    ${SVG_SRC_DIR}/SkSVGOpenTypeSVGDecoder.cpp
    ${SVG_SRC_DIR}/SkSVGPath.cpp
    ${SVG_SRC_DIR}/SkSVGPattern.cpp
    ${SVG_SRC_DIR}/SkSVGPoly.cpp
    ${SVG_SRC_DIR}/SkSVGRadialGradient.cpp
    ${SVG_SRC_DIR}/SkSVGRect.cpp
    ${SVG_SRC_DIR}/SkSVGRenderContext.cpp
    ${SVG_SRC_DIR}/SkSVGSVG.cpp
    ${SVG_SRC_DIR}/SkSVGShape.cpp
    ${SVG_SRC_DIR}/SkSVGStop.cpp
    ${SVG_SRC_DIR}/SkSVGText.cpp
    ${SVG_SRC_DIR}/SkSVGTransformableNode.cpp
    ${SVG_SRC_DIR}/SkSVGUse.cpp
    ${SVG_SRC_DIR}/SkSVGValue.cpp
    ${SVG_SRC_DIR}/SkSVGRectPriv.h
    ${SVG_SRC_DIR}/SkSVGTextPriv.h
)

if(SKIA_ENABLE_SVG AND SKIA_USE_EXPAT)
    add_library(svg STATIC ${SVG_SOURCES} ${SVG_PUBLIC_HEADERS})
    
    target_include_directories(svg
        PUBLIC
            $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
            $<INSTALL_INTERFACE:include/svg>
        PRIVATE
            ${SVG_SRC_DIR}
            $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/../../include>
            ${CMAKE_CURRENT_SOURCE_DIR}/../../
    )
    
    target_compile_definitions(svg
        PUBLIC
            SK_ENABLE_SVG
        PRIVATE
            SK_IMPLEMENTATION
    )
    
    target_link_libraries(svg
        PUBLIC
            # skia::skia  # 主 Skia 库
            # skia::skresources
            # skia::skshaper
            # skia::skunicode
    )
    
    add_library(skia::svg ALIAS svg)
    

    install(FILES ${SVG_PUBLIC_HEADERS}
        DESTINATION include/svg
    )
    
    if(SKIA_ENABLE_TOOLS)
        add_executable(svg_tool
            ${SVG_UTILS_DIR}/SvgTool.cpp
        )
        
        target_link_libraries(svg_tool
            PRIVATE
                svg
                # skia::skia
                # skia::flags
                # skia::tool_utils
        )
        
        target_compile_definitions(svg_tool
            PRIVATE
                SK_IMPLEMENTATION
        )
    endif()
    
    if(SKIA_ENABLE_TOOLS)
        add_executable(svg_tests
            ${SVG_TESTS_DIR}/Filters.cpp
            ${SVG_TESTS_DIR}/Text.cpp
        )
        
        target_link_libraries(svg_tests
            PRIVATE
                svg
                # skia::skia
                # skia::test
                # skia::skshaper
        )
        
        target_compile_definitions(svg_tests
            PRIVATE
                SK_IMPLEMENTATION
        )
    endif()
    
else()
    add_library(svg INTERFACE)
    add_library(skia::svg ALIAS svg)
endif()

message(STATUS "Skia SVG Module Configuration:")
message(STATUS "  SKIA_ENABLE_SVG: ${SKIA_ENABLE_SVG}")
message(STATUS "  SKIA_USE_EXPAT: ${SKIA_USE_EXPAT}")
message(STATUS "  SKIA_ENABLE_TOOLS: ${SKIA_ENABLE_TOOLS}")

if(SKIA_DUILIB_X)
set_target_properties(svg PROPERTIES
  ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_CURRENT_LIST_DIR}/../../../../lib"
  ARCHIVE_OUTPUT_DIRECTORY_DEBUG "${CMAKE_CURRENT_LIST_DIR}/../../../../lib/Debug"
  ARCHIVE_OUTPUT_DIRECTORY_RELEASE "${CMAKE_CURRENT_LIST_DIR}/../../../../lib/Release"
)
endif()