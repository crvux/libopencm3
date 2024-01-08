libopencm3_add_library(
    NAME "efm32hg"
    ALIAS_NAME "efm32::hg"
    DEFINITIONS EFM32HG
    PUBLIC_COMPILE_OPTIONS -mcpu=cortex-m0plus -mthumb
    PRIVATE_COMPILE_OPTIONS -Os
    VPATH "../../usb" "../common"
    FILES
        cmu.c
        gpio_common.c
        timer_common.c

        usb.c usb_control.c usb_standard.c usb_msc.c
        usb_hid.c
        usb_audio.c usb_cdc.c usb_midi.c
        usb_dwc_common.c usb_efm32hg.c
)
