libopencm3_add_library(
    NAME "stm32f2"
    ALIAS_NAME "stm32::f2"
    DEFINITIONS STM32F2
    PUBLIC_COMPILE_OPTIONS -mcpu=cortex-m3 -mthumb
    PRIVATE_COMPILE_OPTIONS -Os
    VPATH "../../usb" "../common"
    FILES
        crc_common_all.c
        crypto_common_f24.c
        dac_common_all.c dac_common_v1.c
        desig_common_all.c desig_common_v1.c
        dma_common_f24.c
        exti_common_all.c
        flash.c flash_common_all.c flash_common_f.c flash_common_f24.c flash_common_idcache.c
        gpio_common_all.c gpio_common_f0234.c
        hash_common_f24.c
        i2c_common_v1.c
        iwdg_common_all.c
        rcc.c rcc_common_all.c
        rng_common_v1.c
        rtc_common_l1f024.c
        spi_common_all.c spi_common_v1.c spi_common_v1_frf.c
        timer_common_all.c timer_common_f0234.c timer_common_f24.c
        usart_common_all.c usart_common_f124.c

        usb.c usb_standard.c usb_control.c usb_msc.c
        usb_hid.c
        usb_audio.c usb_cdc.c usb_midi.c
        usb_dwc_common.c usb_f107.c usb_f207.c
)
