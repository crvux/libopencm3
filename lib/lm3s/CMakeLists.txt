set(LIB_NAME opencm3_lm3s)
set(FAMILY LM3S)
set(PATH_FRAG "lm3s")

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
    "${CMAKE_BINARY_DIR}/lib/lm3s/"
)
target_sources(${LIB_NAME} PRIVATE
    "${TARGET_SRC_DIR}/gpio.c"
    "${TARGET_SRC_DIR}/rcc.c"
    "${TARGET_SRC_DIR}/usart.c"

    "${CM3_SRCS}"
)
