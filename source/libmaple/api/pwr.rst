.. highlight:: c
.. _libmaple-pwr:

``pwr.h``
=========

Power control (PWR) support.

.. contents:: Contents
   :local:

Types
-----

.. doxygenstruct:: pwr_reg_map

Devices
-------

None.

Functions
---------

.. doxygenfunction:: pwr_init

Register Map Base Pointers
--------------------------

.. doxygendefine:: PWR_BASE

Register Bit Definitions
------------------------

Control register
~~~~~~~~~~~~~~~~

.. doxygendefine:: PWR_CR_DBP
.. doxygendefine:: PWR_CR_PVDE
.. doxygendefine:: PWR_CR_CSBF
.. doxygendefine:: PWR_CR_CWUF
.. doxygendefine:: PWR_CR_PDDS
.. doxygendefine:: PWR_CR_LPDS

Control and status register
~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: PWR_CSR_EWUP
.. doxygendefine:: PWR_CSR_PVDO
.. doxygendefine:: PWR_CSR_SBF
.. doxygendefine:: PWR_CSR_WUF
