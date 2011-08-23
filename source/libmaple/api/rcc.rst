.. highlight:: c
.. _libmaple-rcc:

``rcc.h``
=========

Reset and Clock Control (RCC) support.

.. contents:: Contents
   :local:

Types
-----

.. doxygenstruct:: rcc_reg_map
.. doxygenenum:: rcc_sysclk_src
.. doxygenenum:: rcc_pllsrc
.. doxygenenum:: rcc_pll_multiplier
.. doxygenenum:: rcc_clk_id
.. doxygenenum:: rcc_clk_domain
.. doxygenenum:: rcc_prescaler
.. doxygenenum:: rcc_adc_divider
.. doxygenenum:: rcc_apb1_divider
.. doxygenenum:: rcc_apb2_divider
.. doxygenenum:: rcc_ahb_divider

Devices
-------

None.

Functions
---------

.. doxygenfunction:: rcc_clk_init
.. doxygenfunction:: rcc_clk_enable
.. doxygenfunction:: rcc_reset_dev
.. doxygenfunction:: rcc_dev_clk
.. doxygenfunction:: rcc_set_prescaler

Register Map Base Pointers
--------------------------

.. doxygendefine:: RCC_BASE

Register Bit Definitions
------------------------

Clock control register
~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: RCC_CR_PLLRDY_BIT
.. doxygendefine:: RCC_CR_PLLON_BIT
.. doxygendefine:: RCC_CR_CSSON_BIT
.. doxygendefine:: RCC_CR_HSEBYP_BIT
.. doxygendefine:: RCC_CR_HSERDY_BIT
.. doxygendefine:: RCC_CR_HSEON_BIT
.. doxygendefine:: RCC_CR_HSIRDY_BIT
.. doxygendefine:: RCC_CR_HSION_BIT

.. doxygendefine:: RCC_CR_PLLRDY
.. doxygendefine:: RCC_CR_PLLON
.. doxygendefine:: RCC_CR_CSSON
.. doxygendefine:: RCC_CR_HSEBYP
.. doxygendefine:: RCC_CR_HSERDY
.. doxygendefine:: RCC_CR_HSEON
.. doxygendefine:: RCC_CR_HSICAL
.. doxygendefine:: RCC_CR_HSITRIM
.. doxygendefine:: RCC_CR_HSIRDY
.. doxygendefine:: RCC_CR_HSION

Clock configuration register
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: RCC_CFGR_USBPRE_BIT
.. doxygendefine:: RCC_CFGR_PLLXTPRE_BIT
.. doxygendefine:: RCC_CFGR_PLLSRC_BIT

.. doxygendefine:: RCC_CFGR_MCO
.. doxygendefine:: RCC_CFGR_USBPRE
.. doxygendefine:: RCC_CFGR_PLLMUL
.. doxygendefine:: RCC_CFGR_PLLXTPRE
.. doxygendefine:: RCC_CFGR_PLLSRC
.. doxygendefine:: RCC_CFGR_ADCPRE
.. doxygendefine:: RCC_CFGR_PPRE2
.. doxygendefine:: RCC_CFGR_PPRE1
.. doxygendefine:: RCC_CFGR_HPRE
.. doxygendefine:: RCC_CFGR_SWS
.. doxygendefine:: RCC_CFGR_SWS_PLL
.. doxygendefine:: RCC_CFGR_SWS_HSE
.. doxygendefine:: RCC_CFGR_SW
.. doxygendefine:: RCC_CFGR_SW_PLL
.. doxygendefine:: RCC_CFGR_SW_HSE

Clock interrupt register
~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: RCC_CIR_CSSC_BIT
.. doxygendefine:: RCC_CIR_PLLRDYC_BIT
.. doxygendefine:: RCC_CIR_HSERDYC_BIT
.. doxygendefine:: RCC_CIR_HSIRDYC_BIT
.. doxygendefine:: RCC_CIR_LSERDYC_BIT
.. doxygendefine:: RCC_CIR_LSIRDYC_BIT
.. doxygendefine:: RCC_CIR_PLLRDYIE_BIT
.. doxygendefine:: RCC_CIR_HSERDYIE_BIT
.. doxygendefine:: RCC_CIR_HSIRDYIE_BIT
.. doxygendefine:: RCC_CIR_LSERDYIE_BIT
.. doxygendefine:: RCC_CIR_LSIRDYIE_BIT
.. doxygendefine:: RCC_CIR_CSSF_BIT
.. doxygendefine:: RCC_CIR_PLLRDYF_BIT
.. doxygendefine:: RCC_CIR_HSERDYF_BIT
.. doxygendefine:: RCC_CIR_HSIRDYF_BIT
.. doxygendefine:: RCC_CIR_LSERDYF_BIT
.. doxygendefine:: RCC_CIR_LSIRDYF_BIT

.. doxygendefine:: RCC_CIR_CSSC
.. doxygendefine:: RCC_CIR_PLLRDYC
.. doxygendefine:: RCC_CIR_HSERDYC
.. doxygendefine:: RCC_CIR_HSIRDYC
.. doxygendefine:: RCC_CIR_LSERDYC
.. doxygendefine:: RCC_CIR_LSIRDYC
.. doxygendefine:: RCC_CIR_PLLRDYIE
.. doxygendefine:: RCC_CIR_HSERDYIE
.. doxygendefine:: RCC_CIR_HSIRDYIE
.. doxygendefine:: RCC_CIR_LSERDYIE
.. doxygendefine:: RCC_CIR_LSIRDYIE
.. doxygendefine:: RCC_CIR_CSSF
.. doxygendefine:: RCC_CIR_PLLRDYF
.. doxygendefine:: RCC_CIR_HSERDYF
.. doxygendefine:: RCC_CIR_HSIRDYF
.. doxygendefine:: RCC_CIR_LSERDYF
.. doxygendefine:: RCC_CIR_LSIRDYF

APB2 peripheral reset register
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: RCC_APB2RSTR_TIM11RST_BIT
.. doxygendefine:: RCC_APB2RSTR_TIM10RST_BIT
.. doxygendefine:: RCC_APB2RSTR_TIM9RST_BIT
.. doxygendefine:: RCC_APB2RSTR_ADC3RST_BIT
.. doxygendefine:: RCC_APB2RSTR_USART1RST_BIT
.. doxygendefine:: RCC_APB2RSTR_TIM8RST_BIT
.. doxygendefine:: RCC_APB2RSTR_SPI1RST_BIT
.. doxygendefine:: RCC_APB2RSTR_TIM1RST_BIT
.. doxygendefine:: RCC_APB2RSTR_ADC2RST_BIT
.. doxygendefine:: RCC_APB2RSTR_ADC1RST_BIT
.. doxygendefine:: RCC_APB2RSTR_IOPGRST_BIT
.. doxygendefine:: RCC_APB2RSTR_IOPFRST_BIT
.. doxygendefine:: RCC_APB2RSTR_IOPERST_BIT
.. doxygendefine:: RCC_APB2RSTR_IOPDRST_BIT
.. doxygendefine:: RCC_APB2RSTR_IOPCRST_BIT
.. doxygendefine:: RCC_APB2RSTR_IOPBRST_BIT
.. doxygendefine:: RCC_APB2RSTR_IOPARST_BIT
.. doxygendefine:: RCC_APB2RSTR_AFIORST_BIT

.. doxygendefine:: RCC_APB2RSTR_TIM11RST
.. doxygendefine:: RCC_APB2RSTR_TIM10RST
.. doxygendefine:: RCC_APB2RSTR_TIM9RST
.. doxygendefine:: RCC_APB2RSTR_ADC3RST
.. doxygendefine:: RCC_APB2RSTR_USART1RST
.. doxygendefine:: RCC_APB2RSTR_TIM8RST
.. doxygendefine:: RCC_APB2RSTR_SPI1RST
.. doxygendefine:: RCC_APB2RSTR_TIM1RST
.. doxygendefine:: RCC_APB2RSTR_ADC2RST
.. doxygendefine:: RCC_APB2RSTR_ADC1RST
.. doxygendefine:: RCC_APB2RSTR_IOPGRST
.. doxygendefine:: RCC_APB2RSTR_IOPFRST
.. doxygendefine:: RCC_APB2RSTR_IOPERST
.. doxygendefine:: RCC_APB2RSTR_IOPDRST
.. doxygendefine:: RCC_APB2RSTR_IOPCRST
.. doxygendefine:: RCC_APB2RSTR_IOPBRST
.. doxygendefine:: RCC_APB2RSTR_IOPARST
.. doxygendefine:: RCC_APB2RSTR_AFIORST

APB1 peripheral reset register
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: RCC_APB1RSTR_DACRST_BIT
.. doxygendefine:: RCC_APB1RSTR_PWRRST_BIT
.. doxygendefine:: RCC_APB1RSTR_BKPRST_BIT
.. doxygendefine:: RCC_APB1RSTR_CANRST_BIT
.. doxygendefine:: RCC_APB1RSTR_USBRST_BIT
.. doxygendefine:: RCC_APB1RSTR_I2C2RST_BIT
.. doxygendefine:: RCC_APB1RSTR_I2C1RST_BIT
.. doxygendefine:: RCC_APB1RSTR_UART5RST_BIT
.. doxygendefine:: RCC_APB1RSTR_UART4RST_BIT
.. doxygendefine:: RCC_APB1RSTR_USART3RST_BIT
.. doxygendefine:: RCC_APB1RSTR_USART2RST_BIT
.. doxygendefine:: RCC_APB1RSTR_SPI3RST_BIT
.. doxygendefine:: RCC_APB1RSTR_SPI2RST_BIT
.. doxygendefine:: RCC_APB1RSTR_WWDRST_BIT
.. doxygendefine:: RCC_APB1RSTR_TIM14RST_BIT
.. doxygendefine:: RCC_APB1RSTR_TIM13RST_BIT
.. doxygendefine:: RCC_APB1RSTR_TIM12RST_BIT
.. doxygendefine:: RCC_APB1RSTR_TIM7RST_BIT
.. doxygendefine:: RCC_APB1RSTR_TIM6RST_BIT
.. doxygendefine:: RCC_APB1RSTR_TIM5RST_BIT
.. doxygendefine:: RCC_APB1RSTR_TIM4RST_BIT
.. doxygendefine:: RCC_APB1RSTR_TIM3RST_BIT
.. doxygendefine:: RCC_APB1RSTR_TIM2RST_BIT

.. doxygendefine:: RCC_APB1RSTR_DACRST
.. doxygendefine:: RCC_APB1RSTR_PWRRST
.. doxygendefine:: RCC_APB1RSTR_BKPRST
.. doxygendefine:: RCC_APB1RSTR_CANRST
.. doxygendefine:: RCC_APB1RSTR_USBRST
.. doxygendefine:: RCC_APB1RSTR_I2C2RST
.. doxygendefine:: RCC_APB1RSTR_I2C1RST
.. doxygendefine:: RCC_APB1RSTR_UART5RST
.. doxygendefine:: RCC_APB1RSTR_UART4RST
.. doxygendefine:: RCC_APB1RSTR_USART3RST
.. doxygendefine:: RCC_APB1RSTR_USART2RST
.. doxygendefine:: RCC_APB1RSTR_SPI3RST
.. doxygendefine:: RCC_APB1RSTR_SPI2RST
.. doxygendefine:: RCC_APB1RSTR_WWDRST
.. doxygendefine:: RCC_APB1RSTR_TIM14RST
.. doxygendefine:: RCC_APB1RSTR_TIM13RST
.. doxygendefine:: RCC_APB1RSTR_TIM12RST
.. doxygendefine:: RCC_APB1RSTR_TIM7RST
.. doxygendefine:: RCC_APB1RSTR_TIM6RST
.. doxygendefine:: RCC_APB1RSTR_TIM5RST
.. doxygendefine:: RCC_APB1RSTR_TIM4RST
.. doxygendefine:: RCC_APB1RSTR_TIM3RST
.. doxygendefine:: RCC_APB1RSTR_TIM2RST

AHB peripheral clock enable register
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: RCC_AHBENR_SDIOEN_BIT
.. doxygendefine:: RCC_AHBENR_FSMCEN_BIT
.. doxygendefine:: RCC_AHBENR_CRCEN_BIT
.. doxygendefine:: RCC_AHBENR_FLITFEN_BIT
.. doxygendefine:: RCC_AHBENR_SRAMEN_BIT
.. doxygendefine:: RCC_AHBENR_DMA2EN_BIT
.. doxygendefine:: RCC_AHBENR_DMA1EN_BIT

.. doxygendefine:: RCC_AHBENR_SDIOEN
.. doxygendefine:: RCC_AHBENR_FSMCEN
.. doxygendefine:: RCC_AHBENR_CRCEN
.. doxygendefine:: RCC_AHBENR_FLITFEN
.. doxygendefine:: RCC_AHBENR_SRAMEN
.. doxygendefine:: RCC_AHBENR_DMA2EN
.. doxygendefine:: RCC_AHBENR_DMA1EN

APB2 peripheral clock enable register
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: RCC_APB2ENR_TIM11EN_BIT
.. doxygendefine:: RCC_APB2ENR_TIM10EN_BIT
.. doxygendefine:: RCC_APB2ENR_TIM9EN_BIT
.. doxygendefine:: RCC_APB2ENR_ADC3EN_BIT
.. doxygendefine:: RCC_APB2ENR_USART1EN_BIT
.. doxygendefine:: RCC_APB2ENR_TIM8EN_BIT
.. doxygendefine:: RCC_APB2ENR_SPI1EN_BIT
.. doxygendefine:: RCC_APB2ENR_TIM1EN_BIT
.. doxygendefine:: RCC_APB2ENR_ADC2EN_BIT
.. doxygendefine:: RCC_APB2ENR_ADC1EN_BIT
.. doxygendefine:: RCC_APB2ENR_IOPGEN_BIT
.. doxygendefine:: RCC_APB2ENR_IOPFEN_BIT
.. doxygendefine:: RCC_APB2ENR_IOPEEN_BIT
.. doxygendefine:: RCC_APB2ENR_IOPDEN_BIT
.. doxygendefine:: RCC_APB2ENR_IOPCEN_BIT
.. doxygendefine:: RCC_APB2ENR_IOPBEN_BIT
.. doxygendefine:: RCC_APB2ENR_IOPAEN_BIT
.. doxygendefine:: RCC_APB2ENR_AFIOEN_BIT

.. doxygendefine:: RCC_APB2ENR_TIM11EN
.. doxygendefine:: RCC_APB2ENR_TIM10EN
.. doxygendefine:: RCC_APB2ENR_TIM9EN
.. doxygendefine:: RCC_APB2ENR_ADC3EN
.. doxygendefine:: RCC_APB2ENR_USART1EN
.. doxygendefine:: RCC_APB2ENR_TIM8EN
.. doxygendefine:: RCC_APB2ENR_SPI1EN
.. doxygendefine:: RCC_APB2ENR_TIM1EN
.. doxygendefine:: RCC_APB2ENR_ADC2EN
.. doxygendefine:: RCC_APB2ENR_ADC1EN
.. doxygendefine:: RCC_APB2ENR_IOPGEN
.. doxygendefine:: RCC_APB2ENR_IOPFEN
.. doxygendefine:: RCC_APB2ENR_IOPEEN
.. doxygendefine:: RCC_APB2ENR_IOPDEN
.. doxygendefine:: RCC_APB2ENR_IOPCEN
.. doxygendefine:: RCC_APB2ENR_IOPBEN
.. doxygendefine:: RCC_APB2ENR_IOPAEN
.. doxygendefine:: RCC_APB2ENR_AFIOEN

APB1 peripheral clock enable register
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: RCC_APB1ENR_DACEN_BIT
.. doxygendefine:: RCC_APB1ENR_PWREN_BIT
.. doxygendefine:: RCC_APB1ENR_BKPEN_BIT
.. doxygendefine:: RCC_APB1ENR_CANEN_BIT
.. doxygendefine:: RCC_APB1ENR_USBEN_BIT
.. doxygendefine:: RCC_APB1ENR_I2C2EN_BIT
.. doxygendefine:: RCC_APB1ENR_I2C1EN_BIT
.. doxygendefine:: RCC_APB1ENR_UART5EN_BIT
.. doxygendefine:: RCC_APB1ENR_UART4EN_BIT
.. doxygendefine:: RCC_APB1ENR_USART3EN_BIT
.. doxygendefine:: RCC_APB1ENR_USART2EN_BIT
.. doxygendefine:: RCC_APB1ENR_SPI3EN_BIT
.. doxygendefine:: RCC_APB1ENR_SPI2EN_BIT
.. doxygendefine:: RCC_APB1ENR_WWDEN_BIT
.. doxygendefine:: RCC_APB1ENR_TIM14EN_BIT
.. doxygendefine:: RCC_APB1ENR_TIM13EN_BIT
.. doxygendefine:: RCC_APB1ENR_TIM12EN_BIT
.. doxygendefine:: RCC_APB1ENR_TIM7EN_BIT
.. doxygendefine:: RCC_APB1ENR_TIM6EN_BIT
.. doxygendefine:: RCC_APB1ENR_TIM5EN_BIT
.. doxygendefine:: RCC_APB1ENR_TIM4EN_BIT
.. doxygendefine:: RCC_APB1ENR_TIM3EN_BIT
.. doxygendefine:: RCC_APB1ENR_TIM2EN_BIT

.. doxygendefine:: RCC_APB1ENR_DACEN
.. doxygendefine:: RCC_APB1ENR_PWREN
.. doxygendefine:: RCC_APB1ENR_BKPEN
.. doxygendefine:: RCC_APB1ENR_CANEN
.. doxygendefine:: RCC_APB1ENR_USBEN
.. doxygendefine:: RCC_APB1ENR_I2C2EN
.. doxygendefine:: RCC_APB1ENR_I2C1EN
.. doxygendefine:: RCC_APB1ENR_UART5EN
.. doxygendefine:: RCC_APB1ENR_UART4EN
.. doxygendefine:: RCC_APB1ENR_USART3EN
.. doxygendefine:: RCC_APB1ENR_USART2EN
.. doxygendefine:: RCC_APB1ENR_SPI3EN
.. doxygendefine:: RCC_APB1ENR_SPI2EN
.. doxygendefine:: RCC_APB1ENR_WWDEN
.. doxygendefine:: RCC_APB1ENR_TIM14EN
.. doxygendefine:: RCC_APB1ENR_TIM13EN
.. doxygendefine:: RCC_APB1ENR_TIM12EN
.. doxygendefine:: RCC_APB1ENR_TIM7EN
.. doxygendefine:: RCC_APB1ENR_TIM6EN
.. doxygendefine:: RCC_APB1ENR_TIM5EN
.. doxygendefine:: RCC_APB1ENR_TIM4EN
.. doxygendefine:: RCC_APB1ENR_TIM3EN
.. doxygendefine:: RCC_APB1ENR_TIM2EN

Backup domain control register
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: RCC_BDCR_BDRST_BIT
.. doxygendefine:: RCC_BDCR_RTCEN_BIT
.. doxygendefine:: RCC_BDCR_LSEBYP_BIT
.. doxygendefine:: RCC_BDCR_LSERDY_BIT
.. doxygendefine:: RCC_BDCR_LSEON_BIT

.. doxygendefine:: RCC_BDCR_BDRST
.. doxygendefine:: RCC_BDCR_RTCEN
.. doxygendefine:: RCC_BDCR_RTCSEL
.. doxygendefine:: RCC_BDCR_RTCSEL_NONE
.. doxygendefine:: RCC_BDCR_RTCSEL_LSE
.. doxygendefine:: RCC_BDCR_RTCSEL_HSE
.. doxygendefine:: RCC_BDCR_LSEBYP
.. doxygendefine:: RCC_BDCR_LSERDY
.. doxygendefine:: RCC_BDCR_LSEON

Control/status register
~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: RCC_CSR_LPWRRSTF_BIT
.. doxygendefine:: RCC_CSR_WWDGRSTF_BIT
.. doxygendefine:: RCC_CSR_IWDGRSTF_BIT
.. doxygendefine:: RCC_CSR_SFTRSTF_BIT
.. doxygendefine:: RCC_CSR_PORRSTF_BIT
.. doxygendefine:: RCC_CSR_PINRSTF_BIT
.. doxygendefine:: RCC_CSR_RMVF_BIT
.. doxygendefine:: RCC_CSR_LSIRDY_BIT
.. doxygendefine:: RCC_CSR_LSION_BIT

.. doxygendefine:: RCC_CSR_LPWRRSTF
.. doxygendefine:: RCC_CSR_WWDGRSTF
.. doxygendefine:: RCC_CSR_IWDGRSTF
.. doxygendefine:: RCC_CSR_SFTRSTF
.. doxygendefine:: RCC_CSR_PORRSTF
.. doxygendefine:: RCC_CSR_PINRSTF
.. doxygendefine:: RCC_CSR_RMVF
.. doxygendefine:: RCC_CSR_LSIRDY
.. doxygendefine:: RCC_CSR_LSION
