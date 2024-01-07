libopencm3_add_library(
    NAME "stm32h7"
    ALIAS_NAME "stm32::h7"
    DEFINITIONS STM32H7
    PUBLIC_COMPILE_OPTIONS -mcpu=cortex-m7 -mthumb -mfloat-abi=hard -mfpu=fpv5-d16
    PRIVATE_COMPILE_OPTIONS -Os
    GENERATE_IRQ
    VPATH "../common"
    FILES
        dac_common_all.c dac_common_v2.c
        exti_common_all.c
        fdcan.c fdcan_common.c
        flash_common_all.c flash_common_f.c flash_common_f24.c
        fmc_common_f47.c
        gpio_common_all.c gpio_common_f0234.c
        pwr.c rcc.c
        rcc_common_all.c
        rng_common_v1.c
        spi_common_all.c spi_common_v2.c
        timer_common_all.c
        usart_common_all.c usart_common_v2.c usart_common_fifos.c
        quadspi_common_v1.c
)