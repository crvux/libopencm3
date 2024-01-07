libopencm3_add_library(
    NAME "stm32l1"
    ALIAS_NAME "stm32::l1"
    DEFINITIONS STM32L1
    PUBLIC_COMPILE_OPTIONS -mcpu=cortex-m3 -mthumb
    PRIVATE_COMPILE_OPTIONS -Os
    GENERATE_IRQ
    VPATH "../../usb" "../common" "../"
    FILES
        adc.c adc_common_v1.c adc_common_v1_multi.c
        flash.c
        crc_common_all.c
        dac_common_all.c dac_common_v1.c
        desig_common_all.c desig.c
        dma_common_l1f013.c
        exti_common_all.c
        flash_common_all.c flash_common_l01.c
        gpio_common_all.c gpio_common_f0234.c
        i2c_common_v1.c
        iwdg_common_all.c
        lcd.c
        pwr_common_v1.c pwr_common_v2.c
        rcc.c rcc_common_all.c
        rtc_common_l1f024.c
        spi_common_all.c spi_common_v1.c spi_common_v1_frf.c
        timer.c timer_common_all.c
        usart_common_all.c usart_common_f124.c

        usb.c usb_control.c usb_standard.c usb_msc.c
        usb_hid.c
        usb_audio.c usb_cdc.c usb_midi.c
        st_usbfs_core.c st_usbfs_v1.c
)