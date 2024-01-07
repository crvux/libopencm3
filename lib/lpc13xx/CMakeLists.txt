libopencm3_add_library(
    NAME "lpc13xx"
    ALIAS_NAME "lpc13xx"
    DEFINITIONS LPC13XX
    PUBLIC_COMPILE_OPTIONS -mcpu=cortex-m3 -mthumb
    PRIVATE_COMPILE_OPTIONS -Os
    GENERATE_IRQ
    FILES
        gpio.c
)
