.. highlight:: c
.. _libmaple-stm32:

``<libmaple/stm32.h>``
======================

STM32 chip header. This header supplies various series-specific and
chip-specific macros for the current build target.  It's useful both
to abstract away hardware details (e.g. through use of
:ref:`STM32_NR_INTERRUPTS <libmaple-stm32-STM32_NR_INTERRUPTS>`) and
to decide what to do when you want something nonportable (e.g. by
checking :ref:`STM32_MCU_SERIES <libmaple-stm32-STM32_MCU_SERIES>`).

.. contents:: Contents
   :local:

Determining the Target Series
-----------------------------

The STM32 series (e.g. STM32F1, STM32F2, etc.) of the current target
can be inspected with ``STM32_MCU_SERIES``.

.. _libmaple-stm32-STM32_MCU_SERIES:
.. doxygendefine:: STM32_MCU_SERIES

Allowed values for ``STM32_MCU_SERIES`` are the following. This set is
expected to grow over time.

.. doxygendefine:: STM32_SERIES_F1
.. doxygendefine:: STM32_SERIES_F2
.. doxygendefine:: STM32_SERIES_L1
.. doxygendefine:: STM32_SERIES_F4

Series-Specific Characteristics
-------------------------------

The macros in this section are only available on some STM32 series.

STM32F1
~~~~~~~

.. note:: These macros are only available when the current target is
          an STM32F1 series MCU (i.e., when :ref:`STM32_MCU_SERIES
          <libmaple-stm32-STM32_MCU_SERIES>` is ``STM32_SERIES_F1``).

The STM32F1 series is further subdivided into :ref:`lines
<stm32-series-f1-lines>`. The line of the current target can be
inspected with ``STM32_F1_LINE``.

.. doxygendefine:: STM32_F1_LINE

There are five STM32F1 lines. The corresponding values
``STM32_F1_LINE`` can take are the following, though libmaple doesn't
currently support all of them.

.. doxygendefine:: STM32_F1_LINE_VALUE
.. doxygendefine:: STM32_F1_LINE_ACCESS
.. doxygendefine:: STM32_F1_LINE_USB_ACCESS
.. doxygendefine:: STM32_F1_LINE_PERFORMANCE
.. doxygendefine:: STM32_F1_LINE_CONNECTIVITY

MCU Feature Tests
-----------------

The following defines can be used to determine if the target MCU has
a particular feature.

.. _libmaple-stm32-STM32_HAVE_FSMC:
.. doxygendefine:: STM32_HAVE_FSMC
.. doxygendefine:: STM32_HAVE_USB

MCU Characteristics
-------------------

The following defines give salient characteristics of the target MCU.

.. doxygendefine:: STM32_NR_GPIO_PORTS
.. _libmaple-stm32-STM32_NR_INTERRUPTS:
.. doxygendefine:: STM32_NR_INTERRUPTS
.. doxygendefine:: STM32_SRAM_END

Clock Speeds
------------

The macros in this section are related to clock rates.  As such, they
are really part of the configuration of the MCU, rather than inherent
characteristics of the MCU itself.  For instance, it's possible to
change the PCLK1 and PCLK2 clock rates by reconfiguring the :ref:`RCC
<libmaple-rcc>`. libmaple proper never changes any clock rates, but it
does have APIs for doing so (such as :ref:`rcc_configure_pll()
<libmaple-rcc-rcc_configure_pll>`). Because of this, be careful when
using the macros in this section, as they assume that some values are
constant which in fact may be changed.

The values these macros actually take are typically the maximum values
supported by the MCU. Since these are their actual values in practice
(at least in LeafLabs' current use cases, which have the chips running
as fast as possible), they're still considered useful.

.. doxygendefine:: STM32_PCLK1
.. doxygendefine:: STM32_PCLK2

The following macro, ``STM32_DELAY_US_MULT``, is a libmaple
implementation detail. It was included in this public API page in a
previous release by mistake, and is not deprecated, but using it in
your own code is a bad idea.

.. doxygendefine:: STM32_DELAY_US_MULT

Deprecated Macros
-----------------

.. warning:: The macros in this section are deprecated, and are
             available for backwards compatibility only. Do not use
             them in new code.

.. doxygendefine:: PCLK1
.. doxygendefine:: PCLK2
.. doxygendefine:: NR_INTERRUPTS
.. doxygendefine:: NR_GPIO_PORTS
.. doxygendefine:: DELAY_US_MULT
