libopencm3_add_library(
    NAME "stm32f4"
    ALIAS_NAME "stm32::f4"
    DEFINITIONS STM32F4
    PUBLIC_COMPILE_OPTIONS -mcpu=cortex-m4 -mthumb -mfloat-abi=hard -mfpu=fpv4-sp-d16
    PRIVATE_COMPILE_OPTIONS -Os
    GENERATE_IRQ
    VPATH "../../usb" "../../ethernet" "../common" "../"
    FILES
        adc_common_v1.c adc_common_v1_multi.c adc_common_f47.c
        can.c
        crc_common_all.c
        crypto_common_f24.c crypto.c
        dac_common_all.c dac_common_v1.c
        dcmi_common_f47.c
        desig_common_all.c desig_common_v1.c
        dma_common_f24.c
        dma2d_common_f47.c
        dsi_common_f47.c
        exti_common_all.c
        flash.c flash_common_all.c flash_common_f.c flash_common_f24.c
        flash_common_idcache.c
        fmc_common_f47.c
        gpio_common_all.c gpio_common_f0234.c
        hash_common_f24.c
        i2c_common_v1.c
        iwdg_common_all.c
        lptimer_common_all.c
        ltdc_common_f47.c
        pwr_common_v1.c pwr.c
        rcc_common_all.c rcc.c
        rng_common_v1.c
        rtc_common_l1f024.c rtc.c
        spi_common_all.c spi_common_v1.c spi_common_v1_frf.c
        timer_common_all.c timer_common_f0234.c timer_common_f24.c
        usart_common_all.c usart_common_f124.c
        quadspi_common_v1.c

        usb.c usb_standard.c usb_control.c usb_msc.c
        usb_hid.c
        usb_audio.c usb_cdc.c usb_midi.c
        usb_dwc_common.c usb_f107.c usb_f207.c

        mac.c phy.c mac_stm32fxx7.c phy_ksz80x1.c
)
