set(LIB_NAME opencm3_lpc13xx)
set(FAMILY LPC13XX)
set(PATH_FRAG "lpc13xx")

set(TARGET_SRC_DIR "${LIBOPENCM3_CMAKE_SOURCE_DIR}/lib/${PATH_FRAG}")

generate_irq(${PATH_FRAG})
add_library(${LIB_NAME} STATIC
    "${CMAKE_BINARY_DIR}/include/libopencmsis/${PATH_FRAG}/irqhandlers.h"
    "${CMAKE_BINARY_DIR}/include/libopencm3/${PATH_FRAG}/nvic.h"
)
target_compile_definitions(${LIB_NAME} PUBLIC ${FAMILY})
target_compile_options(${LIB_NAME} PRIVATE
    ${GCC_WARN_OPTIONS}
    -mcpu=cortex-m3 -mthumb
    -Os -fno-common -ffunction-sections -fdata-sections
)
# FIXME include only needed!
target_include_directories(${LIB_NAME} PRIVATE
    "${LIBOPENCM3_CMAKE_SOURCE_DIR}/include/"
    "${CMAKE_BINARY_DIR}/include/"
    "${CMAKE_BINARY_DIR}/lib/stm32/"
)
target_sources(${LIB_NAME} PRIVATE
    "${TARGET_SRC_DIR}/gpio.c"

    "${CM3_SRCS}"
)
