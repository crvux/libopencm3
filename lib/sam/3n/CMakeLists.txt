libopencm3_add_library(
    NAME "sam3n"
    ALIAS_NAME "sam::3n"
    DEFINITIONS SAM3N
    PUBLIC_COMPILE_OPTIONS -mcpu=cortex-m3 -mthumb
    PRIVATE_COMPILE_OPTIONS -Os
    VPATH "../common"
    FILES
        gpio_common_all.c gpio_common_3n3s.c
        pmc.c
        usart_common_all.c usart_common_3.c
)
