set(LIB_NAME opencm3_swm050)
set(FAMILY SWM050)
set(PATH_FRAG "swm050")

set(COMMON_SRC_DIR "${LIBOPENCM3_CMAKE_SOURCE_DIR}/lib/swm050")

generate_irq(${PATH_FRAG})
add_library(${LIB_NAME} STATIC
    "${CMAKE_BINARY_DIR}/include/libopencmsis/${PATH_FRAG}/irqhandlers.h"
    "${CMAKE_BINARY_DIR}/include/libopencm3/${PATH_FRAG}/nvic.h"
)
target_compile_definitions(${LIB_NAME} PUBLIC ${FAMILY})
target_compile_options(${LIB_NAME} PRIVATE
    ${GCC_WARN_OPTIONS}
    -mcpu=cortex-m0 -mthumb
    -Os -fno-common -ffunction-sections -fdata-sections
)
# FIXME include only needed!
target_include_directories(${LIB_NAME} PRIVATE
    "${LIBOPENCM3_CMAKE_SOURCE_DIR}/include/"
    "${CMAKE_BINARY_DIR}/include/"
    "${CMAKE_BINARY_DIR}/lib/stm32/"
)
target_sources(${LIB_NAME} PRIVATE
    "${COMMON_SRC_DIR}/clk.c"
    "${COMMON_SRC_DIR}/flash.c"
    "${COMMON_SRC_DIR}/gpio.c"
    "${COMMON_SRC_DIR}/pwr.c"
    "${COMMON_SRC_DIR}/syscon.c"
    "${COMMON_SRC_DIR}/timer.c"
    "${COMMON_SRC_DIR}/wdt.c"

    "${CM3_SRCS}"
)
