libopencm3_add_library(
    NAME "sam3a"
    ALIAS_NAME "sam::3a"
    DEFINITIONS SAM3A
    PUBLIC_COMPILE_OPTIONS -mcpu=cortex-m3 -mthumb 
    PRIVATE_COMPILE_OPTIONS -Os
    VPATH "../common"
    FILES
        gpio_common_all.c gpio_common_3a3u3x.c
        pmc.c
        usart_common_all.c usart_common_3.c
)
