libopencm3_add_library(
    NAME "lpc17xx"
    ALIAS_NAME "lpc17xx"
    DEFINITIONS LPC17XX
    PUBLIC_COMPILE_OPTIONS -mcpu=cortex-m3 -mthumb
    PRIVATE_COMPILE_OPTIONS -Os
    FILES
        gpio.c
        pwr.c
)
