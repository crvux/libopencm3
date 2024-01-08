libopencm3_add_library(
    NAME "stm32g4"
    ALIAS_NAME "stm32::g4"
    DEFINITIONS STM32G4
    PUBLIC_COMPILE_OPTIONS -mcpu=cortex-m4 -mthumb -mfloat-abi=hard -mfpu=fpv4-sp-d16
    PRIVATE_COMPILE_OPTIONS -Os
    VPATH "../../usb" "../common" "../"
    FILES
        adc.c adc_common_v2.c adc_common_v2_multi.c
        cordic_common_v1.c
        crs_common_all.c
        crc_common_all.c crc_v2.c
        dac_common_all.c dac_common_v2.c
        dma_common_l1f013.c
        dmamux.c
        fdcan.c fdcan_common.c
        flash.c flash_common_all.c flash_common_f.c flash_common_idcache.c
        gpio_common_all.c gpio_common_f0234.c
        i2c_common_v2.c
        opamp_common_all.c opamp_common_v2.c
        pwr.c
        rcc.c rcc_common_all.c
        rng_common_v1.c
        spi_common_all.c spi_common_v2.c
        timer_common_all.c timer_common_f0234.c
        quadspi_common_v1.c
        usart_common_v2.c usart_common_all.c

        usb.c usb_control.c usb_standard.c
        usb_audio.c
        usb_cdc.c
        usb_hid.c
        usb_midi.c
        usb_msc.c
        st_usbfs_core.c st_usbfs_v2.c
)