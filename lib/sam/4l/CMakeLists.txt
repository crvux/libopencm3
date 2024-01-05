set(LIB_NAME opencm3_sam4l)
set(FAMILY SAM4L)
set(PATH_FRAG "sam/4l")

set(COMMON_SRC_DIR "${LIBOPENCM3_CMAKE_SOURCE_DIR}/lib/sam/common")
set(TARGET_SRC_DIR "${LIBOPENCM3_CMAKE_SOURCE_DIR}/lib/sam/4l")

generate_irq(${PATH_FRAG})
add_library(${LIB_NAME} STATIC
    "${CMAKE_BINARY_DIR}/include/libopencmsis/${PATH_FRAG}/irqhandlers.h"
    "${CMAKE_BINARY_DIR}/include/libopencm3/${PATH_FRAG}/nvic.h"
)
target_compile_definitions(${LIB_NAME} PUBLIC ${FAMILY})
target_compile_options(${LIB_NAME} PRIVATE
    -Os -Wall -Wextra -fno-common
    -mcpu=cortex-m4 -mthumb -msoft-float -Wstrict-prototypes
    -ffunction-sections -fdata-sections
)
# FIXME include only needed!
target_include_directories(${LIB_NAME} PRIVATE
    "${LIBOPENCM3_CMAKE_SOURCE_DIR}/include/"
    "${CMAKE_BINARY_DIR}/include/"
    "${CMAKE_BINARY_DIR}/lib/stm32/"
)
target_sources(${LIB_NAME} PRIVATE
    "${TARGET_SRC_DIR}/adcife.c"
    "${TARGET_SRC_DIR}/gpio.c"
    "${TARGET_SRC_DIR}/pm.c"
    "${TARGET_SRC_DIR}/scif.c"
    "${COMMON_SRC_DIR}/usart_common_all.c" "${TARGET_SRC_DIR}/usart.c"

    "${CM3_SRCS}"
)
