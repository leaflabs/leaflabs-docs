.. highlight:: c
.. _libmaple-scb:

``scb.h``
=========

System Control Block (SCB) support.

.. warning::

   At time of writing, ST PM0056 (which specifies the system control
   block) appears to be buggy (some registers required by ARM are not
   mentioned).  This file is the result of combining material from ARM
   and ST, and is subject to change.

   If you notice a problem or have any other input on this, please
   `contact`_ us!

.. contents:: Contents
   :local:

Types
-----

.. doxygenstruct:: scb_reg_map

Devices
-------

None.

Register Map Base Pointers
--------------------------

.. doxygendefine:: SCB_BASE

Register Bit Definitions
------------------------

CPUID base register (SCB_CPUID)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: SCB_CPUID_IMPLEMENTER
.. doxygendefine:: SCB_CPUID_VARIANT
.. doxygendefine:: SCB_CPUID_CONSTANT
.. doxygendefine:: SCB_CPUID_PARTNO
.. doxygendefine:: SCB_CPUID_REVISION

Interrupt control state register (SCB_ICSR)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: SCB_ICSR_NMIPENDSET
.. doxygendefine:: SCB_ICSR_PENDSVSET
.. doxygendefine:: SCB_ICSR_PENDSVCLR
.. doxygendefine:: SCB_ICSR_PENDSTSET
.. doxygendefine:: SCB_ICSR_PENDSTCLR
.. doxygendefine:: SCB_ICSR_ISRPENDING
.. doxygendefine:: SCB_ICSR_VECTPENDING
.. doxygendefine:: SCB_ICSR_RETOBASE
.. doxygendefine:: SCB_ICSR_VECTACTIVE

Vector table offset register (SCB_VTOR)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: SCB_VTOR_TBLOFF

Application interrupt and reset control register (SCB_AIRCR)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: SCB_AIRCR_VECTKEYSTAT
.. doxygendefine:: SCB_AIRCR_VECTKEY
.. doxygendefine:: SCB_AIRCR_ENDIANNESS
.. doxygendefine:: SCB_AIRCR_PRIGROUP
.. doxygendefine:: SCB_AIRCR_SYSRESETREQ
.. doxygendefine:: SCB_AIRCR_VECTCLRACTIVE
.. doxygendefine:: SCB_AIRCR_VECTRESET

System control register (SCB_SCR)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: SCB_SCR_SEVONPEND
.. doxygendefine:: SCB_SCR_SLEEPDEEP
.. doxygendefine:: SCB_SCR_SLEEPONEXIT

Configuration and Control Register (SCB_CCR)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: SCB_CCR_STKALIGN
.. doxygendefine:: SCB_CCR_BFHFNMIGN
.. doxygendefine:: SCB_CCR_DIV_0_TRP
.. doxygendefine:: SCB_CCR_UNALIGN_TRP
.. doxygendefine:: SCB_CCR_USERSETMPEND
.. doxygendefine:: SCB_CCR_NONBASETHRDENA

System handler priority registers (SCB_SHPRx)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: SCB_SHPR1_PRI6
.. doxygendefine:: SCB_SHPR1_PRI5
.. doxygendefine:: SCB_SHPR1_PRI4

.. doxygendefine:: SCB_SHPR2_PRI11

.. doxygendefine:: SCB_SHPR3_PRI15
.. doxygendefine:: SCB_SHPR3_PRI14

System Handler Control and state register (SCB_SHCSR)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: SCB_SHCSR_USGFAULTENA
.. doxygendefine:: SCB_SHCSR_BUSFAULTENA
.. doxygendefine:: SCB_SHCSR_MEMFAULTENA
.. doxygendefine:: SCB_SHCSR_SVCALLPENDED
.. doxygendefine:: SCB_SHCSR_BUSFAULTPENDED
.. doxygendefine:: SCB_SHCSR_MEMFAULTPENDED
.. doxygendefine:: SCB_SHCSR_USGFAULTPENDED
.. doxygendefine:: SCB_SHCSR_SYSTICKACT
.. doxygendefine:: SCB_SHCSR_PENDSVACT
.. doxygendefine:: SCB_SHCSR_MONITORACT
.. doxygendefine:: SCB_SHCSR_SVCALLACT
.. doxygendefine:: SCB_SHCSR_USGFAULTACT
.. doxygendefine:: SCB_SHCSR_BUSFAULTACT
.. doxygendefine:: SCB_SHCSR_MEMFAULTACT

Configurable fault status register (SCB_CFSR)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: SCB_CFSR_DIVBYZERO
.. doxygendefine:: SCB_CFSR_UNALIGNED
.. doxygendefine:: SCB_CFSR_NOCP
.. doxygendefine:: SCB_CFSR_INVPC
.. doxygendefine:: SCB_CFSR_INVSTATE
.. doxygendefine:: SCB_CFSR_UNDEFINSTR
.. doxygendefine:: SCB_CFSR_BFARVALID
.. doxygendefine:: SCB_CFSR_STKERR
.. doxygendefine:: SCB_CFSR_UNSTKERR
.. doxygendefine:: SCB_CFSR_IMPRECISERR
.. doxygendefine:: SCB_CFSR_PRECISERR
.. doxygendefine:: SCB_CFSR_IBUSERR
.. doxygendefine:: SCB_CFSR_MMARVALID
.. doxygendefine:: SCB_CFSR_MSTKERR
.. doxygendefine:: SCB_CFSR_MUNSTKERR
.. doxygendefine:: SCB_CFSR_DACCVIOL
.. doxygendefine:: SCB_CFSR_IACCVIOL

Hard Fault Status Register (SCB_HFSR)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: SCB_HFSR_DEBUG_VT
.. doxygendefine:: SCB_CFSR_FORCED
.. doxygendefine:: SCB_CFSR_VECTTBL

Debug Fault Status Register
~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. note:: This register is not specified in PM0056, but it is required
   by ARM.  The bit definitions here are based on the names given in
   the ARM v7-M ARM.

.. doxygendefine:: SCB_DFSR_EXTERNAL
.. doxygendefine:: SCB_DFSR_VCATCH
.. doxygendefine:: SCB_DFSR_DWTTRAP
.. doxygendefine:: SCB_DFSR_BKPT
.. doxygendefine:: SCB_DFSR_HALTED

