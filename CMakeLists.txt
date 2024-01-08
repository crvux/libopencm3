cmake_minimum_required(VERSION 3.26)
project(libopencm3 LANGUAGES C)
set(CMAKE_C_STANDARD 99)

# FIXME toolchain file
set(CMAKE_C_COMPILER   arm-none-eabi-gcc)
set(CMAKE_AR  arm-none-eabi-ar)

set(LIBOPENCM3_CMAKE_SOURCE_DIR ${CMAKE_CURRENT_LIST_DIR})
set(CMAKE_C_CREATE_STATIC_LIBRARY "<CMAKE_AR> rcsD <TARGET> <OBJECTS> ")

function(generate_irq MCU_PATH)
    add_custom_command(
        OUTPUT
            "${CMAKE_BINARY_DIR}/include/libopencmsis/${MCU_PATH}/irqhandlers.h"
            "${CMAKE_BINARY_DIR}/include/libopencm3/${MCU_PATH}/nvic.h"
            "${CMAKE_BINARY_DIR}/lib/${MCU_PATH}/vector_nvic.c"
        COMMAND
            mkdir -p ${CMAKE_BINARY_DIR}/include/libopencmsis/${MCU_PATH}/
            && mkdir -p ${CMAKE_BINARY_DIR}/include/libopencm3/${MCU_PATH}/
            && python ${LIBOPENCM3_CMAKE_SOURCE_DIR}/scripts/irq2nvic_h ./include/libopencm3/${MCU_PATH}/irq.json
            && mv ${LIBOPENCM3_CMAKE_SOURCE_DIR}/include/libopencmsis/${MCU_PATH}/irqhandlers.h ${CMAKE_BINARY_DIR}/include/libopencmsis/${MCU_PATH}/irqhandlers.h
            && mv ${LIBOPENCM3_CMAKE_SOURCE_DIR}/include/libopencm3/${MCU_PATH}/nvic.h ${CMAKE_BINARY_DIR}/include/libopencm3/${MCU_PATH}/nvic.h
            && mv ${LIBOPENCM3_CMAKE_SOURCE_DIR}/lib/${MCU_PATH}/vector_nvic.c ${CMAKE_BINARY_DIR}/lib/${MCU_PATH}/vector_nvic.c
        DEPENDS
            "${LIBOPENCM3_CMAKE_SOURCE_DIR}/include/libopencm3/${MCU_PATH}/irq.json"
        WORKING_DIRECTORY "${LIBOPENCM3_CMAKE_SOURCE_DIR}"
        VERBATIM
    )
endfunction()

function(libopencm3_collect_sources _FILES _VPATH _FOUND_VAR _NOT_FOUND_VAR)
    # Find sources in vpath dirs
    set(found "")
    foreach(path IN LISTS ${_VPATH})
        set(checkSrcs ${${_FILES}})
        list(TRANSFORM checkSrcs PREPEND "${path}/")
        file(GLOB foundSrcs LIST_DIRECTORIES ON ${checkSrcs})
        set(found ${found} ${foundSrcs})
    endforeach()

    # Check matching
    set(notFound ${${_FILES}})
    foreach(foundFile IN LISTS found)
        get_filename_component(filename "${foundFile}" NAME)
        list(REMOVE_ITEM notFound "${filename}")
    endforeach()

    set(${_FOUND_VAR} ${found} PARENT_SCOPE)
    set(${_NOT_FOUND_VAR} ${notFound} PARENT_SCOPE)
endfunction()

function(libopencm3_add_library)
    # FIXME check mandatory args!
    set(oneValueArgs NAME ALIAS_NAME)
    set(multiValueArgs VPATH FILES DEFINITIONS PRIVATE_COMPILE_OPTIONS PUBLIC_COMPILE_OPTIONS)
    cmake_parse_arguments(_ARG "${options}" "${oneValueArgs}" "${multiValueArgs}" ${ARGN})

#    message("_ARG_NAME=${_ARG_NAME}")
#    message("_ARG_ALIAS_NAME=${_ARG_ALIAS_NAME}")
#    message("_ARG_VPATH=${_ARG_VPATH}")
#    message("_ARG_FILES=${_ARG_FILES}")
#    message("_ARG_DEFINE=${_ARG_DEFINE}")
#    message("_ARG_PRIVATE_COMPILE_OPTIONS=${_ARG_PRIVATE_COMPILE_OPTIONS}")
#    message("_ARG_PUBLIC_COMPILE_OPTIONS=${_ARG_PUBLIC_COMPILE_OPTIONS}")

    # target and alias names
    set(target "opencm3_${_ARG_NAME}")
    set(alias "libopencm3::${_ARG_ALIAS_NAME}")

    # sources
    # try to implement vpath like behavior
    set(vpath "${_ARG_VPATH}")
    list(TRANSFORM vpath PREPEND "${CMAKE_CURRENT_LIST_DIR}/")
    list(APPEND vpath "${CMAKE_CURRENT_LIST_DIR}")
    libopencm3_collect_sources(_ARG_FILES vpath srcs notFoundSrcs)
    if(notFoundSrcs)
        message(FATAL_ERROR
            "Sources not found: ${notFoundSrcs}\n"
            "CMAKE_CURRENT_LIST_DIR: ${CMAKE_CURRENT_LIST_DIR}\n"
            "vpath: ${vpath}\n"
        )
    endif()
    set(cm3SrcDir "${LIBOPENCM3_CMAKE_SOURCE_DIR}/lib/cm3")
    list(APPEND srcs
        "${cm3SrcDir}/vector.c" "${cm3SrcDir}/systick.c" "${cm3SrcDir}/scb.c"
        "${cm3SrcDir}/nvic.c" "${cm3SrcDir}/assert.c" "${cm3SrcDir}/sync.c"
        "${cm3SrcDir}/dwt.c"
    )

    add_library(${target} STATIC)
    add_library(${alias} ALIAS ${target})
    target_compile_definitions(${target} PUBLIC ${_ARG_DEFINITIONS})
    target_compile_options(${target}
        PUBLIC
            ${_ARG_PUBLIC_COMPILE_OPTIONS}
        PRIVATE
            ${_ARG_PRIVATE_COMPILE_OPTIONS}
            -Wall -Wextra -Wimplicit-function-declaration -Wredundant-decls
            -Wmissing-prototypes -Wstrict-prototypes -Wundef -Wshadow
            -fno-common -ffunction-sections -fdata-sections
    )
    # FIXME inconsistency!
    # FIXME bug with files copy!
    if("${_ARG_NAME}" STREQUAL "lm4f")
        generate_irq("lm3s")
        target_include_directories(${target}
            PUBLIC "${CMAKE_BINARY_DIR}/include"
            PRIVATE "${CMAKE_BINARY_DIR}/lib/lm3s"
        )
        target_sources(${target} PRIVATE
            "${CMAKE_BINARY_DIR}/include/libopencmsis/lm3s/irqhandlers.h"
            "${CMAKE_BINARY_DIR}/include/libopencm3/lm3s/nvic.h"
        )
    else()
        # FIXME bad handling of generated files
        string(REPLACE "::" "/" genDir ${_ARG_ALIAS_NAME})
        generate_irq(${genDir})
        string(REPLACE "/" ";" commonDir ${genDir})
        list(GET commonDir 0 commonDir)
        target_include_directories(${target}
            PUBLIC "${CMAKE_BINARY_DIR}/include"
            PRIVATE "${CMAKE_BINARY_DIR}/lib/${commonDir}"
        )
        target_sources(${target} PRIVATE
            "${CMAKE_BINARY_DIR}/include/libopencmsis/${genDir}/irqhandlers.h"
            "${CMAKE_BINARY_DIR}/include/libopencm3/${genDir}/nvic.h"
        )
    endif()
    target_include_directories(${target} PUBLIC "${LIBOPENCM3_CMAKE_SOURCE_DIR}/include/")
    target_sources(${target} PRIVATE ${srcs})
endfunction()

add_subdirectory(lib/efm32)
add_subdirectory(lib/gd32)
add_subdirectory(lib/lm3s)
add_subdirectory(lib/lm4f)
add_subdirectory(lib/lpc13xx)
add_subdirectory(lib/lpc17xx)
add_subdirectory(lib/lpc43xx)
add_subdirectory(lib/msp432)
add_subdirectory(lib/nrf)
add_subdirectory(lib/pac55xx)
add_subdirectory(lib/sam)
add_subdirectory(lib/stm32)
add_subdirectory(lib/swm050)
add_subdirectory(lib/vf6xx)
