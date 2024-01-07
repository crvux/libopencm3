set(LIB_NAME opencm3_gd32f1x0)
set(FAMILY GD32F1X0)
set(PATH_FRAG "gd32/f1x0")

set(COMMON_SRC_DIR "${LIBOPENCM3_CMAKE_SOURCE_DIR}/lib/gd32/common")
set(COMMON_STM32_SRC_DIR "${LIBOPENCM3_CMAKE_SOURCE_DIR}/lib/stm32/common")
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
    -mcpu=cortex-m3 -mthumb
    -Os -fno-common -ffunction-sections -fdata-sections
)
# FIXME include only needed!
target_include_directories(${LIB_NAME} PRIVATE
    "${LIBOPENCM3_CMAKE_SOURCE_DIR}/include/"
    "${CMAKE_BINARY_DIR}/include/"
    "${CMAKE_BINARY_DIR}/lib/stm32/"
)
target_sources(${LIB_NAME} PRIVATE
    "${TARGET_SRC_DIR}/flash.c" "${COMMON_STM32_SRC_DIR}/flash_common_all.c"
    "${COMMON_STM32_SRC_DIR}/flash_common_f.c" "${COMMON_STM32_SRC_DIR}/flash_common_f01.c"
    "${COMMON_STM32_SRC_DIR}/gpio_common_all.c" "${COMMON_STM32_SRC_DIR}/gpio_common_f0234.c"
    "${TARGET_SRC_DIR}/rcc.c" "${COMMON_STM32_SRC_DIR}/rcc_common_all.c"

    "${CM3_SRCS}"
)
