.. highlight:: c
.. _libmaple-bkp:

``bkp.h``
=========

Backup register (BKP) suport.

.. contents:: Contents
   :local:

Types
-----

.. doxygenstruct:: bkp_dev
.. doxygenstruct:: bkp_reg_map

Devices
-------

.. doxygenvariable:: BKP

Convenience Functions
---------------------

.. doxygenfunction:: bkp_init
.. doxygenfunction:: bkp_enable_writes
.. doxygenfunction:: bkp_disable_writes
.. doxygenfunction:: bkp_read
.. doxygenfunction:: bkp_write

Register Map Base Pointers
--------------------------

.. doxygendefine:: BKP_BASE

Register Bit Definitions
------------------------

Data Registers
~~~~~~~~~~~~~~

.. doxygendefine:: BKP_DR_D

RTC Clock Calibration Register
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: BKP_RTCCR_ASOS_BIT
.. doxygendefine:: BKP_RTCCR_ASOE_BIT
.. doxygendefine:: BKP_RTCCR_CCO_BIT

.. doxygendefine:: BKP_RTCCR_ASOS
.. doxygendefine:: BKP_RTCCR_ASOE
.. doxygendefine:: BKP_RTCCR_CCO
.. doxygendefine:: BKP_RTCCR_CAL

Backup control register
~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: BKP_CR_TPAL_BIT
.. doxygendefine:: BKP_CR_TPE_BIT

.. doxygendefine:: BKP_CR_TPAL
.. doxygendefine:: BKP_CR_TPE

Backup control/status register
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: BKP_CSR_TIF_BIT
.. doxygendefine:: BKP_CSR_TEF_BIT
.. doxygendefine:: BKP_CSR_TPIE_BIT
.. doxygendefine:: BKP_CSR_CTI_BIT
.. doxygendefine:: BKP_CSR_CTE_BIT

.. doxygendefine:: BKP_CSR_TIF
.. doxygendefine:: BKP_CSR_TEF
.. doxygendefine:: BKP_CSR_TPIE
.. doxygendefine:: BKP_CSR_CTI
.. doxygendefine:: BKP_CSR_CTE
