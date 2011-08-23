.. highlight:: c
.. _libmaple-fsmc:

``fsmc.h``
==========

Flexible Static Memory Controller (FSMC) support.

.. contents:: Contents
   :local:

Types
-----

.. doxygenstruct:: fsmc_reg_map
.. doxygenstruct:: fsmc_nor_psram_reg_map

Devices
-------

None at this time.

Functions
---------

.. doxygenfunction:: fsmc_sram_init_gpios
.. doxygenfunction:: fsmc_nor_psram_set_datast
.. doxygenfunction:: fsmc_nor_psram_set_addset

Memory Bank Boundary Addresses
------------------------------

.. doxygendefine:: FSMC_BANK1
.. doxygendefine:: FSMC_BANK2
.. doxygendefine:: FSMC_BANK3
.. doxygendefine:: FSMC_BANK4

.. doxygendefine:: FSMC_NOR_PSRAM_REGION1
.. doxygendefine:: FSMC_NOR_PSRAM_REGION2
.. doxygendefine:: FSMC_NOR_PSRAM_REGION3
.. doxygendefine:: FSMC_NOR_PSRAM_REGION4

Register Map Base Pointers
--------------------------

.. doxygendefine:: FSMC_BASE

.. doxygendefine:: FSMC_NOR_PSRAM1_BASE
.. doxygendefine:: FSMC_NOR_PSRAM2_BASE
.. doxygendefine:: FSMC_NOR_PSRAM3_BASE
.. doxygendefine:: FSMC_NOR_PSRAM4_BASE

Register Bit Definitions
------------------------

NOR/PSRAM Chip-Select Control Registers
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: FSMC_BCR_CBURSTRW_BIT
.. doxygendefine:: FSMC_BCR_ASYNCWAIT_BIT
.. doxygendefine:: FSMC_BCR_EXTMOD_BIT
.. doxygendefine:: FSMC_BCR_WAITEN_BIT
.. doxygendefine:: FSMC_BCR_WREN_BIT
.. doxygendefine:: FSMC_BCR_WAITCFG_BIT
.. doxygendefine:: FSMC_BCR_WRAPMOD_BIT
.. doxygendefine:: FSMC_BCR_WAITPOL_BIT
.. doxygendefine:: FSMC_BCR_BURSTEN_BIT
.. doxygendefine:: FSMC_BCR_FACCEN_BIT
.. doxygendefine:: FSMC_BCR_MUXEN_BIT
.. doxygendefine:: FSMC_BCR_MBKEN_BIT

.. doxygendefine:: FSMC_BCR_CBURSTRW
.. doxygendefine:: FSMC_BCR_ASYNCWAIT
.. doxygendefine:: FSMC_BCR_EXTMOD
.. doxygendefine:: FSMC_BCR_WAITEN
.. doxygendefine:: FSMC_BCR_WREN
.. doxygendefine:: FSMC_BCR_WAITCFG
.. doxygendefine:: FSMC_BCR_WRAPMOD
.. doxygendefine:: FSMC_BCR_WAITPOL
.. doxygendefine:: FSMC_BCR_BURSTEN
.. doxygendefine:: FSMC_BCR_FACCEN
.. doxygendefine:: FSMC_BCR_MWID
.. doxygendefine:: FSMC_BCR_MWID_8BITS
.. doxygendefine:: FSMC_BCR_MWID_16BITS
.. doxygendefine:: FSMC_BCR_MTYP
.. doxygendefine:: FSMC_BCR_MTYP_SRAM
.. doxygendefine:: FSMC_BCR_MTYP_PSRAM
.. doxygendefine:: FSMC_BCR_MTYP_NOR_FLASH
.. doxygendefine:: FSMC_BCR_MUXEN
.. doxygendefine:: FSMC_BCR_MBKEN

SRAM/NOR-Flash Chip-Select Timing Registers
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: FSMC_BTR_ACCMOD
.. doxygendefine:: FSMC_BTR_ACCMOD_A
.. doxygendefine:: FSMC_BTR_ACCMOD_B
.. doxygendefine:: FSMC_BTR_ACCMOD_C
.. doxygendefine:: FSMC_BTR_ACCMOD_D
.. doxygendefine:: FSMC_BTR_DATLAT
.. doxygendefine:: FSMC_BTR_CLKDIV
.. doxygendefine:: FSMC_BTR_BUSTURN
.. doxygendefine:: FSMC_BTR_DATAST
.. doxygendefine:: FSMC_BTR_ADDHLD
.. doxygendefine:: FSMC_BTR_ADDSET

SRAM/NOR-Flash Write Timing Registers
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: FSMC_BWTR_ACCMOD
.. doxygendefine:: FSMC_BWTR_ACCMOD_A
.. doxygendefine:: FSMC_BWTR_ACCMOD_B
.. doxygendefine:: FSMC_BWTR_ACCMOD_C
.. doxygendefine:: FSMC_BWTR_ACCMOD_D
.. doxygendefine:: FSMC_BWTR_DATLAT
.. doxygendefine:: FSMC_BWTR_CLKDIV
.. doxygendefine:: FSMC_BWTR_DATAST
.. doxygendefine:: FSMC_BWTR_ADDHLD
.. doxygendefine:: FSMC_BWTR_ADDSET

NAND Flash/PC Card Controller Registers
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: FSMC_PCR_ECCEN_BIT
.. doxygendefine:: FSMC_PCR_PTYP_BIT
.. doxygendefine:: FSMC_PCR_PBKEN_BIT
.. doxygendefine:: FSMC_PCR_PWAITEN_BIT

.. doxygendefine:: FSMC_PCR_ECCPS
.. doxygendefine:: FSMC_PCR_ECCPS_256B
.. doxygendefine:: FSMC_PCR_ECCPS_512B
.. doxygendefine:: FSMC_PCR_ECCPS_1024B
.. doxygendefine:: FSMC_PCR_ECCPS_2048B
.. doxygendefine:: FSMC_PCR_ECCPS_4096B
.. doxygendefine:: FSMC_PCR_ECCPS_8192B
.. doxygendefine:: FSMC_PCR_TAR
.. doxygendefine:: FSMC_PCR_TCLR
.. doxygendefine:: FSMC_PCR_ECCEN
.. doxygendefine:: FSMC_PCR_PWID
.. doxygendefine:: FSMC_PCR_PWID_8BITS
.. doxygendefine:: FSMC_PCR_PWID_16BITS
.. doxygendefine:: FSMC_PCR_PTYP
.. doxygendefine:: FSMC_PCR_PTYP_PC_CF_PCMCIA
.. doxygendefine:: FSMC_PCR_PTYP_NAND
.. doxygendefine:: FSMC_PCR_PBKEN
.. doxygendefine:: FSMC_PCR_PWAITEN

FIFO Status And Interrupt Registers
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: FSMC_SR_FEMPT_BIT
.. doxygendefine:: FSMC_SR_IFEN_BIT
.. doxygendefine:: FSMC_SR_ILEN_BIT
.. doxygendefine:: FSMC_SR_IREN_BIT
.. doxygendefine:: FSMC_SR_IFS_BIT
.. doxygendefine:: FSMC_SR_ILS_BIT
.. doxygendefine:: FSMC_SR_IRS_BIT

.. doxygendefine:: FSMC_SR_FEMPT
.. doxygendefine:: FSMC_SR_IFEN
.. doxygendefine:: FSMC_SR_ILEN
.. doxygendefine:: FSMC_SR_IREN
.. doxygendefine:: FSMC_SR_IFS
.. doxygendefine:: FSMC_SR_ILS
.. doxygendefine:: FSMC_SR_IRS

Common Memory Space Timing Registers
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: FSMC_PMEM_MEMHIZ
.. doxygendefine:: FSMC_PMEM_MEMHOLD
.. doxygendefine:: FSMC_PMEM_MEMWAIT
.. doxygendefine:: FSMC_PMEM_MEMSET

Attribute Memory Space Timing Registers
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: FSMC_PATT_ATTHIZ
.. doxygendefine:: FSMC_PATT_ATTHOLD
.. doxygendefine:: FSMC_PATT_ATTWAIT
.. doxygendefine:: FSMC_PATT_ATTSET

I/O Space Timing Register 4
~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: FSMC_PIO_IOHIZ
.. doxygendefine:: FSMC_PIO_IOHOLD
.. doxygendefine:: FSMC_PIO_IOWAIT
.. doxygendefine:: FSMC_PIO_IOSET
