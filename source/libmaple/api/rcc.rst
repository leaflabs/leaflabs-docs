.. highlight:: c
.. _libmaple-rcc:

``<libmaple/rcc.h>``
====================

Reset and Clock Control (RCC) support.

The RCC is responsible for managing the MCU's various clocks. This
includes the core clock SYSCLK, which determines the CPU clock
frequency, as well as the clock lines that drive peripherals.

Because of this, the available RCC functionality varies by target.
There are a :ref:`variety of abstractions <libmaple-rcc-core-types>`
in place to make managing this more convenient.

.. contents:: Contents
   :local:
   :depth: 2

.. _libmaple-rcc-core-types:

Core Types
----------

The core abstractions in place are
:ref:`rcc_clk_id <libmaple-rcc-rcc_clk_id>`,
:ref:`rcc_clk <libmaple-rcc-rcc_clk>`,
:ref:`rcc_sysclk_src <libmaple-rcc-rcc_sysclk_src>`,
:ref:`rcc_clk_domain <libmaple-rcc-rcc_clk_domain>`, and
:ref:`rcc_prescaler <libmaple-rcc-rcc_prescaler>`.

.. _libmaple-rcc-rcc_clk_id:

Peripheral Identifiers: ``rcc_clk_id``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

``rcc_clk_id`` is an enum used to identify peripherals. The RCC
back-ends use them to look up a peripheral's bus and clock line, but
they are also generally useful as unique identifiers for each
peripheral.  You can manage peripherals using their ``rcc_clk_id``\ s
with :ref:`these functions <libmaple-rcc-clk-id-funcs>`.

Peripherals which are common across targets have the same token
(though not necessarily the same value) for their ``rcc_clk_id``
across different targets. For example, the ``rcc_clk_id`` for the ADC1
peripheral is always ``RCC_ADC1`` regardless of the target.
Additionally, as explained in :ref:`libmaple-overview-devices`, each
peripheral device type struct contains the ``rcc_clk_id`` for that
peripheral in a ``clk_id`` field.

The available ``rcc_clk_id``\ s on each supported target series are as
follows.

STM32F1 Targets
+++++++++++++++

.. doxygenenum:: stm32f1::rcc_clk_id

STM32F2 Targets
+++++++++++++++

.. doxygenenum:: stm32f2::rcc_clk_id

.. _libmaple-rcc-rcc_sysclk_src:

System Clock (SYSCLK) Sources: ``rcc_sysclk_src``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

SYSCLK is the core system clock. It determines the CPU clock rate, and
it's the base clock which is used to drive (most of) the peripherals
on the STM32. ``rcc_sysclk_src`` is an enum for the possible SYSCLK
sources. Switch the SYSCLK source with :ref:`rcc_switch_sysclk()
<libmaple-rcc-rcc_switch_sysclk>`.

.. doxygenenum:: rcc_sysclk_src

As a special case, you can configure the PLL with a call to
:ref:`rcc_configure_pll() <libmaple-rcc-rcc_configure_pll>`.

.. _libmaple-rcc-rcc_clk:

System and Secondary Clock Sources: ``rcc_clk``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The ``rcc_clk`` type gives available system and secondary clock
sources (e.g. HSI, HSE, LSE). As with :ref:`rcc_clk_id
<libmaple-rcc-rcc_clk_id>`, clock sources which are common across
targets have the same token, but not necessarily the same value, for
their ``rcc_clk`` on each target.  A variety of :ref:`clock management
functions <libmaple-rcc-clk-funcs>` are available.

Note that the inclusion of secondary clock sources, like LSI and LSE,
makes ``rcc_clk`` different from the SYSCLK sources, which are managed
using :ref:`rcc_sysclk_src <libmaple-rcc-rcc_sysclk_src>`.

The available ``rcc_clk``\ s for each supported target series are as
follows.

STM32F1 Targets
+++++++++++++++

.. doxygenenum:: stm32f1::rcc_clk

STM32F2 Targets
+++++++++++++++

.. doxygenenum:: stm32f2::rcc_clk

.. _libmaple-rcc-rcc_clk_domain:

Clock Domains: ``rcc_clk_domain``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

These specify the available clock domains.  For example, each AHB and
APB is a clock domain.

This type mostly exists to enable asking devices what bus they're on,
which, given knowledge of your system's clock configuration, can be
useful when making decisions about prescalers, etc.

Given an :ref:`rcc_clk_id <libmaple-rcc-rcc_clk_id>`, you can get the
peripheral's clock domain with :ref:`rcc_dev_clk()
<libmaple-rcc-rcc_dev_clk>`.  Clock domains that are common across
series have the same token (but not necessarily the same value) for
their corresponding ``rcc_clk_domain``.

The available ``rcc_clk_domain``\ s for each supported target series
are as follows.

STM32F1 Targets
+++++++++++++++

.. doxygenenum:: stm32f1::rcc_clk_domain

STM32F2 Targets
+++++++++++++++

.. doxygenenum:: stm32f2::rcc_clk_domain

.. _libmaple-rcc-rcc_prescaler:

Prescalers: ``rcc_prescaler`` and Friends
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Available prescalers are managed via the ``rcc_prescaler`` type, the
``rcc_set_prescaler()`` function, and a variety of related prescaler
divider types.  See :ref:`libmaple-rcc-prescalers` for more
information and usage notes.

Functions
---------

.. _libmaple-rcc-sysclk-funcs:
.. _libmaple-rcc-rcc_switch_sysclk:

SYSCLK Management
~~~~~~~~~~~~~~~~~

Change the SYSCLK source with ``rcc_switch_sysclk()``.

.. doxygenfunction:: rcc_switch_sysclk

.. _libmaple-rcc-rcc_configure_pll:

PLL Configuration
~~~~~~~~~~~~~~~~~

You can configure the PLL with ``rcc_configure_pll()``.  This takes an
``rcc_pll_cfg`` struct as its argument.  Though the definition of
``rcc_pll_cfg`` is common across series, its contents are entirely
target-dependent.

.. doxygenstruct:: rcc_pll_cfg
.. _rcc-rcc_configure_pll:
.. doxygenfunction:: rcc_configure_pll

The fields in an ``rcc_pll_cfg`` on each target are as follows.

rcc_pll_cfg on STM32F1 Targets
++++++++++++++++++++++++++++++

The ``pllsrc`` field is chosen from the following.

.. doxygenenum:: stm32f1::rcc_pllsrc

.. FIXME [0.0.13] We've got plans to redo this; make sure you watch
.. libmaple for changes here.

The ``data`` field must point to a ``struct stm32f1_rcc_pll_data``.
This just contains an ``rcc_pll_multiplier``.

.. doxygenenum:: stm32f1::rcc_pll_multiplier

.. doxygenstruct:: stm32f1::stm32f1_rcc_pll_data

rcc_pll_cfg on STM32F2 Targets
++++++++++++++++++++++++++++++

The ``pllsrc`` field is chosen from the following.

.. doxygenenum:: stm32f2::rcc_pllsrc

The ``data`` field must point to a ``struct stm32f2_rcc_pll_data``.

.. doxygenstruct:: stm32f2::stm32f2_rcc_pll_data

.. _libmaple-rcc-clk-funcs:

System and Secondary Clock Management
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

These functions are useful for managing clocks via their :ref:`rcc_clk
<libmaple-rcc-rcc_clk>`.

.. doxygenfunction:: rcc_turn_on_clk
.. doxygenfunction:: rcc_turn_off_clk
.. doxygenfunction:: rcc_is_clk_on
.. doxygenfunction:: rcc_is_clk_ready

.. _libmaple-rcc-clk-id-funcs:

Peripheral Management
~~~~~~~~~~~~~~~~~~~~~

These functions are useful for managing peripherals via their
:ref:`rcc_clk_id <libmaple-rcc-rcc_clk_id>`.

.. _libmaple-rcc-rcc_clk_enable:
.. doxygenfunction:: rcc_clk_enable
.. doxygenfunction:: rcc_reset_dev
.. _libmaple-rcc-rcc_dev_clk:
.. doxygenfunction:: rcc_dev_clk

.. _libmaple-rcc-prescalers:

Prescaler Management
~~~~~~~~~~~~~~~~~~~~

All clock prescalers managed by RCC can be controlled with a single
function, ``rcc_set_prescaler()``.

.. doxygenfunction:: rcc_set_prescaler

The arguments to ``rcc_set_prescaler()`` are target-dependent, but
follow a common pattern:

- The first argument is the prescaler to set, so there's one for each
  peripheral clock domain, etc.  These have names like
  ``RCC_PRESCALER_FOO``, e.g. ``RCC_PRESCALER_APB1``.  Choose the
  prescaler from the ``rcc_prescaler``\ s on your target (see below).

- The second argument is the actual clock divider to use; it's chosen
  based on the first argument. The dividers for ``RCC_PRESCALER_FOO``
  are given by the type ``rcc_foo_divider``, and have values like
  ``RCC_FOO_xxx_DIV_y``. This means that the foo clock will be the
  ``xxx`` clock divided by ``y``.

For example, calling ``rcc_set_prescaler(RCC_PRESCALER_APB1,
RCC_APB1_HCLK_DIV_1)`` would set the APB1 clock to HCLK divided by 1.

Prescalers which are common across targets have the same token, though
not necessarily the same value, for their ``rcc_prescaler`` (for
example, ``RCC_PRESCALER_APB1`` is available on both STM32F1 and
STM32F2 targets). The available prescalers and dividers on each
supported target series are as follows.

STM32F1 Targets
+++++++++++++++

.. doxygenenum:: stm32f1::rcc_prescaler
.. doxygenenum:: stm32f1::rcc_adc_divider
.. doxygenenum:: stm32f1::rcc_apb1_divider
.. doxygenenum:: stm32f1::rcc_apb2_divider
.. doxygenenum:: stm32f1::rcc_ahb_divider

STM32F2 Targets
+++++++++++++++

.. doxygenenum:: stm32f2::rcc_prescaler
.. doxygenenum:: stm32f2::rcc_mco2_divider
.. doxygenenum:: stm32f2::rcc_mco1_divider
.. doxygenenum:: stm32f2::rcc_rtc_divider
.. doxygenenum:: stm32f2::rcc_apb2_divider
.. doxygenenum:: stm32f2::rcc_apb1_divider
.. doxygenenum:: stm32f2::rcc_ahb_divider

Register Maps
-------------

These vary by target. The base pointer is always ``RCC_BASE``.

.. doxygendefine:: RCC_BASE

STM32F1 Targets
~~~~~~~~~~~~~~~

.. doxygenstruct:: stm32f1::rcc_reg_map

STM32F2 Targets
~~~~~~~~~~~~~~~

.. doxygenstruct:: stm32f2::rcc_reg_map

Register Bit Definitions
------------------------

These are given as source code.  Available register bit definitions
vary by target.

.. We need this include to avoid crashing Emacs's ReST parser. Yuck.

.. include:: rcc-reg-bits.txt

Deprecated Functionality
------------------------

.. _rcc-rcc_clk_init:
.. doxygenfunction:: stm32f1::rcc_clk_init

To replace a call to ``rcc_clk_init()`` in order to set SYSCLK to PLL
driven by an external oscillator, you can use something like this,
which is portable except for the initialization of ``your_pll_cfg``::

    /* You need to make this point to something valid for your target; see
     * the documentation for rcc_configure_pll() for more details. */
    extern rcc_pll_cfg *your_pll_cfg;

    void pll_reconfigure() {
        /* Turn on HSI using rcc_turn_on_clk() and wait for it to
         * become ready by busy-waiting on rcc_is_clk_ready().
         *
         * Switch to HSI to ensure we're not using the PLL while we
         * reconfigure it. */
        rcc_turn_on_clk(RCC_CLK_HSI);
        while (!rcc_is_clk_ready(RCC_CLK_HSI))
            ;
        rcc_switch_sysclk(RCC_CLKSRC_HSI);

        /* Turn off HSE and the PLL, or we can't reconfigure it. */
        rcc_turn_off_clk(RCC_CLK_PLL);
        rcc_turn_off_clk(RCC_CLK_HSE);

        /* Reconfigure the PLL. You can also perform any other
         * prescaler management here. */
        rcc_configure_pll(your_pll_cfg);

        /* Turn on RCC_CLK_HSE. */
        rcc_turn_on_clk(RCC_CLK_HSE);
        while (!rcc_is_clk_ready(RCC_CLK_HSE))
            ;

        /* Turn on RCC_CLK_PLL. */
        rcc_turn_on_clk(RCC_CLK_PLL);
        while (!rcc_is_clk_ready(RCC_CLK_PLL))
            ;

        /* Finally, switch to the PLL. */
        rcc_switch_sysclk(RCC_CLKSRC_PLL);
    }
