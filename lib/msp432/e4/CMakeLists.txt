libopencm3_add_library(
    NAME "msp432e4"
    ALIAS_NAME "msp432::e4"
    DEFINITIONS MSP432E4
    PUBLIC_COMPILE_OPTIONS -mcpu=cortex-m4 -mthumb -mfloat-abi=hard -mfpu=fpv4-sp-d16
    PRIVATE_COMPILE_OPTIONS -Os
    FILES
        gpio.c
        systemcontrol.c
)
