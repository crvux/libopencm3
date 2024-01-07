set(LIB_NAME opencm3_lpc43xx_m0)
set(FAMILY LPC43XX_M0)
set(PATH_FRAG "lpc43xx/m0")

set(TARGET_SRC_DIR "${LIBOPENCM3_CMAKE_SOURCE_DIR}/lib/${PATH_FRAG}")
set(COMMON_SRC_DIR "${LIBOPENCM3_CMAKE_SOURCE_DIR}/lib/lpc43xx")

generate_irq(${PATH_FRAG})
add_library(${LIB_NAME} STATIC
    "${CMAKE_BINARY_DIR}/include/libopencmsis/${PATH_FRAG}/irqhandlers.h"
    "${CMAKE_BINARY_DIR}/include/libopencm3/${PATH_FRAG}/nvic.h"
)
target_compile_definitions(${LIB_NAME} PUBLIC ${FAMILY} LPC43XX)
target_compile_options(${LIB_NAME} PRIVATE
    ${GCC_WARN_OPTIONS}
    -mcpu=cortex-m0 -mthumb
    -O2 -fno-common -ffunction-sections -fdata-sections
)
# FIXME include only needed!
target_include_directories(${LIB_NAME} PRIVATE
    "${LIBOPENCM3_CMAKE_SOURCE_DIR}/include/"
    "${CMAKE_BINARY_DIR}/include/"
    "${CMAKE_BINARY_DIR}/lib/stm32/"
)
target_sources(${LIB_NAME} PRIVATE
    "${COMMON_SRC_DIR}/gpio.c"
    "${COMMON_SRC_DIR}/scu.c"
    "${COMMON_SRC_DIR}/i2c.c"
    "${COMMON_SRC_DIR}/ssp.c"
    "${COMMON_SRC_DIR}/uart.c"
    "${COMMON_SRC_DIR}/timer.c"

    "${CM3_SRCS}"
)
