set(LIB_NAME opencm3_lm4f)
set(FAMILY LM4F)
set(PATH_FRAG "lm4f")

set(USB_SRC_DIR "${LIBOPENCM3_CMAKE_SOURCE_DIR}/lib/usb")
set(TARGET_SRC_DIR "${LIBOPENCM3_CMAKE_SOURCE_DIR}/lib/${PATH_FRAG}")

add_library(${LIB_NAME} STATIC)
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
    "${TARGET_SRC_DIR}/gpio.c"
    "${TARGET_SRC_DIR}/rcc.c"
    "${TARGET_SRC_DIR}/systemcontrol.c"
    "${TARGET_SRC_DIR}/uart.c"

    "${USB_SRC_DIR}/usb.c" "${USB_SRC_DIR}/usb_control.c" "${USB_SRC_DIR}/usb_standard.c" "${USB_SRC_DIR}/usb_msc.c"
    "${USB_SRC_DIR}/usb_hid.c"
    "${USB_SRC_DIR}/usb_audio.c" "${USB_SRC_DIR}/usb_cdc.c" "${USB_SRC_DIR}/usb_midi.c"
    "${USB_SRC_DIR}/usb_lm4f.c"

    "${CM3_SRCS}"
)
