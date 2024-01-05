set(LIB_NAME opencm3_stm32f0)
set(FAMILY STM32F0)
set(PATH_FRAG "stm32/f0")

set(COMMON_SRC_DIR "${LIBOPENCM3_CMAKE_SOURCE_DIR}/lib/stm32/common")
set(COMMON_STM32_SRC_DIR "${LIBOPENCM3_CMAKE_SOURCE_DIR}/lib/stm32")
set(USB_SRC_DIR "${LIBOPENCM3_CMAKE_SOURCE_DIR}/lib/usb")
set(TARGET_SRC_DIR "${LIBOPENCM3_CMAKE_SOURCE_DIR}/lib/${PATH_FRAG}")

generate_irq(${PATH_FRAG})
add_library(${LIB_NAME} STATIC
    "${CMAKE_BINARY_DIR}/include/libopencmsis/${PATH_FRAG}/irqhandlers.h"
    "${CMAKE_BINARY_DIR}/include/libopencm3/${PATH_FRAG}/nvic.h"
)
add_library(libopencm3::stm32::f0 ALIAS ${LIB_NAME})
target_compile_definitions(${LIB_NAME} PUBLIC ${FAMILY})
target_compile_options(${LIB_NAME} PRIVATE
    -Os
    -Wall -Wextra -Wimplicit-function-declaration
    -Wredundant-decls -Wmissing-prototypes -Wstrict-prototypes
    -Wundef -Wshadow
    -fno-common
    -mcpu=cortex-m0 -mthumb -Wstrict-prototypes
    -ffunction-sections -fdata-sections
)
# FIXME include only needed!
target_include_directories(${LIB_NAME}
    PRIVATE
        "${CMAKE_BINARY_DIR}/lib/stm32/"
    PUBLIC
        "${CMAKE_BINARY_DIR}/include/"
        "${LIBOPENCM3_CMAKE_SOURCE_DIR}/include/"
)
target_sources(${LIB_NAME} PRIVATE
    "${TARGET_SRC_DIR}/adc.c" "${COMMON_SRC_DIR}/adc_common_v2.c"
    "${COMMON_STM32_SRC_DIR}/can.c"
    "${TARGET_SRC_DIR}/comparator.c"
    "${COMMON_SRC_DIR}/crc_common_all.c" "${COMMON_SRC_DIR}/crc_v2.c"
    "${COMMON_SRC_DIR}/crs_common_all.c"
    "${COMMON_SRC_DIR}/dac_common_all.c" "${COMMON_SRC_DIR}/dac_common_v1.c"
    "${COMMON_SRC_DIR}/desig_common_all.c" "${COMMON_SRC_DIR}/desig_common_v1.c"
    "${COMMON_SRC_DIR}/dma_common_l1f013.c" "${COMMON_SRC_DIR}/dma_common_csel.c"
    "${COMMON_SRC_DIR}/exti_common_all.c"
    "${TARGET_SRC_DIR}/flash.c" "${COMMON_SRC_DIR}/flash_common_all.c" "${COMMON_SRC_DIR}/flash_common_f.c" "${COMMON_SRC_DIR}/flash_common_f01.c"
    "${COMMON_SRC_DIR}/gpio_common_all.c" "${COMMON_SRC_DIR}/gpio_common_f0234.c"
    "${COMMON_SRC_DIR}/iwdg_common_all.c"
    "${COMMON_SRC_DIR}/i2c_common_v2.c"
    "${COMMON_SRC_DIR}/pwr_common_v1.c"
    "${TARGET_SRC_DIR}/rcc.c" "${COMMON_SRC_DIR}/rcc_common_all.c"
    "${COMMON_SRC_DIR}/rtc_common_l1f024.c"
    "${COMMON_SRC_DIR}/spi_common_all.c" "${COMMON_SRC_DIR}/spi_common_v2.c"
    "${COMMON_SRC_DIR}/timer_common_all.c" "${COMMON_SRC_DIR}/timer_common_f0234.c"
    "${COMMON_SRC_DIR}/usart_common_all.c" "${COMMON_SRC_DIR}/usart_common_v2.c"

    "${USB_SRC_DIR}/usb.c" "${USB_SRC_DIR}/usb_control.c" "${USB_SRC_DIR}/usb_standard.c" "${USB_SRC_DIR}/usb_msc.c"
    "${USB_SRC_DIR}/usb_hid.c"
    "${USB_SRC_DIR}/usb_audio.c" "${USB_SRC_DIR}/usb_cdc.c" "${USB_SRC_DIR}/usb_midi.c"
    "${COMMON_SRC_DIR}/st_usbfs_core.c" "${COMMON_STM32_SRC_DIR}/st_usbfs_v2.c"

    "${CM3_SRCS}"
)
