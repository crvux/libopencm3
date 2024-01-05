cmake_minimum_required(VERSION 3.26)
project(libopencm3 LANGUAGES C)
set(CMAKE_C_STANDARD 99)

# FIXME toolchain file
set(CMAKE_C_COMPILER   arm-none-eabi-gcc)
set(CMAKE_AR  arm-none-eabi-ar)

set(CMAKE_C_OUTPUT_EXTENSION_REPLACE 1)
set(CMAKE_C_OUTPUT_EXTENSION .o)
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
            && python ${CMAKE_SOURCE_DIR}/scripts/irq2nvic_h ./include/libopencm3/${MCU_PATH}/irq.json
            && mv ${CMAKE_SOURCE_DIR}/include/libopencmsis/${MCU_PATH}/irqhandlers.h ${CMAKE_BINARY_DIR}/include/libopencmsis/${MCU_PATH}/irqhandlers.h
            && mv ${CMAKE_SOURCE_DIR}/include/libopencm3/${MCU_PATH}/nvic.h ${CMAKE_BINARY_DIR}/include/libopencm3/${MCU_PATH}/nvic.h
            && mv ${CMAKE_SOURCE_DIR}/lib/${MCU_PATH}/vector_nvic.c ${CMAKE_BINARY_DIR}/lib/${MCU_PATH}/vector_nvic.c
        DEPENDS
            "${CMAKE_SOURCE_DIR}/include/libopencm3/${MCU_PATH}/irq.json"
        WORKING_DIRECTORY "${CMAKE_SOURCE_DIR}"
        VERBATIM
    )
endfunction()

set(CM3_SRC_DIR "${CMAKE_SOURCE_DIR}/lib/cm3")
set(CM3_SRCS
    "${CM3_SRC_DIR}/vector.c"
    "${CM3_SRC_DIR}/systick.c"
    "${CM3_SRC_DIR}/scb.c"
    "${CM3_SRC_DIR}/nvic.c"
    "${CM3_SRC_DIR}/assert.c"
    "${CM3_SRC_DIR}/sync.c"
    "${CM3_SRC_DIR}/dwt.c"
)

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
