set(LIB_NAME opencm3_vf6xx)
set(FAMILY VF6XX)
set(PATH_FRAG "vf6xx")

set(COMMON_SRC_DIR "${LIBOPENCM3_CMAKE_SOURCE_DIR}/lib/vf6xx")

generate_irq(${PATH_FRAG})
add_library(${LIB_NAME} STATIC
    "${CMAKE_BINARY_DIR}/include/libopencmsis/${PATH_FRAG}/irqhandlers.h"
    "${CMAKE_BINARY_DIR}/include/libopencm3/${PATH_FRAG}/nvic.h"
)
target_compile_definitions(${LIB_NAME} PUBLIC ${FAMILY})
target_compile_options(${LIB_NAME} PRIVATE
    -Os -Wall -Wextra -Wimplicit-function-declaration
    -Wredundant-decls -Wmissing-prototypes -Wstrict-prototypes
    -Wundef -Wshadow
    -fno-common
    -mcpu=cortex-m4 -mthumb -mfloat-abi=hard -mfpu=fpv4-sp-d16 -Wstrict-prototypes
    -ffunction-sections -fdata-sections
)
# FIXME include only needed!
target_include_directories(${LIB_NAME} PRIVATE
    "${LIBOPENCM3_CMAKE_SOURCE_DIR}/include/"
    "${CMAKE_BINARY_DIR}/include/"
    "${CMAKE_BINARY_DIR}/lib/stm32/"
)
target_sources(${LIB_NAME} PRIVATE
    "${COMMON_SRC_DIR}/ccm.c"
    "${COMMON_SRC_DIR}/gpio.c"
    "${COMMON_SRC_DIR}/iomuxc.c"
    "${COMMON_SRC_DIR}/uart.c"

    "${CM3_SRCS}"
)
