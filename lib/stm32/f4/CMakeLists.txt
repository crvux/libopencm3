set(LIB_NAME opencm3_stm32f4)
set(FAMILY STM32F4)
set(PATH_FRAG "stm32/f4")

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
    -mcpu=cortex-m4 -mthumb -Wstrict-prototypes
    -ffunction-sections -fdata-sections
    -mfloat-abi=hard -mfpu=fpv4-sp-d16
)
# FIXME include only needed!
target_include_directories(${LIB_NAME} PRIVATE
    "${CMAKE_SOURCE_DIR}/include/"
    "${CMAKE_BINARY_DIR}/include/"
    "${CMAKE_BINARY_DIR}/lib/stm32/"
)
target_sources(${LIB_NAME} PRIVATE
    "${COMMON_SRC_DIR}/adc_common_v1.c" "${COMMON_SRC_DIR}/adc_common_v1_multi.c" "${COMMON_SRC_DIR}/adc_common_f47.c"
    "${COMMON_STM32_SRC_DIR}/can.c"
    "${COMMON_SRC_DIR}/crc_common_all.c"
    "${COMMON_SRC_DIR}/crypto_common_f24.c" "${TARGET_SRC_DIR}/crypto.c"
    "${COMMON_SRC_DIR}/dac_common_all.c" "${COMMON_SRC_DIR}/dac_common_v1.c"
    "${COMMON_SRC_DIR}/dcmi_common_f47.c"
    "${COMMON_SRC_DIR}/desig_common_all.c" "${COMMON_SRC_DIR}/desig_common_v1.c"
    "${COMMON_SRC_DIR}/dma_common_f24.c"
    "${COMMON_SRC_DIR}/dma2d_common_f47.c"
    "${COMMON_SRC_DIR}/dsi_common_f47.c"
    "${COMMON_SRC_DIR}/exti_common_all.c"
    "${TARGET_SRC_DIR}/flash.c" "${COMMON_SRC_DIR}/flash_common_all.c" "${COMMON_SRC_DIR}/flash_common_f.c"
    "${COMMON_SRC_DIR}/flash_common_f24.c" "${COMMON_SRC_DIR}/flash_common_idcache.c"
    "${COMMON_SRC_DIR}/fmc_common_f47.c"
    "${COMMON_SRC_DIR}/gpio_common_all.c" "${COMMON_SRC_DIR}/gpio_common_f0234.c"
    "${COMMON_SRC_DIR}/hash_common_f24.c"
    "${COMMON_SRC_DIR}/i2c_common_v1.c"
    "${COMMON_SRC_DIR}/iwdg_common_all.c"
    "${COMMON_SRC_DIR}/lptimer_common_all.c"
    "${COMMON_SRC_DIR}/ltdc_common_f47.c"
    "${COMMON_SRC_DIR}/pwr_common_v1.c" "${TARGET_SRC_DIR}/pwr.c"
    "${COMMON_SRC_DIR}/rcc_common_all.c" "${TARGET_SRC_DIR}/rcc.c"
    "${COMMON_SRC_DIR}/rng_common_v1.c"
    "${COMMON_SRC_DIR}/rtc_common_l1f024.c" "${TARGET_SRC_DIR}/rtc.c"
    "${COMMON_SRC_DIR}/spi_common_all.c" "${COMMON_SRC_DIR}/spi_common_v1.c" "${COMMON_SRC_DIR}/spi_common_v1_frf.c"
    "${COMMON_SRC_DIR}/timer_common_all.c" "${COMMON_SRC_DIR}/timer_common_f0234.c" "${COMMON_SRC_DIR}/timer_common_f24.c"
    "${COMMON_SRC_DIR}/usart_common_all.c" "${COMMON_SRC_DIR}/usart_common_f124.c"
    "${COMMON_SRC_DIR}/quadspi_common_v1.c"

    "${USB_SRC_DIR}/usb.c" "${USB_SRC_DIR}/usb_standard.c" "${USB_SRC_DIR}/usb_control.c" "${USB_SRC_DIR}/usb_msc.c"
    "${USB_SRC_DIR}/usb_hid.c"
    "${USB_SRC_DIR}/usb_audio.c" "${USB_SRC_DIR}/usb_cdc.c" "${USB_SRC_DIR}/usb_midi.c"
    "${USB_SRC_DIR}/usb_dwc_common.c" "${USB_SRC_DIR}/usb_f107.c" "${USB_SRC_DIR}/usb_f207.c"

    "${ETH_SRC_DIR}/mac.c" "${ETH_SRC_DIR}/phy.c"
    "${ETH_SRC_DIR}/mac_stm32fxx7.c" "${ETH_SRC_DIR}/phy_ksz80x1.c"

    # FIXME cmsis sources
    "${CM3_SRC_DIR}/vector.c"
    "${CM3_SRC_DIR}/systick.c"
    "${CM3_SRC_DIR}/scb.c"
    "${CM3_SRC_DIR}/nvic.c"
    "${CM3_SRC_DIR}/assert.c"
    "${CM3_SRC_DIR}/sync.c"
    "${CM3_SRC_DIR}/dwt.c"
)
