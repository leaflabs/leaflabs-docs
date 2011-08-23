.. highlight:: c
.. _libmaple-iwdg:

``iwdg.h``
==========

Independent Watchdog (IWDG) support.

.. contents:: Contents
   :local:

Usage Note
----------

To use the independent watchdog, first call :c:func:`iwdg_init()` with
the appropriate prescaler and IWDG counter reload values for your
application.  Afterwards, you must periodically call
:c:func:`iwdg_feed()` before the IWDG counter reaches 0 to reset the
counter to its reload value.  If you do not, the chip will reset.

Once started, the independent watchdog cannot be turned off.

Types
-----

.. doxygenstruct:: iwdg_reg_map
.. doxygenenum:: iwdg_prescaler

Devices
-------

None at this time.

Functions
---------

.. doxygenfunction:: iwdg_init
.. doxygenfunction:: iwdg_feed

Register Map Base Pointers
--------------------------

.. doxygendefine:: IWDG_BASE

Register Bit Definitions
------------------------

Key register
~~~~~~~~~~~~

.. doxygendefine:: IWDG_KR_UNLOCK
.. doxygendefine:: IWDG_KR_FEED
.. doxygendefine:: IWDG_KR_START

Prescaler register
~~~~~~~~~~~~~~~~~~

.. doxygendefine:: IWDG_PR_DIV_4
.. doxygendefine:: IWDG_PR_DIV_8
.. doxygendefine:: IWDG_PR_DIV_16
.. doxygendefine:: IWDG_PR_DIV_32
.. doxygendefine:: IWDG_PR_DIV_64
.. doxygendefine:: IWDG_PR_DIV_128
.. doxygendefine:: IWDG_PR_DIV_256

Status register
~~~~~~~~~~~~~~~

.. doxygendefine:: IWDG_SR_RVU_BIT
.. doxygendefine:: IWDG_SR_PVU_BIT

.. doxygendefine:: IWDG_SR_RVU
.. doxygendefine:: IWDG_SR_PVU
