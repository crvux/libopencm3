libopencm3_add_library(
    NAME "lm4f"
    ALIAS_NAME "lm4f"
    DEFINITIONS LM4F
    PUBLIC_COMPILE_OPTIONS -mcpu=cortex-m4 -mthumb -mfloat-abi=hard -mfpu=fpv4-sp-d16
    PRIVATE_COMPILE_OPTIONS -Os
    VPATH "../usb"
    FILES
        gpio.c
        rcc.c
        systemcontrol.c
        uart.c

        usb.c usb_control.c usb_standard.c usb_msc.c
        usb_hid.c
        usb_audio.c usb_cdc.c usb_midi.c
        usb_lm4f.c
)
