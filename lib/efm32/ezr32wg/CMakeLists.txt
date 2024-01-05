set(LIB_NAME opencm3_ezr32wg)
set(FAMILY EZR32WG)
set(PATH_FRAG "efm32/ezr32wg")

set(COMMON_SRC_DIR "${LIBOPENCM3_CMAKE_SOURCE_DIR}/lib/efm32/common")
set(USB_SRC_DIR "${LIBOPENCM3_CMAKE_SOURCE_DIR}/lib/usb")
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
    -mcpu=cortex-m4 -mthumb -Wstrict-prototypes
    -ffunction-sections -fdata-sections
    -mfloat-abi=hard -mfpu=fpv4-sp-d16
)
# FIXME include only needed!
target_include_directories(${LIB_NAME} PRIVATE
    "${LIBOPENCM3_CMAKE_SOURCE_DIR}/include/"
    "${CMAKE_BINARY_DIR}/include/"
    "${CMAKE_BINARY_DIR}/lib/stm32/"
)
target_sources(${LIB_NAME} PRIVATE
    "${COMMON_SRC_DIR}/acmp_common.c"
    "${COMMON_SRC_DIR}/adc_common.c"
    "${COMMON_SRC_DIR}/burtc_common.c"
    "${COMMON_SRC_DIR}/cmu_common.c"
    "${COMMON_SRC_DIR}/dac_common.c"
    "${COMMON_SRC_DIR}/dma_common.c"
    "${COMMON_SRC_DIR}/emu_common.c"
    "${COMMON_SRC_DIR}/gpio_common.c"
    "${COMMON_SRC_DIR}/i2c_common.c"
    "${COMMON_SRC_DIR}/letimer_common.c"
    "${COMMON_SRC_DIR}/msc_common.c"
    "${COMMON_SRC_DIR}/prs_common.c"
    "${COMMON_SRC_DIR}/rmu_common.c"
    "${COMMON_SRC_DIR}/rtc_common.c"
    "${COMMON_SRC_DIR}/timer_common.c"
    "${COMMON_SRC_DIR}/usart_common.c"
    "${COMMON_SRC_DIR}/wdog_common.c"

    "${USB_SRC_DIR}/usb.c" "${USB_SRC_DIR}/usb_control.c" "${USB_SRC_DIR}/usb_standard.c" "${USB_SRC_DIR}/usb_msc.c"
    "${USB_SRC_DIR}/usb_hid.c"
    "${USB_SRC_DIR}/usb_audio.c" "${USB_SRC_DIR}/usb_cdc.c" "${USB_SRC_DIR}/usb_midi.c"
    "${USB_SRC_DIR}/usb_efm32.c"

    "${CM3_SRCS}"
)
