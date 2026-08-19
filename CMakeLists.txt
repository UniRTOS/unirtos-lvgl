message(STATUS "cmake config ${CMAKE_CURRENT_SOURCE_DIR}")

set(target unirtos-lvgl)
if(DEFINED UNIRTOS_EXTERNAL_LIBRARY_NAME)
    set(target ${UNIRTOS_EXTERNAL_LIBRARY_NAME})
endif()

if(NOT target STREQUAL "unirtos-lvgl")
    message(FATAL_ERROR "This repository must be built as the unirtos-lvgl library")
endif()

add_library(${target} STATIC)

set(LVGL_DIR ${CMAKE_CURRENT_SOURCE_DIR}/lvgl-v8.3.11)
file(GLOB_RECURSE LVGL_SRC CONFIGURE_DEPENDS ${LVGL_DIR}/src/*.c)

target_include_directories(${target} PRIVATE
    ${SOURCE_TOP_DIR}
    ${SOURCE_SYS_DEBUG_DIR}
    ${SOURCE_SYS_OS_DIR}
    ${SOURCE_COMPONENTS_PUBLIC_INC}
)

# Consumers must compile against the exact same LVGL configuration.
target_include_directories(${target} PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}/include
    ${LVGL_DIR}
)
target_compile_definitions(${target} PUBLIC LV_CONF_INCLUDE_SIMPLE)
target_sources(${target} PRIVATE ${LVGL_SRC})

