libopencm3_add_library(
    NAME "swm050"
    ALIAS_NAME "swm050"
    DEFINITIONS SWM050
    PUBLIC_COMPILE_OPTIONS -mcpu=cortex-m0 -mthumb
    PRIVATE_COMPILE_OPTIONS -Os
    FILES
        clk.c
        flash.c
        gpio.c
        pwr.c
        syscon.c
        timer.c
        wdt.c
)
