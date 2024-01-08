libopencm3_add_library(
    NAME "efm32gg"
    ALIAS_NAME "efm32::gg"
    DEFINITIONS EFM32GG
    PUBLIC_COMPILE_OPTIONS -mcpu=cortex-m3 -mthumb
    PRIVATE_COMPILE_OPTIONS -Os
)
