.. highlight:: c
.. _libmaple-flash:

``flash.h``
===========

Flash support.

.. contents:: Contents
   :local:

Types
-----

.. doxygenstruct:: flash_reg_map

Functions
---------

.. doxygenfunction:: flash_enable_prefetch
.. doxygenfunction:: flash_set_latency

Register Map Base Pointers
--------------------------

.. doxygendefine:: FLASH_BASE

Register Bit Definitions
------------------------

Access control register
~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: FLASH_ACR_PRFTBS_BIT
.. doxygendefine:: FLASH_ACR_PRFTBE_BIT
.. doxygendefine:: FLASH_ACR_HLFCYA_BIT

.. doxygendefine:: FLASH_ACR_PRFTBS
.. doxygendefine:: FLASH_ACR_PRFTBE
.. doxygendefine:: FLASH_ACR_HLFCYA
.. doxygendefine:: FLASH_ACR_LATENCY

Status register
~~~~~~~~~~~~~~~

.. doxygendefine:: FLASH_SR_EOP_BIT
.. doxygendefine:: FLASH_SR_WRPRTERR_BIT
.. doxygendefine:: FLASH_SR_PGERR_BIT
.. doxygendefine:: FLASH_SR_BSY_BIT

.. doxygendefine:: FLASH_SR_EOP
.. doxygendefine:: FLASH_SR_WRPRTERR
.. doxygendefine:: FLASH_SR_PGERR
.. doxygendefine:: FLASH_SR_BSY

Control register
~~~~~~~~~~~~~~~~

.. doxygendefine:: FLASH_CR_EOPIE_BIT
.. doxygendefine:: FLASH_CR_ERRIE_BIT
.. doxygendefine:: FLASH_CR_OPTWRE_BIT
.. doxygendefine:: FLASH_CR_LOCK_BIT
.. doxygendefine:: FLASH_CR_STRT_BIT
.. doxygendefine:: FLASH_CR_OPTER_BIT
.. doxygendefine:: FLASH_CR_OPTPG_BIT
.. doxygendefine:: FLASH_CR_MER_BIT
.. doxygendefine:: FLASH_CR_PER_BIT
.. doxygendefine:: FLASH_CR_PG_BIT

.. doxygendefine:: FLASH_CR_EOPIE
.. doxygendefine:: FLASH_CR_ERRIE
.. doxygendefine:: FLASH_CR_OPTWRE
.. doxygendefine:: FLASH_CR_LOCK
.. doxygendefine:: FLASH_CR_STRT
.. doxygendefine:: FLASH_CR_OPTER
.. doxygendefine:: FLASH_CR_OPTPG
.. doxygendefine:: FLASH_CR_MER
.. doxygendefine:: FLASH_CR_PER
.. doxygendefine:: FLASH_CR_PG

Option byte register
~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: FLASH_OBR_nRST_STDBY_BIT
.. doxygendefine:: FLASH_OBR_nRST_STOP_BIT
.. doxygendefine:: FLASH_OBR_WDG_SW_BIT
.. doxygendefine:: FLASH_OBR_RDPRT_BIT
.. doxygendefine:: FLASH_OBR_OPTERR_BIT

.. doxygendefine:: FLASH_OBR_DATA1
.. doxygendefine:: FLASH_OBR_DATA0
.. doxygendefine:: FLASH_OBR_USER
.. doxygendefine:: FLASH_OBR_nRST_STDBY
.. doxygendefine:: FLASH_OBR_nRST_STOP
.. doxygendefine:: FLASH_OBR_WDG_SW
.. doxygendefine:: FLASH_OBR_RDPRT
.. doxygendefine:: FLASH_OBR_OPTERR
