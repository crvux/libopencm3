libopencm3_add_library(
    NAME "stm32l4"
    ALIAS_NAME "stm32::l4"
    DEFINITIONS STM32L4
    PUBLIC_COMPILE_OPTIONS -mcpu=cortex-m4 -mthumb -mfloat-abi=hard -mfpu=fpv4-sp-d16 
    PRIVATE_COMPILE_OPTIONS -Os
    GENERATE_IRQ
    VPATH "../../usb" "../common" "../"
    FILES
        adc.c adc_common_v2.c adc_common_v2_multi.c
        can.c
        crc_common_all.c crc_v2.c
        crs_common_all.c
        dac_common_all.c dac_common_v1.c
        dma_common_l1f013.c dma_common_csel.c
        exti_common_all.c
        flash.c flash_common_all.c flash_common_f.c flash_common_idcache.c
        gpio_common_all.c gpio_common_f0234.c
        i2c_common_v2.c
        iwdg_common_all.c
        lptimer_common_all.c
        pwr.c
        rcc.c rcc_common_all.c
        rng_common_v1.c
        rtc_common_l1f024.c
        spi_common_all.c spi_common_v2.c
        timer_common_all.c
        usart_common_all.c usart_common_v2.c
        quadspi_common_v1.c

        usb.c usb_control.c usb_standard.c usb_msc.c
        usb_hid.c
        usb_audio.c usb_cdc.c usb_midi.c
        st_usbfs_core.c st_usbfs_v2.c
        usb_dwc_common.c usb_f107.c
)