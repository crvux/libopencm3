libopencm3_add_library(
    NAME "lpc43xx_m0"
    ALIAS_NAME "lpc43xx::m0"
    DEFINITIONS LPC43XX LPC43XX_M0
    PUBLIC_COMPILE_OPTIONS -mcpu=cortex-m0 -mthumb
    PRIVATE_COMPILE_OPTIONS -O2
    VPATH "../"
    FILES
        gpio.c
        scu.c
        i2c.c
        ssp.c
        uart.c
        timer.c
)
