.. highlight:: c
.. _libmaple-nvic:

``<libmaple/nvic.h>``
=====================

Nested Vector Interrupt Controller (NVIC) support.

The same API is used on all targets, but the available interrupts are
target-dependent. To manage this, each target series defines an
:ref:`nvic_irq_num <libmaple-nvic-nvic_irq_num>` enumerator for each
available interrupt.

.. contents:: Contents
   :local:

Devices
-------

None at this time.

.. _libmaple-nvic-nvic_irq_num:

``nvic_irq_num``
----------------

This target-dependent enum is used to identify an interrupt vector
number.  Interrupts which are common across series have the same token
(though not necessarily the same value) for their ``nvic_irq_num``\ s.
The available values on each supported target series are as follows.

STM32F1 Targets
~~~~~~~~~~~~~~~

.. doxygenenum:: stm32f1::nvic_irq_num

STM32F2 Targets
~~~~~~~~~~~~~~~

.. doxygenenum:: stm32f2::nvic_irq_num

Functions
---------

.. doxygenfunction:: nvic_init
.. doxygenfunction:: nvic_set_vector_table
.. doxygenfunction:: nvic_irq_set_priority
.. doxygenfunction:: nvic_globalirq_enable
.. doxygenfunction:: nvic_globalirq_disable
.. doxygenfunction:: nvic_irq_enable
.. doxygenfunction:: nvic_irq_disable
.. doxygenfunction:: nvic_irq_disable_all
.. doxygenfunction:: nvic_sys_reset

Register Maps
-------------

Since the NVIC is part of the ARM core, its registers and base pointer
are common across all targes.

.. doxygendefine:: NVIC_BASE
.. doxygenstruct:: nvic_reg_map

Register Bit Definitions
------------------------

None at this time.
