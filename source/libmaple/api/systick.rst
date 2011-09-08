.. highlight:: c

.. _libmaple-systick:

``systick.h``
=============

System timer (SysTick) support.

.. contents:: Contents
   :local:

Types
-----

.. doxygenstruct:: systick_reg_map

Devices
-------

None.

Functions
---------

.. doxygenfunction:: systick_init
.. _libmaple-systick-enable:
.. doxygenfunction:: systick_enable
.. _libmaple-systick-disable:
.. doxygenfunction:: systick_disable
.. doxygenfunction:: systick_uptime
.. doxygenfunction:: systick_get_count
.. doxygenfunction:: systick_check_underflow

Register Map Base Pointers
--------------------------

.. doxygendefine:: SYSTICK_BASE

Register Bit Definitions
------------------------

Control and status register
~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: SYSTICK_CSR_COUNTFLAG
.. doxygendefine:: SYSTICK_CSR_CLKSOURCE
.. doxygendefine:: SYSTICK_CSR_CLKSOURCE_EXTERNAL
.. doxygendefine:: SYSTICK_CSR_CLKSOURCE_CORE
.. doxygendefine:: SYSTICK_CSR_TICKINT
.. doxygendefine:: SYSTICK_CSR_TICKINT_PEND
.. doxygendefine:: SYSTICK_CSR_TICKINT_NO_PEND
.. doxygendefine:: SYSTICK_CSR_ENABLE
.. doxygendefine:: SYSTICK_CSR_ENABLE_MULTISHOT
.. doxygendefine:: SYSTICK_CSR_ENABLE_DISABLED

Calibration value register
~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: SYSTICK_CVR_NOREF
.. doxygendefine:: SYSTICK_CVR_SKEW
.. doxygendefine:: SYSTICK_CVR_TENMS
