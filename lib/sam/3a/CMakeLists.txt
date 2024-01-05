set(LIB_NAME opencm3_sam3a)
set(FAMILY SAM3A)
set(PATH_FRAG "sam/3a")

set(COMMON_SRC_DIR "${LIBOPENCM3_CMAKE_SOURCE_DIR}/lib/sam/common")

generate_irq(${PATH_FRAG})
add_library(${LIB_NAME} STATIC
    "${CMAKE_BINARY_DIR}/include/libopencmsis/${PATH_FRAG}/irqhandlers.h"
    "${CMAKE_BINARY_DIR}/include/libopencm3/${PATH_FRAG}/nvic.h"
)
target_compile_definitions(${LIB_NAME} PUBLIC ${FAMILY})
target_compile_options(${LIB_NAME} PRIVATE
    -Os -Wall -Wextra -fno-common
    -mcpu=cortex-m3 -mthumb -Wstrict-prototypes
    -ffunction-sections -fdata-sections
)
# FIXME include only needed!
target_include_directories(${LIB_NAME} PRIVATE
    "${LIBOPENCM3_CMAKE_SOURCE_DIR}/include/"
    "${CMAKE_BINARY_DIR}/include/"
    "${CMAKE_BINARY_DIR}/lib/stm32/"
)
target_sources(${LIB_NAME} PRIVATE
    "${COMMON_SRC_DIR}/gpio_common_all.c" "${COMMON_SRC_DIR}/gpio_common_3a3u3x.c"
    "${COMMON_SRC_DIR}/pmc.c"
    "${COMMON_SRC_DIR}/usart_common_all.c" "${COMMON_SRC_DIR}/usart_common_3.c"

    "${CM3_SRCS}"
)
