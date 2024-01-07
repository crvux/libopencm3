libopencm3_add_library(
    NAME "gd32f1x0"
    ALIAS_NAME "gd32::f1x0"
    DEFINITIONS GD32F1X0
    PUBLIC_COMPILE_OPTIONS -mcpu=cortex-m3 -mthumb 
    PRIVATE_COMPILE_OPTIONS -Os
    GENERATE_IRQ
    VPATH "../../stm32/common"
    FILES
        flash.c flash_common_all.c flash_common_f.c flash_common_f01.c
        gpio_common_all.c gpio_common_f0234.c
        rcc.c rcc_common_all.c
)
