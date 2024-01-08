libopencm3_add_library(
    NAME "samd"
    ALIAS_NAME "sam::d"
    DEFINITIONS SAMD
    PUBLIC_COMPILE_OPTIONS -mcpu=cortex-m0plus -mthumb
    PRIVATE_COMPILE_OPTIONS -Os
    FILES
        port.c
)
