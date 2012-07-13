.. highlight:: c

What's New
==========

.. FIXME [RELEASE] finish.

This page tracks updates to libmaple and MapleIDE.

.. contents::
   :local:
   :depth: 1

v0.0.13
-------

.. We started doing this as we updated the docs on 29 Jun 2012, so
.. updates before then need to be pulled from libmaple's Git logs.

**General Changes**

- Additional STM32 support: for this release, libmaple was taught
  how to target STM32F1 value line (thanks to Anton Eltchaninov) and
  STM32F2 series microcontrollers.  It learned a huge bag of new
  tricks as a result, so this list is only a summary of the most
  important changes.

- New include style: You should now include libmaple and Wirish
  headers like this (respectively)::

      #include <libmaple/libmaple.h>
      #include <wirish/wirish.h>

  The old include style (e.g. ``#include "libmaple.h"``) is now
  **deprecated**, and will **break in the next release**. This is more
  standard usage for libraries, and was necessary to e.g. allow for
  implementing a Wiring/Arduino-style SPI library (which is included
  as ``#include "SPI.h"`` and clashes with :ref:`libmaple-spi` on
  case-insensitive filesystems like OS X's).

- :ref:`Windows instructions <toolchain-win-setup>` for the
  :ref:`unix-toolchain`.

**Wirish**

- Wire I2C library: New, improved, and more Arduino-compatible
  :ref:`Wire <libs-wire>` library, thanks to Trystan Jones.

**libmaple proper**

Better documentation: The old documentation for libmaple's C layer did
little more than list the Doxygen comments in the source code. It now
includes explanatory material and usage notes. See
:ref:`libmaple-apis`.

.. FIXME [0.0.13] this is ugly

Major changes by header follow.

.. list-table::
   :header-rows: 1
   :widths: 1 10

   * - Header
     - Changes

   * - :ref:`libmaple-rcc`
     - :ref:`rcc_clk_init() <rcc-rcc_clk_init>` is deprecated. Use
       :ref:`rcc_configure_pll() <libmaple-rcc-rcc_configure_pll>` as
       the basis for a portable replacement; see the
       ``rcc_clk_init()`` docs for a porting guide.

   * - :ref:`libmaple-libmaple_types`
     - Various new attributes and type qualifiers.

   * - :ref:`libmaple-adc`
     - New :ref:`adc_enable_single_swstart()
       <adc-adc_enable_single_swstart>` and :ref:`adc_config_gpio()
       <adc-adc_config_gpio>`, for portably enabling ADC peripherals
       and their associated pins for use with :ref:`adc_read()
       <adc-adc_read>`.
