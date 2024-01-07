set(LIB_NAME opencm3_efm32hg)
set(FAMILY EFM32HG)
set(PATH_FRAG "efm32/hg")

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
    ${GCC_WARN_OPTIONS}
    -mcpu=cortex-m0plus -mthumb
    -Os -fno-common -ffunction-sections -fdata-sections
)
# FIXME include only needed!
target_include_directories(${LIB_NAME} PRIVATE
    "${LIBOPENCM3_CMAKE_SOURCE_DIR}/include/"
    "${CMAKE_BINARY_DIR}/include/"
    "${CMAKE_BINARY_DIR}/lib/stm32/"
)
target_sources(${LIB_NAME} PRIVATE
    "${TARGET_SRC_DIR}/cmu.c"
    "${COMMON_SRC_DIR}/gpio_common.c"
    "${COMMON_SRC_DIR}/timer_common.c"

    "${USB_SRC_DIR}/usb.c" "${USB_SRC_DIR}/usb_control.c" "${USB_SRC_DIR}/usb_standard.c" "${USB_SRC_DIR}/usb_msc.c"
    "${USB_SRC_DIR}/usb_hid.c"
    "${USB_SRC_DIR}/usb_audio.c" "${USB_SRC_DIR}/usb_cdc.c" "${USB_SRC_DIR}/usb_midi.c"
    "${USB_SRC_DIR}/usb_dwc_common.c" "${USB_SRC_DIR}/usb_efm32hg.c"

    "${CM3_SRCS}"
)
