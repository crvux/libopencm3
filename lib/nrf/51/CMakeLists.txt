libopencm3_add_library(
    NAME "nrf51"
    ALIAS_NAME "nrf::51"
    DEFINITIONS NRF51
    PUBLIC_COMPILE_OPTIONS -mcpu=cortex-m0 -mthumb -msoft-float
    PRIVATE_COMPILE_OPTIONS -Os
    GENERATE_IRQ
    VPATH "../common"
    FILES
        clock_common.c clock.c
        gpio.c
        i2c_common.c
        ppi.c
        rtc.c
        radio_common.c radio.c
        timer.c
        uart.c
)
