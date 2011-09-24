.. highlight:: c
.. _libmaple-nvic:

``nvic.h``
==========

Nested Vector Interrupt Controller (NVIC) support.

.. contents:: Contents
   :local:

Types
-----

.. doxygenstruct:: nvic_reg_map
.. doxygenenum:: nvic_irq_num

Devices
-------

None at this time.

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

Register Map Base Pointers
--------------------------

.. doxygendefine:: NVIC_BASE

Register Bit Definitions
------------------------

None at this time.
