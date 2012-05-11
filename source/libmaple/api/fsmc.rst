.. highlight:: c
.. _libmaple-fsmc:

``<libmaple/fsmc.h>``
=====================

Flexible Static Memory Controller (FSMC) support. The FSMC peripheral
is only available on some targets.  Including this header on a target
without an FSMC will cause a compilation error.  Check your target's
documentation to determine if it's available.  You can also use
:ref:`STM32_HAVE_FSMC <libmaple-stm32-STM32_HAVE_FSMC>` from
``<libmaple/stm32.h>`` to determine whether your target has an FSMC at
build time.

All functionality documented here is portable.

.. contents:: Contents
   :local:

Usage Note
----------

FSMC support is fairly limited at this time. Current Leaflabs boards
only use the FSMC to interface with external SRAM chips, so that's
what there's the most support for (:ref:`patches welcome!
<libmaple-contributing>`). Even for use with SRAM, you will still need
to program some registers directly.

To use the FSMC with an SRAM chip, first call
:ref:`fsmc_sram_init_gpios() <libmaple-fsmc-fsmc_sram_init_gpios>` to
configure its data, address, and control lines.  Then, turn on the
FSMC clock (by calling :ref:`rcc_clk_enable(RCC_FSMC)
<libmaple-rcc-rcc_clk_enable>`). You can then configure the relevant
:ref:`fsmc_nor_psram_reg_map <libmaple-fsmc-fsmc_nor_psram_reg_map>`
``BCR`` register yourself for the SRAM chip you are using.

You can additionally use :ref:`fsmc_nor_psram_set_datast()
<libmaple-fsmc-fsmc_nor_psram_set_datast>` and
:ref:`fsmc_nor_psram_set_datast() <libmaple-fsmc-fsmc_nor_psram_set_datast>`
to control read/write timing.

Devices
-------

None at this time.

Functions
---------

.. _libmaple-fsmc-fsmc_sram_init_gpios:
.. doxygenfunction:: fsmc_sram_init_gpios
.. _libmaple-fsmc-fsmc_nor_psram_set_datast:
.. doxygenfunction:: fsmc_nor_psram_set_datast
.. _libmaple-fsmc-fsmc_nor_psram_set_addset:
.. doxygenfunction:: fsmc_nor_psram_set_addset

Register Maps
-------------

The general purpose register map type is ``fsmc_reg_map``; its base
pointer is ``FSMC_BASE``.  The ``fsmc_nor_psram_reg_map`` type is for
use configuring the registers for an individual NOR/PSRAM region
(``FSMC_BCRx``, ``FSMC_BTRx``, and ``FSMC_BWTRx``); the relevant base
pointers are ``FSMC_NOR_PSRAM_REGION1`` through
``FSMC_NOR_PSRAM_REGION4``.

.. doxygendefine:: FSMC_BASE

.. doxygendefine:: FSMC_NOR_PSRAM1_BASE
.. doxygendefine:: FSMC_NOR_PSRAM2_BASE
.. doxygendefine:: FSMC_NOR_PSRAM3_BASE
.. doxygendefine:: FSMC_NOR_PSRAM4_BASE

.. doxygenstruct:: fsmc_reg_map
.. _libmaple-fsmc-fsmc_nor_psram_reg_map:
.. doxygenstruct:: fsmc_nor_psram_reg_map

Memory Bank Boundary Addresses
------------------------------

Reading and writing data on an external memory chip using FSMC is done
by reading and writing from addresses in special memory-mapped
sections of the address space called *memory banks*.

This is convenient, since it implies that the usual load and store
instructions used for I/O with the internal SRAM are also used to
perform bus transactions with the external memory chip.  (Which means
you can use ``memcpy()`` etc. on external memory.)

Pointers to the memory banks' base addresses are given by the
following macros.

.. doxygendefine:: FSMC_BANK1
.. doxygendefine:: FSMC_BANK2
.. doxygendefine:: FSMC_BANK3
.. doxygendefine:: FSMC_BANK4

.. doxygendefine:: FSMC_NOR_PSRAM_REGION1
.. doxygendefine:: FSMC_NOR_PSRAM_REGION2
.. doxygendefine:: FSMC_NOR_PSRAM_REGION3
.. doxygendefine:: FSMC_NOR_PSRAM_REGION4

Register Bit Definitions
------------------------

These are given as source code.

::

    /* NOR/PSRAM chip-select control registers */

    #define FSMC_BCR_CBURSTRW_BIT           19
    #define FSMC_BCR_ASYNCWAIT_BIT          15
    #define FSMC_BCR_EXTMOD_BIT             14
    #define FSMC_BCR_WAITEN_BIT             13
    #define FSMC_BCR_WREN_BIT               12
    #define FSMC_BCR_WAITCFG_BIT            11
    #define FSMC_BCR_WRAPMOD_BIT            10
    #define FSMC_BCR_WAITPOL_BIT            9
    #define FSMC_BCR_BURSTEN_BIT            8
    #define FSMC_BCR_FACCEN_BIT             6
    #define FSMC_BCR_MUXEN_BIT              1
    #define FSMC_BCR_MBKEN_BIT              0

    #define FSMC_BCR_CBURSTRW               (1U << FSMC_BCR_CBURSTRW_BIT)
    #define FSMC_BCR_ASYNCWAIT              (1U << FSMC_BCR_ASYNCWAIT_BIT)
    #define FSMC_BCR_EXTMOD                 (1U << FSMC_BCR_EXTMOD_BIT)
    #define FSMC_BCR_WAITEN                 (1U << FSMC_BCR_WAITEN_BIT)
    #define FSMC_BCR_WREN                   (1U << FSMC_BCR_WREN_BIT)
    #define FSMC_BCR_WAITCFG                (1U << FSMC_BCR_WAITCFG_BIT)
    #define FSMC_BCR_WRAPMOD                (1U << FSMC_BCR_WRAPMOD_BIT)
    #define FSMC_BCR_WAITPOL                (1U << FSMC_BCR_WAITPOL_BIT)
    #define FSMC_BCR_BURSTEN                (1U << FSMC_BCR_BURSTEN_BIT)
    #define FSMC_BCR_FACCEN                 (1U << FSMC_BCR_FACCEN_BIT)
    #define FSMC_BCR_MWID                   (0x3 << 4)
    #define FSMC_BCR_MWID_8BITS             (0x0 << 4)
    #define FSMC_BCR_MWID_16BITS            (0x1 << 4)
    #define FSMC_BCR_MTYP                   (0x3 << 2)
    #define FSMC_BCR_MTYP_SRAM              (0x0 << 2)
    #define FSMC_BCR_MTYP_PSRAM             (0x1 << 2)
    #define FSMC_BCR_MTYP_NOR_FLASH         (0x2 << 2)
    #define FSMC_BCR_MUXEN                  (1U << FSMC_BCR_MUXEN_BIT)
    #define FSMC_BCR_MBKEN                  (1U << FSMC_BCR_MBKEN_BIT)

    /* SRAM/NOR-Flash chip-select timing registers */

    #define FSMC_BTR_ACCMOD                 (0x3 << 28)
    #define FSMC_BTR_ACCMOD_A               (0x0 << 28)
    #define FSMC_BTR_ACCMOD_B               (0x1 << 28)
    #define FSMC_BTR_ACCMOD_C               (0x2 << 28)
    #define FSMC_BTR_ACCMOD_D               (0x3 << 28)
    #define FSMC_BTR_DATLAT                 (0xF << 24)
    #define FSMC_BTR_CLKDIV                 (0xF << 20)
    #define FSMC_BTR_BUSTURN                (0xF << 16)
    #define FSMC_BTR_DATAST                 (0xFF << 8)
    #define FSMC_BTR_ADDHLD                 (0xF << 4)
    #define FSMC_BTR_ADDSET                 0xF

    /* SRAM/NOR-Flash write timing registers */

    #define FSMC_BWTR_ACCMOD                 (0x3 << 28)
    #define FSMC_BWTR_ACCMOD_A               (0x0 << 28)
    #define FSMC_BWTR_ACCMOD_B               (0x1 << 28)
    #define FSMC_BWTR_ACCMOD_C               (0x2 << 28)
    #define FSMC_BWTR_ACCMOD_D               (0x3 << 28)
    #define FSMC_BWTR_DATLAT                 (0xF << 24)
    #define FSMC_BWTR_CLKDIV                 (0xF << 20)
    #define FSMC_BWTR_DATAST                 (0xFF << 8)
    #define FSMC_BWTR_ADDHLD                 (0xF << 4)
    #define FSMC_BWTR_ADDSET                 0xF

    /* NAND Flash/PC Card controller registers */

    #define FSMC_PCR_ECCEN_BIT               6
    #define FSMC_PCR_PTYP_BIT                3
    #define FSMC_PCR_PBKEN_BIT               2
    #define FSMC_PCR_PWAITEN_BIT             1

    #define FSMC_PCR_ECCPS                   (0x7 << 17)
    #define FSMC_PCR_ECCPS_256B              (0x0 << 17)
    #define FSMC_PCR_ECCPS_512B              (0x1 << 17)
    #define FSMC_PCR_ECCPS_1024B             (0x2 << 17)
    #define FSMC_PCR_ECCPS_2048B             (0x3 << 17)
    #define FSMC_PCR_ECCPS_4096B             (0x4 << 17)
    #define FSMC_PCR_ECCPS_8192B             (0x5 << 17)
    #define FSMC_PCR_TAR                     (0xF << 13)
    #define FSMC_PCR_TCLR                    (0xF << 9)
    #define FSMC_PCR_ECCEN                   (1U << FSMC_PCR_ECCEN_BIT)
    #define FSMC_PCR_PWID                    (0x3 << 4)
    #define FSMC_PCR_PWID_8BITS              (0x0 << 4)
    #define FSMC_PCR_PWID_16BITS             (0x1 << 4)
    #define FSMC_PCR_PTYP                    (1U << FSMC_PCR_PTYP_BIT)
    #define FSMC_PCR_PTYP_PC_CF_PCMCIA       (0x0 << FSMC_PCR_PTYP_BIT)
    #define FSMC_PCR_PTYP_NAND               (0x1 << FSMC_PCR_PTYP_BIT)
    #define FSMC_PCR_PBKEN                   (1U << FSMC_PCR_PBKEN_BIT)
    #define FSMC_PCR_PWAITEN                 (1U << FSMC_PCR_PWAITEN_BIT)

    /* FIFO status and interrupt registers */

    #define FSMC_SR_FEMPT_BIT                6
    #define FSMC_SR_IFEN_BIT                 5
    #define FSMC_SR_ILEN_BIT                 4
    #define FSMC_SR_IREN_BIT                 3
    #define FSMC_SR_IFS_BIT                  2
    #define FSMC_SR_ILS_BIT                  1
    #define FSMC_SR_IRS_BIT                  0

    #define FSMC_SR_FEMPT                    (1U << FSMC_SR_FEMPT_BIT)
    #define FSMC_SR_IFEN                     (1U << FSMC_SR_IFEN_BIT)
    #define FSMC_SR_ILEN                     (1U << FSMC_SR_ILEN_BIT)
    #define FSMC_SR_IREN                     (1U << FSMC_SR_IREN_BIT)
    #define FSMC_SR_IFS                      (1U << FSMC_SR_IFS_BIT)
    #define FSMC_SR_ILS                      (1U << FSMC_SR_ILS_BIT)
    #define FSMC_SR_IRS                      (1U << FSMC_SR_IRS_BIT)

    /* Common memory space timing registers */

    #define FSMC_PMEM_MEMHIZ                 (0xFF << 24)
    #define FSMC_PMEM_MEMHOLD                (0xFF << 16)
    #define FSMC_PMEM_MEMWAIT                (0xFF << 8)
    #define FSMC_PMEM_MEMSET                 0xFF

    /* Attribute memory space timing registers */

    #define FSMC_PATT_ATTHIZ                 (0xFF << 24)
    #define FSMC_PATT_ATTHOLD                (0xFF << 16)
    #define FSMC_PATT_ATTWAIT                (0xFF << 8)
    #define FSMC_PATT_ATTSET                 0xFF

    /* I/O space timing register 4 */

    #define FSMC_PIO_IOHIZ                  (0xFF << 24)
    #define FSMC_PIO_IOHOLD                 (0xFF << 16)
    #define FSMC_PIO_IOWAIT                 (0xFF << 8)
    #define FSMC_PIO_IOSET                  0xF
