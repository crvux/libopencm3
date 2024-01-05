set(LIB_NAME opencm3_stm32f3)
set(FAMILY STM32F3)
set(PATH_FRAG "stm32/f3")

set(COMMON_SRC_DIR "${CMAKE_SOURCE_DIR}/lib/stm32/common")
set(COMMON_STM32_SRC_DIR "${CMAKE_SOURCE_DIR}/lib/stm32")
set(USB_SRC_DIR "${CMAKE_SOURCE_DIR}/lib/usb")
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
    "${TARGET_SRC_DIR}/adc.c" "${COMMON_SRC_DIR}/adc_common_v2.c" "${COMMON_SRC_DIR}/adc_common_v2_multi.c"
    "${COMMON_STM32_SRC_DIR}/can.c"
    "${COMMON_SRC_DIR}/crc_common_all.c" "${COMMON_SRC_DIR}/crc_v2.c"
    "${COMMON_SRC_DIR}/dac_common_all.c" "${COMMON_SRC_DIR}/dac_common_v1.c"
    "${COMMON_SRC_DIR}/desig_common_all.c" "${COMMON_SRC_DIR}/desig_common_v1.c"
    "${COMMON_SRC_DIR}/dma_common_l1f013.c"
    "${COMMON_SRC_DIR}/exti_common_all.c"
    "${TARGET_SRC_DIR}/flash.c" "${COMMON_SRC_DIR}/flash_common_all.c" "${COMMON_SRC_DIR}/flash_common_f.c"
    "${COMMON_SRC_DIR}/gpio_common_all.c" "${COMMON_SRC_DIR}/gpio_common_f0234.c"
    "${COMMON_SRC_DIR}/i2c_common_v2.c"
    "${COMMON_SRC_DIR}/iwdg_common_all.c"
    "${COMMON_SRC_DIR}/opamp_common_all.c" "${COMMON_SRC_DIR}/opamp_common_v1.c"
    "${COMMON_SRC_DIR}/pwr_common_v1.c"
    "${TARGET_SRC_DIR}/rcc.c" "${COMMON_SRC_DIR}/rcc_common_all.c"
    "${COMMON_SRC_DIR}/rtc_common_l1f024.c"
    "${COMMON_SRC_DIR}/spi_common_all.c" "${COMMON_SRC_DIR}/spi_common_v2.c"
    "${COMMON_SRC_DIR}/timer_common_all.c" "${COMMON_SRC_DIR}/timer_common_f0234.c"
    "${COMMON_SRC_DIR}/usart_common_v2.c" "${COMMON_SRC_DIR}/usart_common_all.c"

    "${USB_SRC_DIR}/usb.c" "${USB_SRC_DIR}/usb_control.c" "${USB_SRC_DIR}/usb_standard.c" "${USB_SRC_DIR}/usb_msc.c"
    "${USB_SRC_DIR}/usb_hid.c"
    "${USB_SRC_DIR}/usb_audio.c" "${USB_SRC_DIR}/usb_cdc.c" "${USB_SRC_DIR}/usb_midi.c"
    "${COMMON_SRC_DIR}/st_usbfs_core.c" "${COMMON_STM32_SRC_DIR}/st_usbfs_v1.c"

    "${CM3_SRCS}"
)
