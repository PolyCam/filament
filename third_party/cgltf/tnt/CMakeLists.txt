cmake_minimum_required(VERSION 3.19)
project(cgltf)

set(TARGET cgltf)

set(PUBLIC_HDR_DIR ${CMAKE_CURRENT_SOURCE_DIR}/..)

set(PUBLIC_HDRS
    ${PUBLIC_HDR_DIR}/cgltf_write.h
    ${PUBLIC_HDR_DIR}/cgltf.h)

add_compile_definitions($<$<CONFIG:Debug>:CGLTF_VALIDATE_ENABLE_ASSERTS=1>)

add_library(${TARGET} INTERFACE)
target_include_directories(${TARGET} INTERFACE
    $<BUILD_INTERFACE:${PUBLIC_HDR_DIR}>
    $<INSTALL_INTERFACE:include>
)
set_target_properties(${TARGET} PROPERTIES FOLDER ThirdParty)
install(TARGETS ${TARGET} EXPORT filamentTargets ARCHIVE DESTINATION lib)