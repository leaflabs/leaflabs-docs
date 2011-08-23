.. highlight:: c
.. _libmaple-dac:

``dac.h``
=========

Digital to Analog Conversion (DAC) support.

.. contents:: Contents
   :local:

Types
-----

.. doxygenstruct:: dac_dev
.. doxygenstruct:: dac_reg_map

Devices
-------

.. doxygenvariable:: DAC

Functions
---------

.. doxygenfunction:: dac_init
.. doxygenfunction:: dac_write_channel
.. doxygenfunction:: dac_enable_channel
.. doxygenfunction:: dac_disable_channel

Register Map Base Pointers
--------------------------

.. doxygendefine:: DAC_BASE

Register Bit Definitions
------------------------

Control register
~~~~~~~~~~~~~~~~

**Channel 1**:

.. doxygendefine:: DAC_CR_EN1
.. doxygendefine:: DAC_CR_BOFF1
.. doxygendefine:: DAC_CR_TEN1
.. doxygendefine:: DAC_CR_TSEL1
.. doxygendefine:: DAC_CR_WAVE1
.. doxygendefine:: DAC_CR_MAMP1
.. doxygendefine:: DAC_CR_DMAEN1

**Channel 2**:

.. doxygendefine:: DAC_CR_EN2
.. doxygendefine:: DAC_CR_BOFF2
.. doxygendefine:: DAC_CR_TEN2
.. doxygendefine:: DAC_CR_TSEL2
.. doxygendefine:: DAC_CR_WAVE2
.. doxygendefine:: DAC_CR_MAMP2
.. doxygendefine:: DAC_CR_DMAEN2

Software trigger register
~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: DAC_SWTRIGR_SWTRIG1
.. doxygendefine:: DAC_SWTRIGR_SWTRIG2

Channel 1 12-bit right-aligned data holding register
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: DAC_DHR12R1_DACC1DHR

Channel 1 12-bit left-aligned data holding register
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: DAC_DHR12L1_DACC1DHR

Channel 1 8-bit left-aligned data holding register
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: DAC_DHR8R1_DACC1DHR

Channel 2 12-bit right-aligned data holding register
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: DAC_DHR12R2_DACC2DHR

Channel 2 12-bit left-aligned data holding register
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: DAC_DHR12L2_DACC2DHR

Channel 2 8-bit left-aligned data holding register
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: DAC_DHR8R2_DACC2DHR

Dual DAC 12-bit right-aligned data holding register
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: DAC_DHR12RD_DACC1DHR
.. doxygendefine:: DAC_DHR12RD_DACC2DHR

Dual DAC 12-bit left-aligned data holding register
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: DAC_DHR12LD_DACC1DHR
.. doxygendefine:: DAC_DHR12LD_DACC2DHR

Dual DAC 8-bit left-aligned data holding register
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: DAC_DHR8RD_DACC1DHR
.. doxygendefine:: DAC_DHR8RD_DACC2DHR

Channel 1 data output register
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: DAC_DOR1_DACC1DOR

Channel 1 data output register
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. doxygendefine:: DAC_DOR2_DACC2DOR
