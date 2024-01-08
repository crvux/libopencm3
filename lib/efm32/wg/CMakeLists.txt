libopencm3_add_library(
    NAME "efm32wg"
    ALIAS_NAME "efm32::wg"
    DEFINITIONS EFM32WG
    PUBLIC_COMPILE_OPTIONS -mcpu=cortex-m4 -mthumb -mfloat-abi=hard -mfpu=fpv4-sp-d16
    PRIVATE_COMPILE_OPTIONS -Os
    VPATH "../../usb" "../common"
    FILES
        acmp_common.c
        adc_common.c
        burtc_common.c
        cmu_common.c
        dac_common.c
        dma_common.c
        emu_common.c
        gpio_common.c
        i2c_common.c
        letimer_common.c
        msc_common.c
        prs_common.c
        rmu_common.c
        rtc_common.c
        timer_common.c
        usart_common.c
        wdog_common.c

        usb.c usb_control.c usb_standard.c usb_msc.c
        usb_hid.c
        usb_audio.c usb_cdc.c usb_midi.c
        usb_efm32.c
)
