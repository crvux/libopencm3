libopencm3_add_library(
    NAME "efm32tg"
    ALIAS_NAME "efm32::tg"
    DEFINITIONS EFM32TG
    PUBLIC_COMPILE_OPTIONS -mcpu=cortex-m3 -mthumb
    PRIVATE_COMPILE_OPTIONS -Os
    GENERATE_IRQ
)
