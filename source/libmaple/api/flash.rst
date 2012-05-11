.. highlight:: c
.. _libmaple-flash:

``<libmaple/flash.h>``
======================

Flash memory support.

The built-in Flash on different STM32 MCUs varies in terms of its
eraseable page/sector size and read/write protections. There isn't
currently much support for dealing with this. This header is mostly
useful for its functions that control Flash features which affect
system performance, like wait states and prefetch buffers.

.. contents:: Contents
   :local:

Devices
-------

None at this time.

Functions
---------

The following functions can be used to portably manipulate Flash memory.

.. doxygenfunction:: flash_set_latency
.. doxygenfunction:: flash_enable_features
.. doxygenfunction:: flash_enable_prefetch

Register Maps
-------------

Register maps vary by target. The base pointer is always ``FLASH_BASE``.

Base Pointer
~~~~~~~~~~~~

.. doxygendefine:: FLASH_BASE

STM32F1 targets
~~~~~~~~~~~~~~~

.. doxygenstruct:: stm32f1::flash_reg_map

STM32F2 targets
~~~~~~~~~~~~~~~

.. doxygenstruct:: stm32f2::flash_reg_map

Register Bit Definitions
------------------------

These are given as source code.  Available register bit definitions
vary by target.

STM32F1 Targets
~~~~~~~~~~~~~~~

::

    /* Access control register */

    #define FLASH_ACR_PRFTBS_BIT            5
    #define FLASH_ACR_PRFTBE_BIT            4
    #define FLASH_ACR_HLFCYA_BIT            3

    #define FLASH_ACR_PRFTBS                (1U << FLASH_ACR_PRFTBS_BIT)
    #define FLASH_ACR_PRFTBE                (1U << FLASH_ACR_PRFTBE_BIT)
    #define FLASH_ACR_HLFCYA                (1U << FLASH_ACR_HLFCYA_BIT)
    #define FLASH_ACR_LATENCY               0x7

    /* Status register */

    #define FLASH_SR_EOP_BIT                5
    #define FLASH_SR_WRPRTERR_BIT           4
    #define FLASH_SR_PGERR_BIT              2
    #define FLASH_SR_BSY_BIT                0

    #define FLASH_SR_EOP                    (1U << FLASH_SR_EOP_BIT)
    #define FLASH_SR_WRPRTERR               (1U << FLASH_SR_WRPRTERR_BIT)
    #define FLASH_SR_PGERR                  (1U << FLASH_SR_PGERR_BIT)
    #define FLASH_SR_BSY                    (1U << FLASH_SR_BSY_BIT)

    /* Control register */

    #define FLASH_CR_EOPIE_BIT              12
    #define FLASH_CR_ERRIE_BIT              10
    #define FLASH_CR_OPTWRE_BIT             9
    #define FLASH_CR_LOCK_BIT               7
    #define FLASH_CR_STRT_BIT               6
    #define FLASH_CR_OPTER_BIT              5
    #define FLASH_CR_OPTPG_BIT              4
    #define FLASH_CR_MER_BIT                2
    #define FLASH_CR_PER_BIT                1
    #define FLASH_CR_PG_BIT                 0

    #define FLASH_CR_EOPIE                  (1U << FLASH_CR_EOPIE_BIT)
    #define FLASH_CR_ERRIE                  (1U << FLASH_CR_ERRIE_BIT)
    #define FLASH_CR_OPTWRE                 (1U << FLASH_CR_OPTWRE_BIT)
    #define FLASH_CR_LOCK                   (1U << FLASH_CR_LOCK_BIT)
    #define FLASH_CR_STRT                   (1U << FLASH_CR_STRT_BIT)
    #define FLASH_CR_OPTER                  (1U << FLASH_CR_OPTER_BIT)
    #define FLASH_CR_OPTPG                  (1U << FLASH_CR_OPTPG_BIT)
    #define FLASH_CR_MER                    (1U << FLASH_CR_MER_BIT)
    #define FLASH_CR_PER                    (1U << FLASH_CR_PER_BIT)
    #define FLASH_CR_PG                     (1U << FLASH_CR_PG_BIT)

    /* Option byte register */

    #define FLASH_OBR_nRST_STDBY_BIT        4
    #define FLASH_OBR_nRST_STOP_BIT         3
    #define FLASH_OBR_WDG_SW_BIT            2
    #define FLASH_OBR_RDPRT_BIT             1
    #define FLASH_OBR_OPTERR_BIT            0

    #define FLASH_OBR_DATA1                 (0xFF << 18)
    #define FLASH_OBR_DATA0                 (0xFF << 10)
    #define FLASH_OBR_USER                  0x3FF
    #define FLASH_OBR_nRST_STDBY            (1U << FLASH_OBR_nRST_STDBY_BIT)
    #define FLASH_OBR_nRST_STOP             (1U << FLASH_OBR_nRST_STOP_BIT)
    #define FLASH_OBR_WDG_SW                (1U << FLASH_OBR_WDG_SW_BIT)
    #define FLASH_OBR_RDPRT                 (1U << FLASH_OBR_RDPRT_BIT)
    #define FLASH_OBR_OPTERR                (1U << FLASH_OBR_OPTERR_BIT)

STM32F2 Targets
~~~~~~~~~~~~~~~

::

    /* Access control register */

    #define FLASH_ACR_DCRST_BIT             12
    #define FLASH_ACR_ICRST_BIT             11
    #define FLASH_ACR_DCEN_BIT              10
    #define FLASH_ACR_ICEN_BIT              9
    #define FLASH_ACR_PRFTEN_BIT            8

    #define FLASH_ACR_DCRST                 (1U << FLASH_ACR_DCRST_BIT)
    #define FLASH_ACR_ICRST                 (1U << FLASH_ACR_ICRST_BIT)
    #define FLASH_ACR_DCEN                  (1U << FLASH_ACR_DCEN_BIT)
    #define FLASH_ACR_ICEN                  (1U << FLASH_ACR_ICEN_BIT)
    #define FLASH_ACR_PRFTEN                (1U << FLASH_ACR_PRFTEN_BIT)
    #define FLASH_ACR_LATENCY               0x7
    #define FLASH_ACR_LATENCY_0WS           0x0
    #define FLASH_ACR_LATENCY_1WS           0x1
    #define FLASH_ACR_LATENCY_2WS           0x2
    #define FLASH_ACR_LATENCY_3WS           0x3
    #define FLASH_ACR_LATENCY_4WS           0x4
    #define FLASH_ACR_LATENCY_5WS           0x5
    #define FLASH_ACR_LATENCY_6WS           0x6
    #define FLASH_ACR_LATENCY_7WS           0x7

    /* Key register */

    #define FLASH_KEYR_KEY1                 0x45670123
    #define FLASH_KEYR_KEY2                 0xCDEF89AB

    /* Option key register */

    #define FLASH_OPTKEYR_OPTKEY1           0x08192A3B
    #define FLASH_OPTKEYR_OPTKEY2           0x4C5D6E7F

    /* Status register */

    #define FLASH_SR_BSY_BIT                16
    #define FLASH_SR_PGSERR_BIT             7
    #define FLASH_SR_PGPERR_BIT             6
    #define FLASH_SR_PGAERR_BIT             5
    #define FLASH_SR_WRPERR_BIT             4
    #define FLASH_SR_OPERR_BIT              1
    #define FLASH_SR_EOP_BIT                0

    #define FLASH_SR_BSY                    (1U << FLASH_SR_BSY_BIT)
    #define FLASH_SR_PGSERR                 (1U << FLASH_SR_PGSERR_BIT)
    #define FLASH_SR_PGPERR                 (1U << FLASH_SR_PGPERR_BIT)
    #define FLASH_SR_PGAERR                 (1U << FLASH_SR_PGAERR_BIT)
    #define FLASH_SR_WRPERR                 (1U << FLASH_SR_WRPERR_BIT)
    #define FLASH_SR_OPERR                  (1U << FLASH_SR_OPERR_BIT)
    #define FLASH_SR_EOP                    (1U << FLASH_SR_EOP_BIT)

    /* Control register */

    #define FLASH_CR_LOCK_BIT               31
    #define FLASH_CR_ERRIE_BIT              25
    #define FLASH_CR_EOPIE_BIT              24
    #define FLASH_CR_STRT_BIT               16
    #define FLASH_CR_MER_BIT                2
    #define FLASH_CR_SER_BIT                1
    #define FLASH_CR_PG_BIT                 0

    #define FLASH_CR_LOCK                   (1U << FLASH_CR_LOCK_BIT)
    #define FLASH_CR_ERRIE                  (1U << FLASH_CR_ERRIE_BIT)
    #define FLASH_CR_EOPIE                  (1U << FLASH_CR_EOPIE_BIT)
    #define FLASH_CR_STRT                   (1U << FLASH_CR_STRT_BIT)

    #define FLASH_CR_PSIZE                  (0x3 << 8)
    #define FLASH_CR_PSIZE_MUL8             (0x0 << 8)
    #define FLASH_CR_PSIZE_MUL16            (0x1 << 8)
    #define FLASH_CR_PSIZE_MUL32            (0x2 << 8)
    #define FLASH_CR_PSIZE_MUL64            (0x3 << 8)

    #define FLASH_CR_SNB                    (0xF << 3)
    #define FLASH_CR_SNB_0                  (0x0 << 3)
    #define FLASH_CR_SNB_1                  (0x1 << 3)
    #define FLASH_CR_SNB_2                  (0x2 << 3)
    #define FLASH_CR_SNB_3                  (0x3 << 3)
    #define FLASH_CR_SNB_4                  (0x4 << 3)
    #define FLASH_CR_SNB_5                  (0x5 << 3)
    #define FLASH_CR_SNB_6                  (0x6 << 3)
    #define FLASH_CR_SNB_7                  (0x7 << 3)
    #define FLASH_CR_SNB_8                  (0x8 << 3)
    #define FLASH_CR_SNB_9                  (0x9 << 3)
    #define FLASH_CR_SNB_10                 (0xA << 3)
    #define FLASH_CR_SNB_11                 (0xB << 3)

    #define FLASH_CR_MER                    (1U << FLASH_CR_MER_BIT)
    #define FLASH_CR_SER                    (1U << FLASH_CR_SER_BIT)
    #define FLASH_CR_PG                     (1U << FLASH_CR_PG_BIT)

    /* Option control register */

    #define FLASH_OPTCR_NRST_STDBY_BIT      7
    #define FLASH_OPTCR_NRST_STOP_BIT       6
    #define FLASH_OPTCR_WDG_SW_BIT          5
    #define FLASH_OPTCR_OPTSTRT_BIT         1
    #define FLASH_OPTCR_OPTLOCK_BIT         0

    #define FLASH_OPTCR_NWRP                (0x3FF << 16)

    /* Excluded: The many level 1 values */
    #define FLASH_OPTCR_RDP                 (0xFF << 8)
    #define FLASH_OPTCR_RDP_LEVEL0          (0xAA << 8)
    #define FLASH_OPTCR_RDP_LEVEL2          (0xCC << 8)

    #define FLASH_OPTCR_USER                (0x7 << 5)
    #define FLASH_OPTCR_nRST_STDBY          (1U << FLASH_OPTCR_nRST_STDBY_BIT)
    #define FLASH_OPTCR_nRST_STOP           (1U << FLASH_OPTCR_nRST_STOP_BIT)
    #define FLASH_OPTCR_WDG_SW              (1U << FLASH_OPTCR_WDG_SW_BIT)

    #define FLASH_OPTCR_BOR_LEV             (0x3 << 2)
    #define FLASH_OPTCR_BOR_LEVEL3          (0x0 << 2)
    #define FLASH_OPTCR_BOR_LEVEL2          (0x1 << 2)
    #define FLASH_OPTCR_BOR_LEVEL1          (0x2 << 2)
    #define FLASH_OPTCR_BOR_OFF             (0x3 << 2)

    #define FLASH_OPTCR_OPTSTRT             (1U << FLASH_OPTCR_OPTSTRT_BIT)
    #define FLASH_OPTCR_OPTLOCK             (1U << FLASH_OPTCR_OPTLOCK_BIT)
