.. highlight:: c
.. _libmaple-iwdg:

``<libmaple/iwdg.h>``
=====================

Independent Watchdog (IWDG) support. The IWDG peripheral is common
across supported targets, so everything documented here is portable.

.. contents:: Contents
   :local:

Usage Note
----------

To use the independent watchdog, first call :ref:`iwdg_init()
<libmaple-iwdg-iwdg_init>` with the appropriate prescaler and IWDG
counter reload values for your application.  Afterwards, you must
periodically call :ref:`iwdg_feed() <libmaple-iwdg-iwdg_feed>` before
the IWDG counter reaches zero to reset the counter to its reload
value.  If you do not, the chip will reset.

Once started, the independent watchdog cannot be turned off.

Devices
-------

None at this time.

Functions
---------

.. _libmaple-iwdg-iwdg_init:
.. doxygenfunction:: iwdg_init
.. _libmaple-iwdg-iwdg_feed:
.. doxygenfunction:: iwdg_feed

Types
-----

.. doxygenenum:: iwdg_prescaler


Register Maps
-------------

.. doxygendefine:: IWDG_BASE

.. doxygenstruct:: iwdg_reg_map

Register Bit Definitions
------------------------

These are given as source code.

::

    /* Key register */

    #define IWDG_KR_UNLOCK                  0x5555
    #define IWDG_KR_FEED                    0xAAAA
    #define IWDG_KR_START                   0xCCCC

    /* Prescaler register */

    #define IWDG_PR_DIV_4                   0x0
    #define IWDG_PR_DIV_8                   0x1
    #define IWDG_PR_DIV_16                  0x2
    #define IWDG_PR_DIV_32                  0x3
    #define IWDG_PR_DIV_64                  0x4
    #define IWDG_PR_DIV_128                 0x5
    #define IWDG_PR_DIV_256                 0x6

    /* Status register */

    #define IWDG_SR_RVU_BIT                 1
    #define IWDG_SR_PVU_BIT                 0

    #define IWDG_SR_RVU                     (1U << IWDG_SR_RVU_BIT)
    #define IWDG_SR_PVU                     (1U << IWDG_SR_PVU_BIT)
