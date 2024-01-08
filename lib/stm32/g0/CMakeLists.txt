libopencm3_add_library(
    NAME "stm32g0"
    ALIAS_NAME "stm32::g0"
    DEFINITIONS STM32G0
    PUBLIC_COMPILE_OPTIONS -mcpu=cortex-m0plus -mthumb
    PRIVATE_COMPILE_OPTIONS -Os
    VPATH "../common"
    FILES
        adc.c adc_common_v2.c
        crc_common_all.c
        dac_common_all.c dac_common_v1.c
        desig_common_all.c desig_common_v1.c
        dma_common_l1f013.c
        dmamux.c
        exti_common_all.c exti_common_v2.c
        flash.c flash_common_all.c
        gpio_common_all.c gpio_common_f0234.c
        i2c_common_v2.c
        iwdg_common_all.c
        lptimer_common_all.c
        pwr.c
        rcc.c rcc_common_all.c
        rng_common_v1.c
        spi_common_all.c spi_common_v2.c
        timer_common_all.c
        usart_common_all.c usart_common_v2.c
)