libopencm3_add_library(
    NAME "stm32f1"
    ALIAS_NAME "stm32::f1"
    DEFINITIONS STM32F1
    PUBLIC_COMPILE_OPTIONS -mcpu=cortex-m3 -mthumb
    PRIVATE_COMPILE_OPTIONS -Os
    VPATH "../../usb" "../../ethernet" "../common" "../"
    FILES
        adc.c adc_common_v1.c
        can.c
        crc_common_all.c
        dac_common_all.c dac_common_v1.c
        desig_common_all.c desig_common_v1.c
        dma_common_l1f013.c
        exti_common_all.c
        flash.c flash_common_all.c flash_common_f.c flash_common_f01.c
        gpio.c gpio_common_all.c
        i2c_common_v1.c
        iwdg_common_all.c
        pwr_common_v1.c
        rcc.c rcc_common_all.c
        rtc.c
        spi_common_all.c spi_common_v1.c
        timer.c timer_common_all.c
        usart_common_all.c usart_common_f124.c

        mac.c mac_stm32fxx7.c
        phy.c phy_ksz80x1.c

        usb.c usb_control.c usb_standard.c usb_msc.c
        usb_hid.c
        usb_audio.c usb_cdc.c usb_midi.c
        usb_dwc_common.c usb_f107.c
        st_usbfs_core.c st_usbfs_v1.c
)
