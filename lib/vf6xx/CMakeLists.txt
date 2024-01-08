libopencm3_add_library(
    NAME "vf6xx"
    ALIAS_NAME "vf6xx"
    DEFINITIONS VF6XX
    PUBLIC_COMPILE_OPTIONS -mcpu=cortex-m4 -mthumb -mfloat-abi=hard -mfpu=fpv4-sp-d16
    PRIVATE_COMPILE_OPTIONS -Os
    FILES
        ccm.c
        gpio.c
        iomuxc.c
        uart.c
)
