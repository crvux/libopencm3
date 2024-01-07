libopencm3_add_library(
    NAME "efm32g"
    ALIAS_NAME "efm32::g"
    DEFINITIONS EFM32G
    PUBLIC_COMPILE_OPTIONS -mcpu=cortex-m3 -mthumb
    PRIVATE_COMPILE_OPTIONS -Os
    GENERATE_IRQ
)
