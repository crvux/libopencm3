libopencm3_add_library(
    NAME "sam4l"
    ALIAS_NAME "sam::4l"
    DEFINITIONS SAM4L
    PUBLIC_COMPILE_OPTIONS -mcpu=cortex-m4 -mthumb -msoft-float
    PRIVATE_COMPILE_OPTIONS -Os
    VPATH "../common"
    FILES
        adcife.c
        gpio.c
        pm.c
        scif.c
        usart_common_all.c usart.c
)
