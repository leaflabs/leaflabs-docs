.. highlight:: c
.. _libmaple-stm32:

``stm32.h``
===========

General STM32-specific definitions.  This file is currently somewhat
incomplete, but it will form the future basis for MCU-specific (rather
than board-specific, which belongs in :ref:`Wirish
<libmaple-vs-wirish>`) configuration.

Defines
-------

.. doxygendefine:: STM32_PCLK1
.. doxygendefine:: STM32_PCLK2
.. doxygendefine:: STM32_NR_INTERRUPTS
.. doxygendefine:: STM32_NR_GPIO_PORTS
.. doxygendefine:: STM32_DELAY_US_MULT
.. doxygendefine:: STM32_SRAM_END

Deprecated Defines
------------------

.. doxygendefine:: PCLK1
.. doxygendefine:: PCLK2
.. doxygendefine:: NR_INTERRUPTS
.. doxygendefine:: NR_GPIO_PORTS
.. doxygendefine:: DELAY_US_MULT
