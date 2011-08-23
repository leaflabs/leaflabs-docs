.. highlight:: c
.. _libmaple-adc:

``adc.h``
=========

:ref:`Analog to Digital Conversion <adc>` (ADC) support.

.. contents:: Contents
   :local:

Types
-----

.. doxygenstruct:: adc_dev
.. doxygenstruct:: adc_reg_map
.. doxygenenum:: adc_extsel_event
.. doxygenenum:: adc_smp_rate

Devices
-------

.. doxygenvariable:: ADC1
.. doxygenvariable:: ADC2
.. doxygenvariable:: ADC3

Functions
---------

.. doxygenfunction:: adc_init
.. doxygenfunction:: adc_calibrate
.. doxygenfunction:: adc_set_extsel
.. doxygenfunction:: adc_enable
.. doxygenfunction:: adc_disable
.. doxygenfunction:: adc_disable_all
.. doxygenfunction:: adc_foreach
.. doxygenfunction:: adc_set_sample_rate
.. doxygenfunction:: adc_read
.. doxygenfunction:: adc_set_reg_seqlen
.. doxygenfunction:: adc_set_exttrig

Register Map Base Pointers
--------------------------

.. doxygendefine:: ADC1_BASE
.. doxygendefine:: ADC2_BASE
.. doxygendefine:: ADC3_BASE

Register Bit Definitions
------------------------

Status register
~~~~~~~~~~~~~~~

.. doxygendefine:: ADC_SR_AWD_BIT
.. doxygendefine:: ADC_SR_EOC_BIT
.. doxygendefine:: ADC_SR_JEOC_BIT
.. doxygendefine:: ADC_SR_JSTRT_BIT
.. doxygendefine:: ADC_SR_STRT_BIT

.. doxygendefine:: ADC_SR_AWD
.. doxygendefine:: ADC_SR_EOC
.. doxygendefine:: ADC_SR_JEOC
.. doxygendefine:: ADC_SR_JSTRT
.. doxygendefine:: ADC_SR_STRT

Control register 1
~~~~~~~~~~~~~~~~~~

.. doxygendefine:: ADC_CR1_EOCIE_BIT
.. doxygendefine:: ADC_CR1_AWDIE_BIT
.. doxygendefine:: ADC_CR1_JEOCIE_BIT
.. doxygendefine:: ADC_CR1_SCAN_BIT
.. doxygendefine:: ADC_CR1_AWDSGL_BIT
.. doxygendefine:: ADC_CR1_JAUTO_BIT
.. doxygendefine:: ADC_CR1_DISCEN_BIT
.. doxygendefine:: ADC_CR1_JDISCEN_BIT
.. doxygendefine:: ADC_CR1_JAWDEN_BIT
.. doxygendefine:: ADC_CR1_AWDEN_BIT

.. doxygendefine:: ADC_CR1_AWDCH
.. doxygendefine:: ADC_CR1_EOCIE
.. doxygendefine:: ADC_CR1_AWDIE
.. doxygendefine:: ADC_CR1_JEOCIE
.. doxygendefine:: ADC_CR1_SCAN
.. doxygendefine:: ADC_CR1_AWDSGL
.. doxygendefine:: ADC_CR1_JAUTO
.. doxygendefine:: ADC_CR1_DISCEN
.. doxygendefine:: ADC_CR1_JDISCEN
.. doxygendefine:: ADC_CR1_DISCNUM
.. doxygendefine:: ADC_CR1_JAWDEN
.. doxygendefine:: ADC_CR1_AWDEN

Control register 2
~~~~~~~~~~~~~~~~~~

.. doxygendefine:: ADC_CR2_ADON_BIT
.. doxygendefine:: ADC_CR2_CONT_BIT
.. doxygendefine:: ADC_CR2_CAL_BIT
.. doxygendefine:: ADC_CR2_RSTCAL_BIT
.. doxygendefine:: ADC_CR2_DMA_BIT
.. doxygendefine:: ADC_CR2_ALIGN_BIT
.. doxygendefine:: ADC_CR2_JEXTTRIG_BIT
.. doxygendefine:: ADC_CR2_EXTTRIG_BIT
.. doxygendefine:: ADC_CR2_JSWSTART_BIT
.. doxygendefine:: ADC_CR2_SWSTART_BIT
.. doxygendefine:: ADC_CR2_TSEREFE_BIT

.. doxygendefine:: ADC_CR2_ADON
.. doxygendefine:: ADC_CR2_CONT
.. doxygendefine:: ADC_CR2_CAL
.. doxygendefine:: ADC_CR2_RSTCAL
.. doxygendefine:: ADC_CR2_DMA
.. doxygendefine:: ADC_CR2_ALIGN
.. doxygendefine:: ADC_CR2_JEXTSEL
.. doxygendefine:: ADC_CR2_JEXTTRIG
.. doxygendefine:: ADC_CR2_EXTSEL
.. doxygendefine:: ADC_CR2_EXTTRIG
.. doxygendefine:: ADC_CR2_JSWSTART
.. doxygendefine:: ADC_CR2_SWSTART
.. doxygendefine:: ADC_CR2_TSEREFE

Sample time register 1
~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: ADC_SMPR1_SMP17
.. doxygendefine:: ADC_SMPR1_SMP16
.. doxygendefine:: ADC_SMPR1_SMP15
.. doxygendefine:: ADC_SMPR1_SMP14
.. doxygendefine:: ADC_SMPR1_SMP13
.. doxygendefine:: ADC_SMPR1_SMP12
.. doxygendefine:: ADC_SMPR1_SMP11
.. doxygendefine:: ADC_SMPR1_SMP10

Sample time register 2
~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: ADC_SMPR2_SMP9
.. doxygendefine:: ADC_SMPR2_SMP8
.. doxygendefine:: ADC_SMPR2_SMP7
.. doxygendefine:: ADC_SMPR2_SMP6
.. doxygendefine:: ADC_SMPR2_SMP5
.. doxygendefine:: ADC_SMPR2_SMP4
.. doxygendefine:: ADC_SMPR2_SMP3
.. doxygendefine:: ADC_SMPR2_SMP2
.. doxygendefine:: ADC_SMPR2_SMP1
.. doxygendefine:: ADC_SMPR2_SMP0

Injected channel data offset register
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: ADC_JOFR_JOFFSET

Watchdog high threshold register
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: ADC_HTR_HT

Watchdog low threshold register
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: ADC_LTR_LT

Regular sequence register 1
~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: ADC_SQR1_L
.. doxygendefine:: ADC_SQR1_SQ16
.. doxygendefine:: ADC_SQR1_SQ15
.. doxygendefine:: ADC_SQR1_SQ14
.. doxygendefine:: ADC_SQR1_SQ13

Regular sequence register 2
~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: ADC_SQR2_SQ12
.. doxygendefine:: ADC_SQR2_SQ11
.. doxygendefine:: ADC_SQR2_SQ10
.. doxygendefine:: ADC_SQR2_SQ9
.. doxygendefine:: ADC_SQR2_SQ8
.. doxygendefine:: ADC_SQR2_SQ7

Regular sequence register 3
~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: ADC_SQR3_SQ6
.. doxygendefine:: ADC_SQR3_SQ5
.. doxygendefine:: ADC_SQR3_SQ4
.. doxygendefine:: ADC_SQR3_SQ3
.. doxygendefine:: ADC_SQR3_SQ2
.. doxygendefine:: ADC_SQR3_SQ1

Injected sequence register
~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: ADC_JSQR_JL
.. doxygendefine:: ADC_JSQR_JL_1CONV
.. doxygendefine:: ADC_JSQR_JL_2CONV
.. doxygendefine:: ADC_JSQR_JL_3CONV
.. doxygendefine:: ADC_JSQR_JL_4CONV
.. doxygendefine:: ADC_JSQR_JSQ4
.. doxygendefine:: ADC_JSQR_JSQ3
.. doxygendefine:: ADC_JSQR_JSQ2
.. doxygendefine:: ADC_JSQR_JSQ1

Injected data registers
~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: ADC_JDR_JDATA

Regular data register
~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: ADC_DR_ADC2DATA
.. doxygendefine:: ADC_DR_DATA
