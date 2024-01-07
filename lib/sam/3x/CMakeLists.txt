libopencm3_add_library(
    NAME "sam3x"
    ALIAS_NAME "sam::3x"
    DEFINITIONS SAM3X
    PUBLIC_COMPILE_OPTIONS -mcpu=cortex-m3 -mthumb
    PRIVATE_COMPILE_OPTIONS -Os
    GENERATE_IRQ
    VPATH "../common"
    FILES
        gpio_common_all.c gpio_common_3a3u3x.c
        pmc.c
        usart_common_all.c usart_common_3.c
)
