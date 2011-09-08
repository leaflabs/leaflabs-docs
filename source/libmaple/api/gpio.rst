.. highlight:: c
.. _libmaple-gpio:

``gpio.h``
==========

General Purpose Input/Output (GPIO) port and Alternate Function
Input/Output (AFIO) support.

.. contents:: Contents
   :local:

Types
-----

.. doxygenstruct:: gpio_reg_map
.. doxygenstruct:: gpio_dev
.. doxygenenum:: gpio_pin_mode

.. doxygenstruct:: afio_reg_map
.. doxygenenum:: afio_exti_port
.. doxygenenum:: afio_exti_num
.. doxygenenum:: afio_remap_peripheral
.. doxygenenum:: afio_debug_cfg

Devices
-------

.. doxygenvariable:: GPIOA
.. doxygenvariable:: GPIOB
.. doxygenvariable:: GPIOC
.. doxygenvariable:: GPIOD
.. doxygenvariable:: GPIOE
.. doxygenvariable:: GPIOF
.. doxygenvariable:: GPIOG

Functions
---------

.. doxygenfunction:: gpio_init
.. doxygenfunction:: gpio_init_all
.. doxygenfunction:: gpio_set_mode
.. doxygenfunction:: gpio_exti_port
.. doxygenfunction:: gpio_write_bit
.. doxygenfunction:: gpio_read_bit
.. doxygenfunction:: gpio_toggle_bit

.. doxygenfunction:: afio_init
.. doxygenfunction:: afio_exti_select

.. _gpio-h-afio-remap:
.. doxygenfunction:: afio_remap
.. doxygenfunction:: afio_cfg_debug_ports

Register Map Base Pointers
--------------------------

.. doxygendefine:: GPIOA_BASE
.. doxygendefine:: GPIOB_BASE
.. doxygendefine:: GPIOC_BASE
.. doxygendefine:: GPIOD_BASE
.. doxygendefine:: GPIOE_BASE
.. doxygendefine:: GPIOF_BASE
.. doxygendefine:: GPIOG_BASE

.. doxygendefine:: AFIO_BASE

Register Bit Definitions
------------------------

GPIO Control Registers
~~~~~~~~~~~~~~~~~~~~~~

These values apply to both the low and high configuration registers
(ST RM0008: GPIOx_CRL and GPIOx_CRH).  You can shift them right by the
appropriate number of bits for the GPIO port bit you're interested in
to obtain a bit mask.

For example, to mask out just the value of GPIOA_CRH_CNF12, note that
GPIO port bit 12's configuration starts at bit 18 in the corresponding
CRH.  Thus, an appropriate mask is ``GPIOA_BASE->CRH & (GPIO_CR_CNF <<
18)``.

.. doxygendefine:: GPIO_CR_CNF_INPUT_ANALOG
.. doxygendefine:: GPIO_CR_CNF_INPUT_FLOATING
.. doxygendefine:: GPIO_CR_CNF_INPUT_PU_PD
.. doxygendefine:: GPIO_CR_CNF_OUTPUT_PP
.. doxygendefine:: GPIO_CR_CNF_OUTPUT_OD
.. doxygendefine:: GPIO_CR_CNF_AF_OUTPUT_PP
.. doxygendefine:: GPIO_CR_CNF_AF_OUTPUT_OD
.. doxygendefine:: GPIO_CR_MODE_INPUT
.. doxygendefine:: GPIO_CR_MODE_OUTPUT_10MHZ
.. doxygendefine:: GPIO_CR_MODE_OUTPUT_2MHZ
.. doxygendefine:: GPIO_CR_MODE_OUTPUT_50MHZ

Event Control Register
~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: AFIO_EVCR_EVOE
.. doxygendefine:: AFIO_EVCR_PORT_PA
.. doxygendefine:: AFIO_EVCR_PORT_PB
.. doxygendefine:: AFIO_EVCR_PORT_PC
.. doxygendefine:: AFIO_EVCR_PORT_PD
.. doxygendefine:: AFIO_EVCR_PORT_PE
.. doxygendefine:: AFIO_EVCR_PIN_0
.. doxygendefine:: AFIO_EVCR_PIN_1
.. doxygendefine:: AFIO_EVCR_PIN_2
.. doxygendefine:: AFIO_EVCR_PIN_3
.. doxygendefine:: AFIO_EVCR_PIN_4
.. doxygendefine:: AFIO_EVCR_PIN_5
.. doxygendefine:: AFIO_EVCR_PIN_6
.. doxygendefine:: AFIO_EVCR_PIN_7
.. doxygendefine:: AFIO_EVCR_PIN_8
.. doxygendefine:: AFIO_EVCR_PIN_9
.. doxygendefine:: AFIO_EVCR_PIN_10
.. doxygendefine:: AFIO_EVCR_PIN_11
.. doxygendefine:: AFIO_EVCR_PIN_12
.. doxygendefine:: AFIO_EVCR_PIN_13
.. doxygendefine:: AFIO_EVCR_PIN_14
.. doxygendefine:: AFIO_EVCR_PIN_15

AF Remap and Debug I/O Configuration Register
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: AFIO_MAPR_SWJ_CFG
.. doxygendefine:: AFIO_MAPR_SWJ_CFG_FULL_SWJ
.. doxygendefine:: AFIO_MAPR_SWJ_CFG_FULL_SWJ_NO_NJRST
.. doxygendefine:: AFIO_MAPR_SWJ_CFG_NO_JTAG_SW
.. doxygendefine:: AFIO_MAPR_SWJ_CFG_NO_JTAG_NO_SW
.. doxygendefine:: AFIO_MAPR_ADC2_ETRGREG_REMAP
.. doxygendefine:: AFIO_MAPR_ADC2_ETRGINJ_REMAP
.. doxygendefine:: AFIO_MAPR_ADC1_ETRGREG_REMAP
.. doxygendefine:: AFIO_MAPR_ADC1_ETRGINJ_REMAP
.. doxygendefine:: AFIO_MAPR_TIM5CH4_IREMAP
.. doxygendefine:: AFIO_MAPR_PD01_REMAP
.. doxygendefine:: AFIO_MAPR_CAN_REMAP
.. doxygendefine:: AFIO_MAPR_CAN_REMAP_NONE
.. doxygendefine:: AFIO_MAPR_CAN_REMAP_PB8_PB9
.. doxygendefine:: AFIO_MAPR_CAN_REMAP_PD0_PD1
.. doxygendefine:: AFIO_MAPR_TIM4_REMAP
.. doxygendefine:: AFIO_MAPR_TIM3_REMAP
.. doxygendefine:: AFIO_MAPR_TIM3_REMAP_NONE
.. doxygendefine:: AFIO_MAPR_TIM3_REMAP_PARTIAL
.. doxygendefine:: AFIO_MAPR_TIM3_REMAP_FULL
.. doxygendefine:: AFIO_MAPR_TIM2_REMAP
.. doxygendefine:: AFIO_MAPR_TIM2_REMAP_NONE
.. doxygendefine:: AFIO_MAPR_TIM2_REMAP_PA15_PB3_PA2_PA3
.. doxygendefine:: AFIO_MAPR_TIM2_REMAP_PA0_PA1_PB10_PB11
.. doxygendefine:: AFIO_MAPR_TIM2_REMAP_FULL
.. doxygendefine:: AFIO_MAPR_TIM1_REMAP
.. doxygendefine:: AFIO_MAPR_TIM1_REMAP_NONE
.. doxygendefine:: AFIO_MAPR_TIM1_REMAP_PARTIAL
.. doxygendefine:: AFIO_MAPR_TIM1_REMAP_FULL
.. doxygendefine:: AFIO_MAPR_USART3_REMAP
.. doxygendefine:: AFIO_MAPR_USART3_REMAP_NONE
.. doxygendefine:: AFIO_MAPR_USART3_REMAP_PARTIAL
.. doxygendefine:: AFIO_MAPR_USART3_REMAP_FULL
.. doxygendefine:: AFIO_MAPR_USART2_REMAP
.. doxygendefine:: AFIO_MAPR_USART1_REMAP
.. doxygendefine:: AFIO_MAPR_I2C1_REMAP
.. doxygendefine:: AFIO_MAPR_SPI1_REMAP

External Interrupt Configuration Register 1
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: AFIO_EXTICR1_EXTI3
.. doxygendefine:: AFIO_EXTICR1_EXTI3_PA
.. doxygendefine:: AFIO_EXTICR1_EXTI3_PB
.. doxygendefine:: AFIO_EXTICR1_EXTI3_PC
.. doxygendefine:: AFIO_EXTICR1_EXTI3_PD
.. doxygendefine:: AFIO_EXTICR1_EXTI3_PE
.. doxygendefine:: AFIO_EXTICR1_EXTI3_PF
.. doxygendefine:: AFIO_EXTICR1_EXTI3_PG
.. doxygendefine:: AFIO_EXTICR1_EXTI2
.. doxygendefine:: AFIO_EXTICR1_EXTI2_PA
.. doxygendefine:: AFIO_EXTICR1_EXTI2_PB
.. doxygendefine:: AFIO_EXTICR1_EXTI2_PC
.. doxygendefine:: AFIO_EXTICR1_EXTI2_PD
.. doxygendefine:: AFIO_EXTICR1_EXTI2_PE
.. doxygendefine:: AFIO_EXTICR1_EXTI2_PF
.. doxygendefine:: AFIO_EXTICR1_EXTI2_PG
.. doxygendefine:: AFIO_EXTICR1_EXTI1
.. doxygendefine:: AFIO_EXTICR1_EXTI1_PA
.. doxygendefine:: AFIO_EXTICR1_EXTI1_PB
.. doxygendefine:: AFIO_EXTICR1_EXTI1_PC
.. doxygendefine:: AFIO_EXTICR1_EXTI1_PD
.. doxygendefine:: AFIO_EXTICR1_EXTI1_PE
.. doxygendefine:: AFIO_EXTICR1_EXTI1_PF
.. doxygendefine:: AFIO_EXTICR1_EXTI1_PG
.. doxygendefine:: AFIO_EXTICR1_EXTI0
.. doxygendefine:: AFIO_EXTICR1_EXTI0_PA
.. doxygendefine:: AFIO_EXTICR1_EXTI0_PB
.. doxygendefine:: AFIO_EXTICR1_EXTI0_PC
.. doxygendefine:: AFIO_EXTICR1_EXTI0_PD
.. doxygendefine:: AFIO_EXTICR1_EXTI0_PE
.. doxygendefine:: AFIO_EXTICR1_EXTI0_PF
.. doxygendefine:: AFIO_EXTICR1_EXTI0_PG

External Interrupt Configuration Register 2
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: AFIO_EXTICR2_EXTI7
.. doxygendefine:: AFIO_EXTICR2_EXTI7_PA
.. doxygendefine:: AFIO_EXTICR2_EXTI7_PB
.. doxygendefine:: AFIO_EXTICR2_EXTI7_PC
.. doxygendefine:: AFIO_EXTICR2_EXTI7_PD
.. doxygendefine:: AFIO_EXTICR2_EXTI7_PE
.. doxygendefine:: AFIO_EXTICR2_EXTI7_PF
.. doxygendefine:: AFIO_EXTICR2_EXTI7_PG
.. doxygendefine:: AFIO_EXTICR2_EXTI6
.. doxygendefine:: AFIO_EXTICR2_EXTI6_PA
.. doxygendefine:: AFIO_EXTICR2_EXTI6_PB
.. doxygendefine:: AFIO_EXTICR2_EXTI6_PC
.. doxygendefine:: AFIO_EXTICR2_EXTI6_PD
.. doxygendefine:: AFIO_EXTICR2_EXTI6_PE
.. doxygendefine:: AFIO_EXTICR2_EXTI6_PF
.. doxygendefine:: AFIO_EXTICR2_EXTI6_PG
.. doxygendefine:: AFIO_EXTICR2_EXTI5
.. doxygendefine:: AFIO_EXTICR2_EXTI5_PA
.. doxygendefine:: AFIO_EXTICR2_EXTI5_PB
.. doxygendefine:: AFIO_EXTICR2_EXTI5_PC
.. doxygendefine:: AFIO_EXTICR2_EXTI5_PD
.. doxygendefine:: AFIO_EXTICR2_EXTI5_PE
.. doxygendefine:: AFIO_EXTICR2_EXTI5_PF
.. doxygendefine:: AFIO_EXTICR2_EXTI5_PG
.. doxygendefine:: AFIO_EXTICR2_EXTI4
.. doxygendefine:: AFIO_EXTICR2_EXTI4_PA
.. doxygendefine:: AFIO_EXTICR2_EXTI4_PB
.. doxygendefine:: AFIO_EXTICR2_EXTI4_PC
.. doxygendefine:: AFIO_EXTICR2_EXTI4_PD
.. doxygendefine:: AFIO_EXTICR2_EXTI4_PE
.. doxygendefine:: AFIO_EXTICR2_EXTI4_PF
.. doxygendefine:: AFIO_EXTICR2_EXTI4_PG

AF Remap and Debug I/O Configuration Register 2
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: AFIO_MAPR2_FSMC_NADV
.. doxygendefine:: AFIO_MAPR2_TIM14_REMAP
.. doxygendefine:: AFIO_MAPR2_TIM13_REMAP
.. doxygendefine:: AFIO_MAPR2_TIM11_REMAP
.. doxygendefine:: AFIO_MAPR2_TIM10_REMAP
.. doxygendefine:: AFIO_MAPR2_TIM9_REMAP
