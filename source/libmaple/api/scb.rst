.. highlight:: c
.. _libmaple-scb:

``<libmaple/scb.h>``
====================

.. TODO [0.0.13] check for any F2 modifications

System Control Block (SCB) support. This is currently limited to a
register map and bit definitions.

.. warning::

   At time of writing, ST PM0056 (which specifies the system control
   block on STM32F1) appears to be buggy (some registers required or
   specified as implementation-defined by ARM are not mentioned).
   This file is the result of combining material from ARM and ST, and
   is subject to change.  See the source code for more details.

   If you notice a problem or have any other input on this, please
   `contact`_ us!

.. contents:: Contents
   :local:

Register Maps
-------------

The SCB has the following register map. Its base pointer is ``SCB_BASE``.

.. doxygenstruct:: scb_reg_map
.. doxygendefine:: SCB_BASE

Register Bit Definitions
------------------------

These are given as source code.

::

    /* No SCB_REG_FIELD_BIT macros as the relevant addresses are not in a
     * bit-band region. */

    /* CPUID base register (SCB_CPUID) */

    #define SCB_CPUID_IMPLEMENTER           (0xFF << 24)
    #define SCB_CPUID_VARIANT               (0xF << 20)
    #define SCB_CPUID_CONSTANT              (0xF << 16)
    #define SCB_CPUID_PARTNO                (0xFFF << 4)
    #define SCB_CPUID_REVISION              0xF

    /* Interrupt control state register (SCB_ICSR) */

    #define SCB_ICSR_NMIPENDSET             (1U << 31)
    #define SCB_ICSR_PENDSVSET              (1U << 28)
    #define SCB_ICSR_PENDSVCLR              (1U << 27)
    #define SCB_ICSR_PENDSTSET              (1U << 26)
    #define SCB_ICSR_PENDSTCLR              (1U << 25)
    #define SCB_ICSR_ISRPENDING             (1U << 22)
    #define SCB_ICSR_VECTPENDING            (0x3FF << 12)
    #define SCB_ICSR_RETOBASE               (1U << 11)
    #define SCB_ICSR_VECTACTIVE             0xFF

    /* Vector table offset register (SCB_VTOR) */

    #define SCB_VTOR_TBLOFF                 (0x1FFFFF << 9)

    /* Application interrupt and reset control register (SCB_AIRCR) */

    #define SCB_AIRCR_VECTKEYSTAT           (0x5FA << 16)
    #define SCB_AIRCR_VECTKEY               (0x5FA << 16)
    #define SCB_AIRCR_ENDIANNESS            (1U << 15)
    #define SCB_AIRCR_PRIGROUP              (0x3 << 8)
    #define SCB_AIRCR_SYSRESETREQ           (1U << 2)
    #define SCB_AIRCR_VECTCLRACTIVE         (1U << 1)
    #define SCB_AIRCR_VECTRESET             (1U << 0)

    /* System control register (SCB_SCR) */

    #define SCB_SCR_SEVONPEND               (1U << 4)
    #define SCB_SCR_SLEEPDEEP               (1U << 2)
    #define SCB_SCR_SLEEPONEXIT             (1U << 1)

    /* Configuration and Control Register (SCB_CCR) */

    #define SCB_CCR_STKALIGN                (1U << 9)
    #define SCB_CCR_BFHFNMIGN               (1U << 8)
    #define SCB_CCR_DIV_0_TRP               (1U << 4)
    #define SCB_CCR_UNALIGN_TRP             (1U << 3)
    #define SCB_CCR_USERSETMPEND            (1U << 1)
    #define SCB_CCR_NONBASETHRDENA          (1U << 0)

    /* System handler priority registers (SCB_SHPRx) */

    #define SCB_SHPR1_PRI6                  (0xFF << 16)
    #define SCB_SHPR1_PRI5                  (0xFF << 8)
    #define SCB_SHPR1_PRI4                  0xFF

    #define SCB_SHPR2_PRI11                 (0xFF << 24)

    #define SCB_SHPR3_PRI15                 (0xFF << 24)
    #define SCB_SHPR3_PRI14                 (0xFF << 16)

    /* System Handler Control and state register (SCB_SHCSR) */

    #define SCB_SHCSR_USGFAULTENA           (1U << 18)
    #define SCB_SHCSR_BUSFAULTENA           (1U << 17)
    #define SCB_SHCSR_MEMFAULTENA           (1U << 16)
    #define SCB_SHCSR_SVCALLPENDED          (1U << 15)
    #define SCB_SHCSR_BUSFAULTPENDED        (1U << 14)
    #define SCB_SHCSR_MEMFAULTPENDED        (1U << 13)
    #define SCB_SHCSR_USGFAULTPENDED        (1U << 12)
    #define SCB_SHCSR_SYSTICKACT            (1U << 11)
    #define SCB_SHCSR_PENDSVACT             (1U << 10)
    #define SCB_SHCSR_MONITORACT            (1U << 8)
    #define SCB_SHCSR_SVCALLACT             (1U << 7)
    #define SCB_SHCSR_USGFAULTACT           (1U << 3)
    #define SCB_SHCSR_BUSFAULTACT           (1U << 1)
    #define SCB_SHCSR_MEMFAULTACT           (1U << 0)

    /* Configurable fault status register (SCB_CFSR) */

    #define SCB_CFSR_DIVBYZERO              (1U << 25)
    #define SCB_CFSR_UNALIGNED              (1U << 24)
    #define SCB_CFSR_NOCP                   (1U << 19)
    #define SCB_CFSR_INVPC                  (1U << 18)
    #define SCB_CFSR_INVSTATE               (1U << 17)
    #define SCB_CFSR_UNDEFINSTR             (1U << 16)
    #define SCB_CFSR_BFARVALID              (1U << 15)
    #define SCB_CFSR_STKERR                 (1U << 12)
    #define SCB_CFSR_UNSTKERR               (1U << 11)
    #define SCB_CFSR_IMPRECISERR            (1U << 10)
    #define SCB_CFSR_PRECISERR              (1U << 9)
    #define SCB_CFSR_IBUSERR                (1U << 8)
    #define SCB_CFSR_MMARVALID              (1U << 7)
    #define SCB_CFSR_MSTKERR                (1U << 4)
    #define SCB_CFSR_MUNSTKERR              (1U << 3)
    #define SCB_CFSR_DACCVIOL               (1U << 1)
    #define SCB_CFSR_IACCVIOL               (1U << 0)

    /* Hard Fault Status Register (SCB_HFSR) */

    #define SCB_HFSR_DEBUG_VT               (1U << 31)
    #define SCB_CFSR_FORCED                 (1U << 30)
    #define SCB_CFSR_VECTTBL                (1U << 1)

    /* Debug Fault Status Register */

    /* Not specified by PM0056, but required by ARM.  The bit definitions
     * here are based on the names given in the ARM v7-M ARM. */

    #define SCB_DFSR_EXTERNAL               (1U << 4)
    #define SCB_DFSR_VCATCH                 (1U << 3)
    #define SCB_DFSR_DWTTRAP                (1U << 2)
    #define SCB_DFSR_BKPT                   (1U << 1)
    #define SCB_DFSR_HALTED                 (1U << 0)
