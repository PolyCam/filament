cmake_minimum_required(VERSION 3.19)
project(tsl)

set(TARGET tsl)
set(OUR_DIR ${CMAKE_CURRENT_SOURCE_DIR}/..)

# ==================================================================================================
# Sources and headers
# ==================================================================================================
set(PUBLIC_HDRS
        ${OUR_DIR}/tsl/robin_growth_policy.h
        ${OUR_DIR}/tsl/robin_hash.h
        ${OUR_DIR}/tsl/robin_map.h
        ${OUR_DIR}/tsl/robin_set.h
)

# ==================================================================================================
# Include and target definitions
# ==================================================================================================

add_library(${TARGET} INTERFACE ${PUBLIC_HDRS})
target_include_directories(${TARGET} INTERFACE
    $<BUILD_INTERFACE:${OUR_DIR}>
    $<INSTALL_INTERFACE:include>
)
set_target_properties(${TARGET} PROPERTIES FOLDER ThirdParty)

# ==================================================================================================
# Installation
# ==================================================================================================
install(FILES ${PUBLIC_HDRS} DESTINATION include/${TARGET})
install(TARGETS ${TARGET} EXPORT filamentTargets ARCHIVE DESTINATION lib)
