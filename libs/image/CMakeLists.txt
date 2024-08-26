cmake_minimum_required(VERSION 3.19)
project(image)

set(TARGET image)
set(PUBLIC_HDR_DIR include)

# ==================================================================================================
# Sources and headers
# ==================================================================================================
set(PUBLIC_HDRS
        include/image/ColorTransform.h
        include/image/ImageOps.h
        include/image/ImageSampler.h
        include/image/Ktx1Bundle.h
        include/image/LinearImage.h
)

set(SRCS
        src/ImageOps.cpp
        src/ImageSampler.cpp
        src/Ktx1Bundle.cpp
        src/LinearImage.cpp
)

# ==================================================================================================
# Include and target definitions
# ==================================================================================================
include_directories(${PUBLIC_HDR_DIR})

add_library(${TARGET} STATIC ${PUBLIC_HDRS} ${SRCS})

target_link_libraries(${TARGET} PUBLIC math utils)

target_include_directories(${TARGET} PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/${PUBLIC_HDR_DIR}>
    $<INSTALL_INTERFACE:include>
)
set_target_properties(${TARGET} PROPERTIES FOLDER Libs)

# ==================================================================================================
# Compiler flags
# ==================================================================================================
if (MSVC)
    target_compile_options(${TARGET} PRIVATE $<$<CONFIG:Release>:/fp:fast>)
else()
    target_compile_options(${TARGET} PRIVATE $<$<CONFIG:Release>:-ffast-math>)
    target_compile_options(${TARGET} PRIVATE -Wno-deprecated-register)
endif()

# ==================================================================================================
# Installation
# ==================================================================================================
install(TARGETS ${TARGET} EXPORT filamentTargets ARCHIVE DESTINATION lib)
install(DIRECTORY ${PUBLIC_HDR_DIR}/image DESTINATION include)
