set(LIB_NAME opencm3_stm32f2)
set(FAMILY STM32F2)
set(PATH_FRAG "stm32/f2")

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
    -mcpu=cortex-m3 -mthumb -Wstrict-prototypes
    -ffunction-sections -fdata-sections
)
# FIXME include only needed!
target_include_directories(${LIB_NAME} PRIVATE
    "${CMAKE_SOURCE_DIR}/include/"
    "${CMAKE_BINARY_DIR}/include/"
    "${CMAKE_BINARY_DIR}/lib/stm32/"
)
target_sources(${LIB_NAME} PRIVATE
    "${COMMON_SRC_DIR}/crc_common_all.c"
    "${COMMON_SRC_DIR}/crypto_common_f24.c"
    "${COMMON_SRC_DIR}/dac_common_all.c" "${COMMON_SRC_DIR}/dac_common_v1.c"
    "${COMMON_SRC_DIR}/desig_common_all.c" "${COMMON_SRC_DIR}/desig_common_v1.c"
    "${COMMON_SRC_DIR}/dma_common_f24.c"
    "${COMMON_SRC_DIR}/exti_common_all.c"
    "${TARGET_SRC_DIR}/flash.c" "${COMMON_SRC_DIR}/flash_common_all.c" "${COMMON_SRC_DIR}/flash_common_f.c"
    "${COMMON_SRC_DIR}/flash_common_f24.c" "${COMMON_SRC_DIR}/flash_common_idcache.c"
    "${COMMON_SRC_DIR}/gpio_common_all.c" "${COMMON_SRC_DIR}/gpio_common_f0234.c"
    "${COMMON_SRC_DIR}/hash_common_f24.c"
    "${COMMON_SRC_DIR}/i2c_common_v1.c"
    "${COMMON_SRC_DIR}/iwdg_common_all.c"
    "${TARGET_SRC_DIR}/rcc.c" "${COMMON_SRC_DIR}/rcc_common_all.c"
    "${COMMON_SRC_DIR}/rng_common_v1.c"
    "${COMMON_SRC_DIR}/rtc_common_l1f024.c"
    "${COMMON_SRC_DIR}/spi_common_all.c" "${COMMON_SRC_DIR}/spi_common_v1.c" "${COMMON_SRC_DIR}/spi_common_v1_frf.c"
    "${COMMON_SRC_DIR}/timer_common_all.c" "${COMMON_SRC_DIR}/timer_common_f0234.c" "${COMMON_SRC_DIR}/timer_common_f24.c"
    "${COMMON_SRC_DIR}/usart_common_all.c" "${COMMON_SRC_DIR}/usart_common_f124.c"

    "${USB_SRC_DIR}/usb.c" "${USB_SRC_DIR}/usb_standard.c" "${USB_SRC_DIR}/usb_control.c" "${USB_SRC_DIR}/usb_msc.c"
    "${USB_SRC_DIR}/usb_hid.c"
    "${USB_SRC_DIR}/usb_audio.c" "${USB_SRC_DIR}/usb_cdc.c" "${USB_SRC_DIR}/usb_midi.c"
    "${USB_SRC_DIR}/usb_dwc_common.c" "${USB_SRC_DIR}/usb_f107.c" "${USB_SRC_DIR}/usb_f207.c"

    # FIXME cmsis sources
    "${CM3_SRC_DIR}/vector.c"
    "${CM3_SRC_DIR}/systick.c"
    "${CM3_SRC_DIR}/scb.c"
    "${CM3_SRC_DIR}/nvic.c"
    "${CM3_SRC_DIR}/assert.c"
    "${CM3_SRC_DIR}/sync.c"
    "${CM3_SRC_DIR}/dwt.c"
)
