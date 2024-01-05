set(LIB_NAME opencm3_stm32g0)
set(FAMILY STM32G0)
set(PATH_FRAG "stm32/g0")

set(COMMON_SRC_DIR "${CMAKE_SOURCE_DIR}/lib/stm32/common")
set(COMMON_STM32_SRC_DIR "${CMAKE_SOURCE_DIR}/lib/stm32")
set(USB_SRC_DIR "${CMAKE_SOURCE_DIR}/lib/usb")
set(ETH_SRC_DIR "${CMAKE_SOURCE_DIR}/lib/ethernet")
set(CM3_SRC_DIR "${CMAKE_SOURCE_DIR}/lib/cm3")
set(TARGET_SRC_DIR "${CMAKE_SOURCE_DIR}/lib/${PATH_FRAG}")

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
    -mcpu=cortex-m0plus -mthumb -Wstrict-prototypes
    -ffunction-sections -fdata-sections
)
# FIXME include only needed!
target_include_directories(${LIB_NAME} PRIVATE
    "${CMAKE_SOURCE_DIR}/include/"
    "${CMAKE_BINARY_DIR}/include/"
    "${CMAKE_BINARY_DIR}/lib/stm32/"
)
target_sources(${LIB_NAME} PRIVATE
    "${TARGET_SRC_DIR}/adc.c" "${COMMON_SRC_DIR}/adc_common_v2.c"
    "${COMMON_SRC_DIR}/crc_common_all.c"
    "${COMMON_SRC_DIR}/dac_common_all.c" "${COMMON_SRC_DIR}/dac_common_v1.c"
    "${COMMON_SRC_DIR}/desig_common_all.c" "${COMMON_SRC_DIR}/desig_common_v1.c"
    "${COMMON_SRC_DIR}/dma_common_l1f013.c"
    "${COMMON_SRC_DIR}/dmamux.c"
    "${COMMON_SRC_DIR}/exti_common_all.c" "${COMMON_SRC_DIR}/exti_common_v2.c"
    "${TARGET_SRC_DIR}/flash.c" "${COMMON_SRC_DIR}/flash_common_all.c"
    "${COMMON_SRC_DIR}/gpio_common_all.c" "${COMMON_SRC_DIR}/gpio_common_f0234.c"
    "${COMMON_SRC_DIR}/i2c_common_v2.c"
    "${COMMON_SRC_DIR}/iwdg_common_all.c"
    "${COMMON_SRC_DIR}/lptimer_common_all.c"
    "${TARGET_SRC_DIR}/pwr.c"
    "${TARGET_SRC_DIR}/rcc.c" "${COMMON_SRC_DIR}/rcc_common_all.c"
    "${COMMON_SRC_DIR}/rng_common_v1.c"
    "${COMMON_SRC_DIR}/spi_common_all.c" "${COMMON_SRC_DIR}/spi_common_v2.c"
    "${COMMON_SRC_DIR}/timer_common_all.c"
    "${COMMON_SRC_DIR}/usart_common_all.c" "${COMMON_SRC_DIR}/usart_common_v2.c"

    # FIXME cmsis sources
    "${CM3_SRC_DIR}/vector.c"
    "${CM3_SRC_DIR}/systick.c"
    "${CM3_SRC_DIR}/scb.c"
    "${CM3_SRC_DIR}/nvic.c"
    "${CM3_SRC_DIR}/assert.c"
    "${CM3_SRC_DIR}/sync.c"
    "${CM3_SRC_DIR}/dwt.c"
)
