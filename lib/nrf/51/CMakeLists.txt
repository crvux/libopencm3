set(LIB_NAME opencm3_nrf51)
set(FAMILY NRF51)
set(PATH_FRAG "nrf/51")

set(COMMON_SRC_DIR "${CMAKE_SOURCE_DIR}/lib/nrf/common")
set(TARGET_SRC_DIR "${CMAKE_SOURCE_DIR}/lib/${PATH_FRAG}")

generate_irq(${PATH_FRAG})
add_library(${LIB_NAME} STATIC
    "${CMAKE_BINARY_DIR}/include/libopencmsis/${PATH_FRAG}/irqhandlers.h"
    "${CMAKE_BINARY_DIR}/include/libopencm3/${PATH_FRAG}/nvic.h"
)
target_compile_definitions(${LIB_NAME} PUBLIC ${FAMILY})
target_compile_options(${LIB_NAME} PRIVATE
    -Os -Wall -Wextra -fno-common
    -mcpu=cortex-m0 -mthumb -msoft-float
    -Wredundant-decls -Wmissing-prototypes -Wstrict-prototypes
    -ffunction-sections -fdata-sections
)
# FIXME include only needed!
target_include_directories(${LIB_NAME} PRIVATE
    "${CMAKE_SOURCE_DIR}/include/"
    "${CMAKE_BINARY_DIR}/include/"
    "${CMAKE_BINARY_DIR}/lib/stm32/"
)
target_sources(${LIB_NAME} PRIVATE
    "${COMMON_SRC_DIR}/clock_common.c" "${TARGET_SRC_DIR}/clock.c"
    "${COMMON_SRC_DIR}/gpio.c"
    "${COMMON_SRC_DIR}/i2c_common.c"
    "${COMMON_SRC_DIR}/ppi.c"
    "${COMMON_SRC_DIR}/rtc.c"
    "${COMMON_SRC_DIR}/radio_common.c" "${TARGET_SRC_DIR}/radio.c"
    "${COMMON_SRC_DIR}/timer.c"
    "${COMMON_SRC_DIR}/uart.c"

    "${CM3_SRCS}"
)
