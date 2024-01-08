libopencm3_add_library(
    NAME "stm32f3"
    ALIAS_NAME "stm32::f3"
    DEFINITIONS STM32F3
    PUBLIC_COMPILE_OPTIONS -mcpu=cortex-m4 -mthumb -mfloat-abi=hard -mfpu=fpv4-sp-d16
    PRIVATE_COMPILE_OPTIONS -Os
    VPATH "../../usb" "../common" "../"
    FILES
        adc.c adc_common_v2.c adc_common_v2_multi.c
        can.c
        crc_common_all.c crc_v2.c
        dac_common_all.c dac_common_v1.c
        desig_common_all.c desig_common_v1.c
        dma_common_l1f013.c
        exti_common_all.c
        flash.c flash_common_all.c flash_common_f.c
        gpio_common_all.c gpio_common_f0234.c
        i2c_common_v2.c
        iwdg_common_all.c
        opamp_common_all.c opamp_common_v1.c
        pwr_common_v1.c
        rcc.c rcc_common_all.c
        rtc_common_l1f024.c
        spi_common_all.c spi_common_v2.c
        timer_common_all.c timer_common_f0234.c
        usart_common_v2.c usart_common_all.c

        usb.c usb_control.c usb_standard.c usb_msc.c
        usb_hid.c
        usb_audio.c usb_cdc.c usb_midi.c
        st_usbfs_core.c st_usbfs_v1.c
)
