libopencm3_add_library(
    NAME "lpc43xx"
    ALIAS_NAME "lpc43xx::m4"
    DEFINITIONS LPC43XX LPC43XX_M4
    PUBLIC_COMPILE_OPTIONS -mcpu=cortex-m4 -mthumb -mfloat-abi=hard -mfpu=fpv4-sp-d16
    PRIVATE_COMPILE_OPTIONS -O2
    GENERATE_IRQ
    VPATH "../"
    FILES
        gpio.c
        scu.c
        i2c.c
        ssp.c
        uart.c
        timer.c
        ipc.c
)
