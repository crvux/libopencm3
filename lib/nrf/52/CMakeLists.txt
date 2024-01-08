libopencm3_add_library(
    NAME "nrf52"
    ALIAS_NAME "nrf::52"
    DEFINITIONS NRF52
    PUBLIC_COMPILE_OPTIONS -mcpu=cortex-m4 -mthumb -mfloat-abi=hard -mfpu=fpv4-sp-d16
    PRIVATE_COMPILE_OPTIONS -Os
    VPATH "../common"
    FILES
        clock_common.c
        gpio.c
        i2c.c i2c_common.c
        ppi.c
        radio_common.c
        rtc.c
        timer.c
        uart.c
)
