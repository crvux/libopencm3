libopencm3_add_library(
    NAME "pac55xx"
    ALIAS_NAME "pac55xx"
    DEFINITIONS PAC55XX
    PUBLIC_COMPILE_OPTIONS -mcpu=cortex-m4 -mthumb -mfloat-abi=hard -mfpu=fpv4-sp-d16
    PRIVATE_COMPILE_OPTIONS -Os
    FILES
        can.c
        ccs.c
        gpio.c
        memctl.c
        usart.c
)
