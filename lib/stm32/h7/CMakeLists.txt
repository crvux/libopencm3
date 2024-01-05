set(LIB_NAME opencm3_stm32h7)
set(FAMILY STM32H7)
set(PATH_FRAG "stm32/h7")

set(COMMON_SRC_DIR "${LIBOPENCM3_CMAKE_SOURCE_DIR}/lib/stm32/common")
set(COMMON_STM32_SRC_DIR "${LIBOPENCM3_CMAKE_SOURCE_DIR}/lib/stm32")
set(USB_SRC_DIR "${LIBOPENCM3_CMAKE_SOURCE_DIR}/lib/usb")
set(ETH_SRC_DIR "${LIBOPENCM3_CMAKE_SOURCE_DIR}/lib/ethernet")
set(TARGET_SRC_DIR "${LIBOPENCM3_CMAKE_SOURCE_DIR}/lib/${PATH_FRAG}")

generate_irq(${PATH_FRAG})
add_library(${LIB_NAME} STATIC
    "${CMAKE_BINARY_DIR}/include/libopencmsis/${PATH_FRAG}/irqhandlers.h"
    "${CMAKE_BINARY_DIR}/include/libopencm3/${PATH_FRAG}/nvic.h"
)
target_compile_definitions(${LIB_NAME} PUBLIC ${FAMILY})
target_compile_options(${LIB_NAME} PRIVATE
    -Os
    -Wall -Wextra -Wimplicit-function-declaration
    -Wredundant-decls -Wmissing-prototypes -Wstrict-prototypes
    -Wundef -Wshadow
    -fno-common
    -mcpu=cortex-m7 -mthumb -Wstrict-prototypes
    -ffunction-sections -fdata-sections
    -mfloat-abi=hard -mfpu=fpv5-d16
)
# FIXME include only needed!
target_include_directories(${LIB_NAME} PRIVATE
    "${LIBOPENCM3_CMAKE_SOURCE_DIR}/include/"
    "${CMAKE_BINARY_DIR}/include/"
    "${CMAKE_BINARY_DIR}/lib/stm32/"
)
target_sources(${LIB_NAME} PRIVATE
    "${COMMON_SRC_DIR}/dac_common_all.c" "${COMMON_SRC_DIR}/dac_common_v2.c"
    "${COMMON_SRC_DIR}/exti_common_all.c"
    "${TARGET_SRC_DIR}/fdcan.c" "${COMMON_SRC_DIR}/fdcan_common.c"
    "${COMMON_SRC_DIR}/flash_common_all.c" "${COMMON_SRC_DIR}/flash_common_f.c" "${COMMON_SRC_DIR}/flash_common_f24.c"
    "${COMMON_SRC_DIR}/fmc_common_f47.c"
    "${COMMON_SRC_DIR}/gpio_common_all.c" "${COMMON_SRC_DIR}/gpio_common_f0234.c"
    "${TARGET_SRC_DIR}/pwr.c"
    "${TARGET_SRC_DIR}/rcc.c" "${COMMON_SRC_DIR}/rcc_common_all.c"
    "${COMMON_SRC_DIR}/rng_common_v1.c"
    "${COMMON_SRC_DIR}/spi_common_all.c" "${COMMON_SRC_DIR}/spi_common_v2.c"
    "${COMMON_SRC_DIR}/timer_common_all.c"
    "${COMMON_SRC_DIR}/usart_common_all.c" "${COMMON_SRC_DIR}/usart_common_v2.c" "${COMMON_SRC_DIR}/usart_common_fifos.c"
    "${COMMON_SRC_DIR}/quadspi_common_v1.c"

    "${CM3_SRCS}"
)
