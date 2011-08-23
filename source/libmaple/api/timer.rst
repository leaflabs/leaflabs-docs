.. highlight:: c
.. _libmaple-timer:

``timer.h``
===========

Timer support.

.. contents:: Contents
   :local:

Types
-----

The timer register map type, unlike that for most other peripherals in
libmaple, is a union rather than a struct.  This is due to the fact
that there are advanced, general purpose, and basic timers.  Thus,
each kind of timer has a register map type, and a ``union
timer_reg_map`` ties it all together.

.. doxygenstruct:: timer_adv_reg_map
.. doxygenstruct:: timer_gen_reg_map
.. doxygenstruct:: timer_bas_reg_map
.. doxygenunion:: timer_reg_map
.. doxygenenum:: timer_type
.. doxygenstruct:: timer_dev
.. doxygenenum:: timer_mode
.. doxygenenum:: timer_channel
.. doxygenenum:: timer_interrupt_id
.. doxygenenum:: timer_dma_base_addr
.. doxygenenum:: timer_oc_mode
.. doxygenenum:: timer_oc_mode_flags

Devices
-------

.. doxygenvariable:: TIMER1
.. doxygenvariable:: TIMER2
.. doxygenvariable:: TIMER3
.. doxygenvariable:: TIMER4
.. doxygenvariable:: TIMER5
.. doxygenvariable:: TIMER6
.. doxygenvariable:: TIMER7
.. doxygenvariable:: TIMER8

Functions
---------

Enabling and Disabling
~~~~~~~~~~~~~~~~~~~~~~

.. doxygenfunction:: timer_init
.. doxygenfunction:: timer_init_all
.. doxygenfunction:: timer_disable
.. doxygenfunction:: timer_disable_all

General Configuration
~~~~~~~~~~~~~~~~~~~~~

.. doxygenfunction:: timer_set_mode
.. doxygenfunction:: timer_foreach

Count and Prescaler
~~~~~~~~~~~~~~~~~~~

.. doxygenfunction:: timer_get_count
.. doxygenfunction:: timer_set_count
.. doxygenfunction:: timer_pause
.. doxygenfunction:: timer_resume
.. doxygenfunction:: timer_generate_update
.. doxygenfunction:: timer_get_prescaler
.. doxygenfunction:: timer_set_prescaler
.. doxygenfunction:: timer_get_reload
.. doxygenfunction:: timer_set_reload

Interrupts
~~~~~~~~~~

.. doxygenfunction:: timer_attach_interrupt
.. doxygenfunction:: timer_detach_interrupt
.. doxygenfunction:: timer_enable_irq
.. doxygenfunction:: timer_disable_irq

Capture/Compare
~~~~~~~~~~~~~~~

.. doxygenfunction:: timer_get_compare
.. doxygenfunction:: timer_set_compare
.. doxygenfunction:: timer_cc_enable
.. doxygenfunction:: timer_cc_disable
.. doxygenfunction:: timer_cc_get_pol
.. doxygenfunction:: timer_cc_set_pol
.. doxygenfunction:: timer_oc_set_mode

DMA
~~~

.. doxygenfunction:: timer_dma_enable_trg_req
.. doxygenfunction:: timer_dma_disable_trg_req
.. doxygenfunction:: timer_dma_enable_req
.. doxygenfunction:: timer_dma_get_burst_len
.. doxygenfunction:: timer_dma_set_burst_len
.. doxygenfunction:: timer_dma_get_base_addr
.. doxygenfunction:: timer_dma_set_base_addr

Register Map Base Pointers
--------------------------

.. doxygendefine:: TIMER1_BASE
.. doxygendefine:: TIMER2_BASE
.. doxygendefine:: TIMER3_BASE
.. doxygendefine:: TIMER4_BASE
.. doxygendefine:: TIMER5_BASE
.. doxygendefine:: TIMER6_BASE
.. doxygendefine:: TIMER7_BASE
.. doxygendefine:: TIMER8_BASE

Register Bit Definitions
------------------------

Control register 1 (CR1)
~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: TIMER_CR1_ARPE_BIT
.. doxygendefine:: TIMER_CR1_DIR_BIT
.. doxygendefine:: TIMER_CR1_OPM_BIT
.. doxygendefine:: TIMER_CR1_URS_BIT
.. doxygendefine:: TIMER_CR1_UDIS_BIT
.. doxygendefine:: TIMER_CR1_CEN_BIT

.. doxygendefine:: TIMER_CR1_CKD
.. doxygendefine:: TIMER_CR1_CKD_1TCKINT
.. doxygendefine:: TIMER_CR1_CKD_2TCKINT
.. doxygendefine:: TIMER_CR1_CKD_4TICKINT
.. doxygendefine:: TIMER_CR1_ARPE
.. doxygendefine:: TIMER_CR1_CKD_CMS
.. doxygendefine:: TIMER_CR1_CKD_CMS_EDGE
.. doxygendefine:: TIMER_CR1_CKD_CMS_CENTER1
.. doxygendefine:: TIMER_CR1_CKD_CMS_CENTER2
.. doxygendefine:: TIMER_CR1_CKD_CMS_CENTER3
.. doxygendefine:: TIMER_CR1_DIR
.. doxygendefine:: TIMER_CR1_OPM
.. doxygendefine:: TIMER_CR1_URS
.. doxygendefine:: TIMER_CR1_UDIS
.. doxygendefine:: TIMER_CR1_CEN

Control register 2 (CR2)
~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: TIMER_CR2_OIS4_BIT
.. doxygendefine:: TIMER_CR2_OIS3N_BIT
.. doxygendefine:: TIMER_CR2_OIS3_BIT
.. doxygendefine:: TIMER_CR2_OIS2N_BIT
.. doxygendefine:: TIMER_CR2_OIS2_BIT
.. doxygendefine:: TIMER_CR2_OIS1N_BIT
.. doxygendefine:: TIMER_CR2_OIS1_BIT
.. doxygendefine:: TIMER_CR2_TI1S_BIT
.. doxygendefine:: TIMER_CR2_CCDS_BIT
.. doxygendefine:: TIMER_CR2_CCUS_BIT
.. doxygendefine:: TIMER_CR2_CCPC_BIT

.. doxygendefine:: TIMER_CR2_OIS4
.. doxygendefine:: TIMER_CR2_OIS3N
.. doxygendefine:: TIMER_CR2_OIS3
.. doxygendefine:: TIMER_CR2_OIS2N
.. doxygendefine:: TIMER_CR2_OIS2
.. doxygendefine:: TIMER_CR2_OIS1N
.. doxygendefine:: TIMER_CR2_OIS1
.. doxygendefine:: TIMER_CR2_TI1S
.. doxygendefine:: TIMER_CR2_MMS
.. doxygendefine:: TIMER_CR2_MMS_RESET
.. doxygendefine:: TIMER_CR2_MMS_ENABLE
.. doxygendefine:: TIMER_CR2_MMS_UPDATE
.. doxygendefine:: TIMER_CR2_MMS_COMPARE_PULSE
.. doxygendefine:: TIMER_CR2_MMS_COMPARE_OC1REF
.. doxygendefine:: TIMER_CR2_MMS_COMPARE_OC2REF
.. doxygendefine:: TIMER_CR2_MMS_COMPARE_OC3REF
.. doxygendefine:: TIMER_CR2_MMS_COMPARE_OC4REF
.. doxygendefine:: TIMER_CR2_CCDS
.. doxygendefine:: TIMER_CR2_CCUS
.. doxygendefine:: TIMER_CR2_CCPC

Slave mode control register (SMCR)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: TIMER_SMCR_ETP_BIT
.. doxygendefine:: TIMER_SMCR_ECE_BIT
.. doxygendefine:: TIMER_SMCR_MSM_BIT

.. doxygendefine:: TIMER_SMCR_ETP
.. doxygendefine:: TIMER_SMCR_ECE
.. doxygendefine:: TIMER_SMCR_ETPS
.. doxygendefine:: TIMER_SMCR_ETPS_OFF
.. doxygendefine:: TIMER_SMCR_ETPS_DIV2
.. doxygendefine:: TIMER_SMCR_ETPS_DIV4
.. doxygendefine:: TIMER_SMCR_ETPS_DIV8
.. doxygendefine:: TIMER_SMCR_ETF
.. doxygendefine:: TIMER_SMCR_MSM
.. doxygendefine:: TIMER_SMCR_TS
.. doxygendefine:: TIMER_SMCR_TS_ITR0
.. doxygendefine:: TIMER_SMCR_TS_ITR1
.. doxygendefine:: TIMER_SMCR_TS_ITR2
.. doxygendefine:: TIMER_SMCR_TS_ITR3
.. doxygendefine:: TIMER_SMCR_TS_TI1F_ED
.. doxygendefine:: TIMER_SMCR_TS_TI1FP1
.. doxygendefine:: TIMER_SMCR_TS_TI2FP2
.. doxygendefine:: TIMER_SMCR_TS_ETRF
.. doxygendefine:: TIMER_SMCR_SMS
.. doxygendefine:: TIMER_SMCR_SMS_DISABLED
.. doxygendefine:: TIMER_SMCR_SMS_ENCODER1
.. doxygendefine:: TIMER_SMCR_SMS_ENCODER2
.. doxygendefine:: TIMER_SMCR_SMS_ENCODER3
.. doxygendefine:: TIMER_SMCR_SMS_RESET
.. doxygendefine:: TIMER_SMCR_SMS_GATED
.. doxygendefine:: TIMER_SMCR_SMS_TRIGGER
.. doxygendefine:: TIMER_SMCR_SMS_EXTERNAL

DMA/Interrupt enable register (DIER)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: TIMER_DIER_TDE_BIT
.. doxygendefine:: TIMER_DIER_CC4DE_BIT
.. doxygendefine:: TIMER_DIER_CC3DE_BIT
.. doxygendefine:: TIMER_DIER_CC2DE_BIT
.. doxygendefine:: TIMER_DIER_CC1DE_BIT
.. doxygendefine:: TIMER_DIER_UDE_BIT
.. doxygendefine:: TIMER_DIER_TIE_BIT
.. doxygendefine:: TIMER_DIER_CC4IE_BIT
.. doxygendefine:: TIMER_DIER_CC3IE_BIT
.. doxygendefine:: TIMER_DIER_CC2IE_BIT
.. doxygendefine:: TIMER_DIER_CC1IE_BIT
.. doxygendefine:: TIMER_DIER_UIE_BIT

.. doxygendefine:: TIMER_DIER_TDE
.. doxygendefine:: TIMER_DIER_CC4DE
.. doxygendefine:: TIMER_DIER_CC3DE
.. doxygendefine:: TIMER_DIER_CC2DE
.. doxygendefine:: TIMER_DIER_CC1DE
.. doxygendefine:: TIMER_DIER_UDE
.. doxygendefine:: TIMER_DIER_TIE
.. doxygendefine:: TIMER_DIER_CC4IE
.. doxygendefine:: TIMER_DIER_CC3IE
.. doxygendefine:: TIMER_DIER_CC2IE
.. doxygendefine:: TIMER_DIER_CC1IE
.. doxygendefine:: TIMER_DIER_UIE

Status register (SR)
~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: TIMER_SR_CC4OF_BIT
.. doxygendefine:: TIMER_SR_CC3OF_BIT
.. doxygendefine:: TIMER_SR_CC2OF_BIT
.. doxygendefine:: TIMER_SR_CC1OF_BIT
.. doxygendefine:: TIMER_SR_BIF_BIT
.. doxygendefine:: TIMER_SR_TIF_BIT
.. doxygendefine:: TIMER_SR_COMIF_BIT
.. doxygendefine:: TIMER_SR_CC4IF_BIT
.. doxygendefine:: TIMER_SR_CC3IF_BIT
.. doxygendefine:: TIMER_SR_CC2IF_BIT
.. doxygendefine:: TIMER_SR_CC1IF_BIT
.. doxygendefine:: TIMER_SR_UIF_BIT

.. doxygendefine:: TIMER_SR_CC4OF
.. doxygendefine:: TIMER_SR_CC3OF
.. doxygendefine:: TIMER_SR_CC2OF
.. doxygendefine:: TIMER_SR_CC1OF
.. doxygendefine:: TIMER_SR_BIF
.. doxygendefine:: TIMER_SR_TIF
.. doxygendefine:: TIMER_SR_COMIF
.. doxygendefine:: TIMER_SR_CC4IF
.. doxygendefine:: TIMER_SR_CC3IF
.. doxygendefine:: TIMER_SR_CC2IF
.. doxygendefine:: TIMER_SR_CC1IF
.. doxygendefine:: TIMER_SR_UIF

Event generation register (EGR)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: TIMER_EGR_TG_BIT
.. doxygendefine:: TIMER_EGR_CC4G_BIT
.. doxygendefine:: TIMER_EGR_CC3G_BIT
.. doxygendefine:: TIMER_EGR_CC2G_BIT
.. doxygendefine:: TIMER_EGR_CC1G_BIT
.. doxygendefine:: TIMER_EGR_UG_BIT

.. doxygendefine:: TIMER_EGR_TG
.. doxygendefine:: TIMER_EGR_CC4G
.. doxygendefine:: TIMER_EGR_CC3G
.. doxygendefine:: TIMER_EGR_CC2G
.. doxygendefine:: TIMER_EGR_CC1G
.. doxygendefine:: TIMER_EGR_UG

Capture/compare mode registers, common values
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: TIMER_CCMR_CCS_OUTPUT
.. doxygendefine:: TIMER_CCMR_CCS_INPUT_TI1
.. doxygendefine:: TIMER_CCMR_CCS_INPUT_TI2
.. doxygendefine:: TIMER_CCMR_CCS_INPUT_TRC

Capture/compare mode register 1 (CCMR1)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: TIMER_CCMR1_OC2CE_BIT
.. doxygendefine:: TIMER_CCMR1_OC2PE_BIT
.. doxygendefine:: TIMER_CCMR1_OC2FE_BIT
.. doxygendefine:: TIMER_CCMR1_OC1CE_BIT
.. doxygendefine:: TIMER_CCMR1_OC1PE_BIT
.. doxygendefine:: TIMER_CCMR1_OC1FE_BIT

.. doxygendefine:: TIMER_CCMR1_OC2CE
.. doxygendefine:: TIMER_CCMR1_OC2M
.. doxygendefine:: TIMER_CCMR1_IC2F
.. doxygendefine:: TIMER_CCMR1_OC2PE
.. doxygendefine:: TIMER_CCMR1_OC2FE
.. doxygendefine:: TIMER_CCMR1_IC2PSC
.. doxygendefine:: TIMER_CCMR1_CC2S
.. doxygendefine:: TIMER_CCMR1_CC2S_OUTPUT
.. doxygendefine:: TIMER_CCMR1_CC2S_INPUT_TI1
.. doxygendefine:: TIMER_CCMR1_CC2S_INPUT_TI2
.. doxygendefine:: TIMER_CCMR1_CC2S_INPUT_TRC
.. doxygendefine:: TIMER_CCMR1_OC1CE
.. doxygendefine:: TIMER_CCMR1_OC1M
.. doxygendefine:: TIMER_CCMR1_IC1F
.. doxygendefine:: TIMER_CCMR1_OC1PE
.. doxygendefine:: TIMER_CCMR1_OC1FE
.. doxygendefine:: TIMER_CCMR1_IC1PSC
.. doxygendefine:: TIMER_CCMR1_CC1S
.. doxygendefine:: TIMER_CCMR1_CC1S_OUTPUT
.. doxygendefine:: TIMER_CCMR1_CC1S_INPUT_TI1
.. doxygendefine:: TIMER_CCMR1_CC1S_INPUT_TI2
.. doxygendefine:: TIMER_CCMR1_CC1S_INPUT_TRC

Capture/compare mode register 2 (CCMR2)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: TIMER_CCMR2_OC4CE_BIT
.. doxygendefine:: TIMER_CCMR2_OC4PE_BIT
.. doxygendefine:: TIMER_CCMR2_OC4FE_BIT
.. doxygendefine:: TIMER_CCMR2_OC3CE_BIT
.. doxygendefine:: TIMER_CCMR2_OC3PE_BIT
.. doxygendefine:: TIMER_CCMR2_OC3FE_BIT

.. doxygendefine:: TIMER_CCMR2_OC4CE
.. doxygendefine:: TIMER_CCMR2_OC4M
.. doxygendefine:: TIMER_CCMR2_IC2F
.. doxygendefine:: TIMER_CCMR2_OC4PE
.. doxygendefine:: TIMER_CCMR2_OC4FE
.. doxygendefine:: TIMER_CCMR2_IC2PSC
.. doxygendefine:: TIMER_CCMR2_CC4S
.. doxygendefine:: TIMER_CCMR1_CC4S_OUTPUT
.. doxygendefine:: TIMER_CCMR1_CC4S_INPUT_TI1
.. doxygendefine:: TIMER_CCMR1_CC4S_INPUT_TI2
.. doxygendefine:: TIMER_CCMR1_CC4S_INPUT_TRC
.. doxygendefine:: TIMER_CCMR2_OC3CE
.. doxygendefine:: TIMER_CCMR2_OC3M
.. doxygendefine:: TIMER_CCMR2_IC1F
.. doxygendefine:: TIMER_CCMR2_OC3PE
.. doxygendefine:: TIMER_CCMR2_OC3FE
.. doxygendefine:: TIMER_CCMR2_IC1PSC
.. doxygendefine:: TIMER_CCMR2_CC3S
.. doxygendefine:: TIMER_CCMR1_CC3S_OUTPUT
.. doxygendefine:: TIMER_CCMR1_CC3S_INPUT_TI1
.. doxygendefine:: TIMER_CCMR1_CC3S_INPUT_TI2
.. doxygendefine:: TIMER_CCMR1_CC3S_INPUT_TRC

Capture/compare enable register (CCER)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: TIMER_CCER_CC4P_BIT
.. doxygendefine:: TIMER_CCER_CC4E_BIT
.. doxygendefine:: TIMER_CCER_CC3P_BIT
.. doxygendefine:: TIMER_CCER_CC3E_BIT
.. doxygendefine:: TIMER_CCER_CC2P_BIT
.. doxygendefine:: TIMER_CCER_CC2E_BIT
.. doxygendefine:: TIMER_CCER_CC1P_BIT
.. doxygendefine:: TIMER_CCER_CC1E_BIT

.. doxygendefine:: TIMER_CCER_CC4P
.. doxygendefine:: TIMER_CCER_CC4E
.. doxygendefine:: TIMER_CCER_CC3P
.. doxygendefine:: TIMER_CCER_CC3E
.. doxygendefine:: TIMER_CCER_CC2P
.. doxygendefine:: TIMER_CCER_CC2E
.. doxygendefine:: TIMER_CCER_CC1P
.. doxygendefine:: TIMER_CCER_CC1E

Break and dead-time register (BDTR)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: TIMER_BDTR_MOE_BIT
.. doxygendefine:: TIMER_BDTR_AOE_BIT
.. doxygendefine:: TIMER_BDTR_BKP_BIT
.. doxygendefine:: TIMER_BDTR_BKE_BIT
.. doxygendefine:: TIMER_BDTR_OSSR_BIT
.. doxygendefine:: TIMER_BDTR_OSSI_BIT

.. doxygendefine:: TIMER_BDTR_MOE
.. doxygendefine:: TIMER_BDTR_AOE
.. doxygendefine:: TIMER_BDTR_BKP
.. doxygendefine:: TIMER_BDTR_BKE
.. doxygendefine:: TIMER_BDTR_OSSR
.. doxygendefine:: TIMER_BDTR_OSSI
.. doxygendefine:: TIMER_BDTR_LOCK
.. doxygendefine:: TIMER_BDTR_LOCK_OFF
.. doxygendefine:: TIMER_BDTR_LOCK_LEVEL1
.. doxygendefine:: TIMER_BDTR_LOCK_LEVEL2
.. doxygendefine:: TIMER_BDTR_LOCK_LEVEL3
.. doxygendefine:: TIMER_BDTR_DTG

DMA control register (DCR)
~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: TIMER_DCR_DBL
.. doxygendefine:: TIMER_DCR_DBL_1BYTE
.. doxygendefine:: TIMER_DCR_DBL_2BYTE
.. doxygendefine:: TIMER_DCR_DBL_3BYTE
.. doxygendefine:: TIMER_DCR_DBL_4BYTE
.. doxygendefine:: TIMER_DCR_DBL_5BYTE
.. doxygendefine:: TIMER_DCR_DBL_6BYTE
.. doxygendefine:: TIMER_DCR_DBL_7BYTE
.. doxygendefine:: TIMER_DCR_DBL_8BYTE
.. doxygendefine:: TIMER_DCR_DBL_9BYTE
.. doxygendefine:: TIMER_DCR_DBL_10BYTE
.. doxygendefine:: TIMER_DCR_DBL_11BYTE
.. doxygendefine:: TIMER_DCR_DBL_12BYTE
.. doxygendefine:: TIMER_DCR_DBL_13BYTE
.. doxygendefine:: TIMER_DCR_DBL_14BYTE
.. doxygendefine:: TIMER_DCR_DBL_15BYTE
.. doxygendefine:: TIMER_DCR_DBL_16BYTE
.. doxygendefine:: TIMER_DCR_DBL_17BYTE
.. doxygendefine:: TIMER_DCR_DBL_18BYTE
.. doxygendefine:: TIMER_DCR_DBA
.. doxygendefine:: TIMER_DCR_DBA_CR1
.. doxygendefine:: TIMER_DCR_DBA_CR2
.. doxygendefine:: TIMER_DCR_DBA_SMCR
.. doxygendefine:: TIMER_DCR_DBA_DIER
.. doxygendefine:: TIMER_DCR_DBA_SR
.. doxygendefine:: TIMER_DCR_DBA_EGR
.. doxygendefine:: TIMER_DCR_DBA_CCMR1
.. doxygendefine:: TIMER_DCR_DBA_CCMR2
.. doxygendefine:: TIMER_DCR_DBA_CCER
.. doxygendefine:: TIMER_DCR_DBA_CNT
.. doxygendefine:: TIMER_DCR_DBA_PSC
.. doxygendefine:: TIMER_DCR_DBA_ARR
.. doxygendefine:: TIMER_DCR_DBA_RCR
.. doxygendefine:: TIMER_DCR_DBA_CCR1
.. doxygendefine:: TIMER_DCR_DBA_CCR2
.. doxygendefine:: TIMER_DCR_DBA_CCR3
.. doxygendefine:: TIMER_DCR_DBA_CCR4
.. doxygendefine:: TIMER_DCR_DBA_BDTR
.. doxygendefine:: TIMER_DCR_DBA_DCR
.. doxygendefine:: TIMER_DCR_DBA_DMAR
