.. highlight:: c
.. _libmaple-adc:

``<libmaple/adc.h>``
====================

:ref:`Analog to Digital Conversion <adc>` (ADC) support.

A common API for basic ADC functionality is available, but the
characteristics of the ADC peripherals vary slightly across
targets. To manage this, each target defines a small set of datatypes
expressing its capabilities (namely :ref:`adc_extsel_event
<adc-adc_extsel_event>`, :ref:`adc_smp_rate <adc-adc_smp_rate>`, and
:ref:`adc_prescaler <adc-adc_prescaler>`).

.. contents:: Contents
   :local:
   :depth: 2

Devices
-------

The individual ADC peripherals have the following device struct.

.. doxygenstruct:: adc_dev

The available ADC peripherals vary by target. The complete list is
``ADC1``, ``ADC2``, and ``ADC3``.

.. doxygenvariable:: ADC1
.. doxygenvariable:: ADC2
.. doxygenvariable:: ADC3

Functions
---------

Activation and Deactivation
~~~~~~~~~~~~~~~~~~~~~~~~~~~

``adc_enable_single_swstart()`` is simple, portable function, which
enables an ADC and sets it up for its basic usage: performing single
conversions using :ref:`adc_read() <adc-adc_read>`.

.. _adc-adc_enable_single_swstart:
.. doxygenfunction:: adc_enable_single_swstart

The precise software sequence used varies by target, so this is a good
function to use if your program needs to support multiple MCUs. By
default, Wirish calls ``adc_enable_single_swstart()`` on all available
ADCs at ``init()`` time, so Wirish users don't have to call this
function.

There are several other lower-level routines used for activating and
deactivating ADCs:

.. _adc-adc_init:
.. doxygenfunction:: adc_init
.. _adc-adc_enable:
.. doxygenfunction:: adc_enable
.. _adc-adc_disable:
.. doxygenfunction:: adc_disable
.. _adc-adc_disable_all:
.. doxygenfunction:: adc_disable_all

ADC Conversion
~~~~~~~~~~~~~~

``adc_read()`` is a simple function which starts conversion on a
single ADC channel, blocks until it has completed, and returns the
converted result. Don't use the ADC device for any other purpose while
it's running.

.. _adc-adc_read:
.. doxygenfunction:: adc_read

To use ``adc_read()``, the device must be configured appropriately.
You can do this with :ref:`adc_enable_single_swstart()
<adc-adc_enable_single_swstart>`.

Note that for an ADC device to perform conversion on a GPIO input
(which is the usual case; the notable exception being taking
temperature reading), the pin must be configured for analog
conversion. Do this with :ref:`adc_config_gpio()
<adc-adc_config_gpio>`.

Other routines helpful for ADC conversion:

.. _adc-adc_set_reg_seqlen:
.. doxygenfunction:: adc_set_reg_seqlen
.. _adc-adc_set_extsel:
.. doxygenfunction:: adc_set_extsel

.. _adc-adc_extsel_event:

The last of these, :ref:`adc_set_extsel() <adc-adc_set_extsel>`, takes
a target-dependent ``adc_extsel_event`` argument.

STM32F1 Targets
+++++++++++++++

.. doxygenenum:: stm32f1::adc_extsel_event

STM32F2 Targets
+++++++++++++++

.. doxygenenum:: stm32f2::adc_extsel_event

ADC Clock Prescaler
~~~~~~~~~~~~~~~~~~~

``adc_set_prescaler()`` is available for setting the prescaler which
determines the common ADC clock rate. (Wirish sets a sensible default
for this, so Wirish users ordinarily don't need to call this
function.)

.. warning:: Increasing the ADC clock rate does speed conversion time,
   but the ADC peripherals have a maximum clock rate which must not be
   exceeded. Make sure to configure your system and ADC clocks to
   respect your device's maximum rate.

.. _adc_adc_set_prescaler:
.. doxygenfunction:: adc_set_prescaler

.. _adc-adc_prescaler:

ADC prescaler values are target-dependent.

STM32F1 Targets
+++++++++++++++

.. doxygenenum:: stm32f1::adc_prescaler

STM32F2 Targets
+++++++++++++++

.. doxygenenum:: stm32f2::adc_prescaler

.. _adc-adc_set_sample_rate:

ADC Sample Time
~~~~~~~~~~~~~~~

You can control the sampling time (in ADC cycles) for an entire ADC
device using ``adc_set_sample_rate()`` [#fchansamp]_.  This function
**only controls the sample rate**; the total conversion time is equal
to the sample time plus an additional number of ADC cycles. Consult
the reference manual for your chip for more details.

.. warning:: Decreasing ADC sample time speeds conversion, but it also
   decreases the maximum allowable impedance of the voltage source you
   are measuring. If your voltage source has a high impedance
   (e.g. you're measuring Vcc through a potentiometer), and your
   sample time is too low, you will get inaccurate results. Consult
   the datasheet for your target for more details.

.. note:: Wirish sets a sensible default sample rate to allow for
   high-impedance inputs at ``init()`` time, but Wirish users who know
   what they're doing may want to call this function to speed up ADC
   conversion.

.. doxygenfunction:: adc_set_sample_rate

.. _adc-adc_smp_rate:

The ``adc_smp_rate`` argument to :ref:`adc_set_sample_rate()
<adc-adc_set_sample_rate>` is target-dependent.

STM32F1 Targets
+++++++++++++++

.. doxygenenum:: stm32f1::adc_smp_rate

STM32F2 Targets
+++++++++++++++

.. doxygenenum:: stm32f2::adc_smp_rate

Miscellaneous
~~~~~~~~~~~~~

.. FIXME [0.0.13] why don't adc_config_gpio()'s docs show up?

.. _adc-adc_foreach:
.. doxygenfunction:: adc_foreach

.. _adc-adc_config_gpio:
.. doxygenfunction:: adc_config_gpio

STM32F1 only
~~~~~~~~~~~~

The following routines are available only on STM32F1 targets.

.. _adc-adc_set_exttrig:
.. doxygenfunction:: adc_set_exttrig

``adc_calibrate()`` performs calibration necessary on STM32F1 before
using an ADC.  Note that on STM32F1 targets,
:ref:`adc_enable_single_swstart() <adc-adc_enable_single_swstart>`
calls ``adc_calibrate()``, so there's no need to do it separately.

.. _adc-adc_calibrate:
.. doxygenfunction:: adc_calibrate

Register Maps
-------------

Individual ADC peripherals have the following register map. The base
pointers are ``ADC1_BASE``, ``ADC2_BASE``, and ``ADC3_BASE``.

.. _adc-adc_reg_map:
.. doxygenstruct:: adc_reg_map

On **STM32F2 targets**, there is an additional common set of registers
shared by all ADC peripherals. Its base pointer is
``ADC_COMMON_BASE``.

.. _adc-adc_common_reg_map:
.. doxygenstruct:: stm32f2::adc_common_reg_map

Register Bit Definitions
------------------------

.. TODO [0.0.13]

TODO

.. rubric:: Footnotes

.. [#fchansamp] Per-channel sample time configuration is possible,
   but currently unsupported.
