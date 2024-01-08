libopencm3_add_library(
    NAME "lm3s"
    ALIAS_NAME "lm3s"
    DEFINITIONS LM3S
    PUBLIC_COMPILE_OPTIONS -mcpu=cortex-m3 -mthumb
    PRIVATE_COMPILE_OPTIONS -Os
    FILES
        gpio.c
        rcc.c
        usart.c
)
