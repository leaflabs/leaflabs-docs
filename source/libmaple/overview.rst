.. highlight:: c

.. _libmaple-overview:

Overview
========

This page is a general overview of :ref:`libmaple proper
<libmaple-vs-wirish>`.  It describes libmaple's design, and names
implementation patterns to look for when using it.  General
familiarity with the :ref:`STM32 <stm32>` is assumed; beginners should
start with the high-level :ref:`Wirish interface <language>` instead.
Examples are given from libmaple's sources.

.. contents:: Contents
   :local:

Design Goals
------------

The central goal for libmaple proper is to provide a pleasant,
portable, and consistent set of interfaces for dealing with the
various series of STM32 microcontrollers.

Portability in particular can be a problem when programming for the
STM32. While the various STM32 series are largely pin-compatible with
one another, the peripheral register maps between series often change
drastically, even when the functionality provided by the peripheral
doesn't change very much. This means that code which accesses
registers directly often needs to change when porting a program to a
different series MCU.

ST's solution to this problem thus far has been to `issue
<http://www.st.com/internet/com/SOFTWARE_RESOURCES/SW_COMPONENT/FIRMWARE/stm32l1_stdperiph_lib.zip>`_
`separate
<http://www.st.com/internet/com/SOFTWARE_RESOURCES/SW_COMPONENT/FIRMWARE/stm32f10x_stdperiph_lib.zip>`_
`firmware
<http://www.st.com/internet/com/SOFTWARE_RESOURCES/SW_COMPONENT/FIRMWARE/stm32f2xx_stdperiph_lib.zip>`_
`libraries
<http://www.st.com/internet/com/SOFTWARE_RESOURCES/SW_COMPONENT/FIRMWARE/stm32f4_dsp_stdperiph_lib.zip>`_;
one for each STM32 series.  Along with these, they have released a
`number
<http://www.st.com/internet/com/TECHNICAL_RESOURCES/TECHNICAL_LITERATURE/APPLICATION_NOTE/DM00024853.pdf>`_
of `application
<http://www.st.com/internet/com/TECHNICAL_RESOURCES/TECHNICAL_LITERATURE/APPLICATION_NOTE/DM00033267.pdf>`_
`notes
<http://www.st.com/internet/com/TECHNICAL_RESOURCES/TECHNICAL_LITERATURE/APPLICATION_NOTE/DM00032987.pdf>`_
describing the compatibility issues and how to migrate between series
by switching firmware libraries. Often, the migration advice is
essentially "rewrite your code"; this occurs, for example, with any
code involving GPIO or DMA being migrated between STM32F1 and STM32F2.

Needless to say, this can be very annoying.  (Didn't we solve this
sort of problem years ago?)  When you just want your robot to fly,
your `LEDs to blink <http://www.youtube.com/watch?v=J845L45zqfk>`_, or
your `FM synthesizer <https://github.com/Ixox/preen>`_ to, well,
`synthesize <http://xhosxe.free.fr/IxoxFMSynth.mp3>`_, you probably
couldn't care less about dealing with a new set of registers.

We want to make it easier to write portable STM32 code. To enable
that, libmaple abstracts away many hardware details behind portable
interfaces. We also want to make it easy for you to get your hands
dirty when need or desire arises. To that end, libmaple makes as few
assumptions as possible, and does its best to get out of your way when
you want it to leave.

.. _libmaple-overview-devices:

Libmaple's Device Model
-----------------------

The libmaple device model is simple and stupid. This is a feature.

*Device types* are the central libmaple abstraction; they exist to
provide portable interfaces to common peripherals, but they still let
you do nonportable things easily if you want to.

The rules for device types are:

- Device types are structs representing peripherals.  The name of the
  device type for peripheral "foo" is ``struct foo_dev`` (so for
  foo=ADC, it's ``struct adc_dev``. For foo=DMA, it's ``struct
  dma_dev``; etc.). These are always ``typedef``\ ed to ``foo_dev``.

- Each device type contains any information needed or used by libmaple
  for operating on the peripheral the type represents. Device types
  are defined alongside declarations for portable support routines in
  the header ``<libmaple/foo.h>`` (examples: :ref:`libmaple-adc`,
  :ref:`libmaple-dma`).

- Direct :ref:`register access <libmaple-overview-regmaps>` is
  possible via the ``regs`` field in each device type.  (Given a
  ``foo_dev *foo``, you can read and write the BAR register
  ``FOO_BAR`` with ``foo->regs->BAR``.)

- An :ref:`rcc_clk_id <libmaple-rcc-rcc_clk_id>` for the device is
  available in the ``clk_id`` field; this is an opaque type that can
  be used to uniquely identifies the peripheral. (Given ``foo_dev
  *foo``, you can check which foo you have by looking at
  ``foo->clk_id``.)

- The backend for each supported STM32 series statically initializes
  devices as appropriate, and ensures that the peripheral support
  header includes declarations for pointers to these statically
  allocated devices.

- Peripheral support functions usually expect a pointer to a device as
  their first argument.  These functions' implementations may vary
  with the particular microcontroller you're targeting, but their
  semantics try to stay the same. To migrate to a different target,
  you'll often be able to simply recompile your program (and libmaple)
  for the new target.

- When complete portability is not possible, libmaple tries to keep
  the nonportable bits in data, rather than code.

Example: ``adc_dev``
~~~~~~~~~~~~~~~~~~~~

These rules are best explained by example. The device type for ADC
peripherals is ``struct adc_dev``. Its definition is provided by
``<libmaple/adc.h>``::

    typedef struct adc_dev {
        adc_reg_map *regs;
        rcc_clk_id clk_id;
    } adc_dev;

An ``adc_dev`` contains a pointer to its register map in the ``regs``
field. This ``regs`` field is available on all device types. Its value
is a :ref:`register map base pointer
<libmaple-overview-regmaps-base-pts>` (like ``ADC1_BASE``, etc.)  for
the peripheral, as determined by the current target. For example, two
equivalent expressions for reading the ADC1 regular data register are
``ADC1_BASE->DR`` and ``ADC1->regs->DR`` (though the first one is
faster).  Manipulating registers directly via ``->regs`` is thus
always possible, but can be nonportable, and should you choose to do
this, it's up to you to get it right.

An ``adc_dev`` also contains an ``rcc_clk_id`` for the ADC peripheral
it represents in the ``clk_id`` field.  The ``rcc_clk_id`` enum type
has an enumerator for each peripheral supported by your series. For
example, the ADC peripherals' ``rcc_clk_id`` enumerators are
``RCC_ADC1``, ``RCC_ADC2``, and ``RCC_ADC3``.  In general, an
``rcc_clk_id`` is useful not only for managing the clock line to a
peripheral, but also as a unique identifier for that peripheral.

(Device types can be more complicated than this; ``adc_dev`` was
chosen as a simple example of the minimum you can expect.)

Rather than have you define your own ``adc_dev``\ s, libmaple defines
them for you as appropriate for your target STM32 series. For example,
on STM32F1, the file libmaple/stm32f1/adc.c contains the following::

    static adc_dev adc1 = {
        .regs   = ADC1_BASE,
        .clk_id = RCC_ADC1,
    };
    /** ADC1 device. */
    const adc_dev *ADC1 = &adc1;

    static adc_dev adc2 = {
        .regs   = ADC2_BASE,
        .clk_id = RCC_ADC2,
    };
    /** ADC2 device. */
    const adc_dev *ADC2 = &adc2;

    #if defined(STM32_HIGH_DENSITY) || defined(STM32_XL_DENSITY)
    static adc_dev adc3 = {
        .regs   = ADC3_BASE,
        .clk_id = RCC_ADC3,
    };
    /** ADC3 device. */
    const adc_dev *ADC3 = &adc3;
    #endif

Since all supported STM32F1 targets support ADC1 and ADC2, libmaple
predefines corresponding ``adc_dev`` instances for you. To save space,
it avoids defining an ``adc_dev`` for ADC3 unless you are targeting a
high- or XL-density STM32F1, as medium- and lower density MCUs don't
have ADC3.

Note that the structs themselves are static and are exposed only via
pointers.  These pointers are declared in a series-specific ADC
header, ``<series/adc.h>`` which is included by ``<libmaple/adc.h>``
based on the MCU you're targeting.  (**Never include <series/foo.h>
directly**.  Instead, include ``<libmaple/foo.h>`` and let it take
care of that for you.)  On STM32F1, the series ADC header contains the
following::

    extern const struct adc_dev *ADC1;
    extern const struct adc_dev *ADC2;
    #if defined(STM32_HIGH_DENSITY) || defined(STM32_XL_DENSITY)
    extern const struct adc_dev *ADC3;
    #endif

In general, you access the predefined devices via these pointers. As
illustrated by the ADC example, the variables for these pointers
follow the naming scheme used in ST's reference manuals -- the pointer
to ADC1's ``adc_dev`` is named ``ADC1``, and so on.

The :ref:`API documentation <libmaple-apis>` for the peripherals
you're interested in will list the available devices on each target.

Using Devices
~~~~~~~~~~~~~

Peripheral support routines usually expect pointers to their device
types as their first arguments. Here are some ADC examples::

    uint16 adc_read(const adc_dev *dev, uint8 channel);
    static inline void adc_enable(const adc_dev *dev);
    static inline void adc_disable(const adc_dev *dev);

So, to read channel 2 of ADC1, you could call ``adc_read(ADC1, 2)``.
To disable ADC2, call ``adc_disable(ADC2)``; etc.

That's it; there's nothing complicated here. In general, just follow
links from the :ref:`libmaple-apis` page to the header for the
peripheral you're interested in. It will explain the supported
functionality, both portable and series-specific.

Segregating Non-portable Functionality into Data
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

As mentioned previously, when total portability isn't possible,
libmaple tries to do the right thing and segregate the nonportable
portions into data rather than code. The function
``adc_set_sample_rate()`` is a good example of how this works, and why
it's useful::

    void adc_set_sample_rate(const adc_dev *dev, adc_smp_rate smp_rate);

For example, while both STM32F1 and STM32F2 support setting the ADC
sample time via the same register interface, the actual sample times
supported are different. For instance, on STM32F1, available sample
times include 1.5, 7.5, and 13.5 ADC cycles. On STM32F2, none of these
are available, but 3, 15, and 28 ADC cycles are supported (which is
not true for STM32F1). To work with this, libmaple provides a single
function, ``adc_set_sample_rate()``, for setting an ADC controller's
channel sampling time, but the actual sample rates it takes are given
by the ``adc_smp_rate`` type, which is different on STM32F1 and
STM32F2.

This is the STM32F1 implementation of adc_smp_rate::

    typedef enum adc_smp_rate {
        ADC_SMPR_1_5,               /**< 1.5 ADC cycles */
        ADC_SMPR_7_5,               /**< 7.5 ADC cycles */
        ADC_SMPR_13_5,              /**< 13.5 ADC cycles */
        ADC_SMPR_28_5,              /**< 28.5 ADC cycles */
        ADC_SMPR_41_5,              /**< 41.5 ADC cycles */
        ADC_SMPR_55_5,              /**< 55.5 ADC cycles */
        ADC_SMPR_71_5,              /**< 71.5 ADC cycles */
        ADC_SMPR_239_5,             /**< 239.5 ADC cycles */
    } adc_smp_rate;

And here is the STM32F2 implementation::

    typedef enum adc_smp_rate {
        ADC_SMPR_3,                 /**< 3 ADC cycles */
        ADC_SMPR_15,                /**< 15 ADC cycles */
        ADC_SMPR_28,                /**< 28 ADC cycles */
        ADC_SMPR_56,                /**< 56 ADC cycles */
        ADC_SMPR_84,                /**< 84 ADC cycles */
        ADC_SMPR_112,               /**< 112 ADC cycles */
        ADC_SMPR_144,               /**< 144 ADC cycles */
        ADC_SMPR_480,               /**< 480 ADC cycles */
    } adc_smp_rate;

So, on F1, you could call ``adc_set_sample_rate(ADC1, ADC_SMPR_1_5)``,
and on F2, you could call ``adc_set_sample_rate(ADC1,
ADC_SMPR_3)``. If you're only interested in one of those series, then
that's all you need to know.

However, if you're targeting multiple series, then this is useful
because it lets you put the actual sample time for the MCU you're
targeting into a variable (or macro, etc.), whose value depends on the
target you're compiling for. This lets you have a single codebase to
test and maintain, and lets you add support for a new target by simply
adding some new data.

To continue the example, one easy way is to pick an ``adc_smp_rate``
for each of STM32F1 and STM32F2 is with conditional compilation. Using
the :ref:`STM32_MCU_SERIES <libmaple-stm32-STM32_MCU_SERIES>` define
from :ref:`libmaple-stm32`, you can write::

    #include <libmaple/adc.h>
    #include <libmaple/stm32.h>

    #if STM32_MCU_SERIES == STM32_SERIES_F1
    /* Target is an STM32F1 */
    adc_smp_rate smp_rate = ADC_SMPR_1_5;
    #elif STM32_MCU_SERIES == STM32_SERIES_F2
    /* Target is an STM32F2 */
    adc_smp_rate smp_rate = ADC_SMPR_3;
    #else
    #error "Unsupported STM32 target; can't pick a sample rate"
    #endif

    void setup(void) {
        adc_set_smp_rate(ADC1, smp_rate);
    }

Adding support for e.g. STM32F4 would only require adding a new
``#elif`` for that series. This is simple, but hackish, and can get
out of control if you're not careful.

Another way to get the job done is to declare an ``extern adc_smp_rate
smp_rate``, and use the build system to compile a file defining
``smp_rate`` depending on your target. As was discussed earlier, this
is what libmaple does when choosing which files to use for defining
the appropriate ``adc_dev``\ s for your target. How to do this is
outside the scope of this overview, however.

.. _libmaple-overview-regmaps:

Register Maps
-------------

Though we aim to enable libmaple's users to interact with the more
portable :ref:`device interface <libmaple-overview-devices>` as much
as possible, there will always be a need for efficient direct register
access.  To allow for that, libmaple provides *register maps* as a
consistent set of names and abstractions for dealing with peripheral
registers and their bits.

A *register map type* is a struct which names and provides access to a
peripheral's registers (we can use a struct because registers are
usually mapped into contiguous regions of memory). Here's an example
register map for the DAC peripheral on STM32F1 series MCUs (``__io``
is just libmaple's way of saying ``volatile`` when referring to
register values)::

    typedef struct dac_reg_map {
        __io uint32 CR;      /**< Control register */
        __io uint32 SWTRIGR; /**< Software trigger register */
        __io uint32 DHR12R1; /**< Channel 1 12-bit right-aligned data
                                  holding register */
        __io uint32 DHR12L1; /**< Channel 1 12-bit left-aligned data
                                  holding register */
        __io uint32 DHR8R1;  /**< Channel 1 8-bit left-aligned data
                                  holding register */
        __io uint32 DHR12R2; /**< Channel 2 12-bit right-aligned data
                                  holding register */
        __io uint32 DHR12L2; /**< Channel 2 12-bit left-aligned data
                                  holding register */
        __io uint32 DHR8R2;  /**< Channel 2 8-bit left-aligned data
                                  holding register */
        __io uint32 DHR12RD; /**< Dual DAC 12-bit right-aligned data
                                  holding register */
        __io uint32 DHR12LD; /**< Dual DAC 12-bit left-aligned data
                                  holding register */
        __io uint32 DHR8RD;  /**< Dual DAC 8-bit right-aligned data holding
                                  register */
        __io uint32 DOR1;    /**< Channel 1 data output register */
        __io uint32 DOR2;    /**< Channel 2 data output register */
    } dac_reg_map;

There are two things to notice here.  First, if the chip reference
manual (for STM32F1, that's RM0008) names a register ``DAC_FOO``, then
``dac_reg_map`` has a field named ``FOO``.  So, the Channel 1 12-bit
right-aligned data register (DAC_DHR12R1) is the ``DHR12R1`` field in
a ``dac_reg_map``.  Second, if the reference manual describes a
register as "Foo bar register", the documentation for the
corresponding field has the same description.  This consistency makes
it easy to search for a particular register, and, if you see one used
in a source file, to feel sure about what's going on just based on its
name.

.. _libmaple-overview-regmaps-base-pts:

So let's say you've included ``<libmaple/foo.h>``, and you want to
mess with some particular register. You'll do this using *register map
base pointers*, which are pointers to ``struct foo_reg_map``. What's
the name of the base pointer you want?  That depends on if there's
more than one foo or not.  If there's only one foo, then libmaple
guarantees there will be a ``#define`` that looks like like this::

    #define FOO_BASE    ((struct foo_reg_map*)0xDEADBEEF)

That is, you're guaranteed there will be a pointer to the (only)
``foo_reg_map`` you want, and it will be called
``FOO_BASE``. (``0xDEADBEEF`` is the register map's *base address*, or
the fixed location in memory where the register map begins).  Here's
an example for STM32F1::

    #define DAC_BASE    ((struct dac_reg_map*)0x40007400)

Here are some examples for how to read and write to registers using
register map base pointers.

* In order to write 2048 to the channel 1 12-bit left-aligned data
  holding register (DAC_DHR12L1), you would write::

      DAC_BASE->DHR12L1 = 2048;

* In order to read the DAC control register, you would write::

      uint32 cr = DAC_BASE->CR;

That covers the case where there's a single foo peripheral.  If
there's more than one (say, if there are *n*), then
``<libmaple/foo.h>`` provides the following::

    #define FOO1_BASE    ((struct foo_reg_map*)0xDEADBEEF)
    #define FOO2_BASE    ((struct foo_reg_map*)0xF00DF00D)
    ...
    #define FOOn_BASE    ((struct foo_reg_map*)0x1EAF1AB5)

Here are some examples for the ADCs on STM32F1::

    #define ADC1_BASE    ((struct adc_reg_map*)0x40012400)
    #define ADC2_BASE    ((struct adc_reg_map*)0x40012800)

In order to read from the ADC1's regular data register (where the
results of ADC conversion are stored), you would write::

    uint32 converted_result = ADC1_BASE->DR;

Register Bit Definitions
------------------------

In ``<libmaple/foo.h>``, there will also be a variety of ``#define``\
s for dealing with interesting bits in the xxx registers, called
*register bit definitions*.  In keeping with the ST reference manuals,
these are named according to the scheme ``FOO_REG_FIELD``, where
"``REG``" refers to the register, and "``FIELD``" refers to the bit or
bits in ``REG`` that are special.

Again, this is probably best explained by example.  On STM32F1, each
Direct Memory Access (DMA) controller's register map has a certain
number of channel configuration registers (DMA_CCRx).  In each of
these channel configuration registers, bit 14 is called the
``MEM2MEM`` bit, and bits 13 and 12 are the priority level (``PL``)
bits.  Here are the register bit definitions for those fields on
STM32F1::

    #define DMA_CCR_MEM2MEM_BIT             14
    #define DMA_CCR_MEM2MEM                 (1U << DMA_CCR_MEM2MEM_BIT)
    #define DMA_CCR_PL                      (0x3 << 12)
    #define DMA_CCR_PL_LOW                  (0x0 << 12)
    #define DMA_CCR_PL_MEDIUM               (0x1 << 12)
    #define DMA_CCR_PL_HIGH                 (0x2 << 12)
    #define DMA_CCR_PL_VERY_HIGH            (0x3 << 12)

Thus, to check if the ``MEM2MEM`` bit is set in DMA controller 1's
channel configuration register 2 (DMA_CCR2), you can write::

    if (DMA1_BASE->CCR2 & DMA_CCR_MEM2MEM) {
        /* MEM2MEM is set */
    }

Certain register values occupy multiple bits.  For example, the
priority level (PL) of a DMA channel is determined by bits 13 and 12
of the corresponding channel configuration register.  As shown above,
libmaple provides several register bit definitions for masking out the
individual PL bits and determining their meaning.  For example, to set
the priority level of a DMA transfer to "high priority", you can
do a read-modify-write sequence on the DMA_CCR_PL bits like so::

    uint32 ccr = DMA1_BASE->CCR2;
    ccr &= ~DMA_CCR_PL;
    ccr |= DMA_CCR_PL_HIGH;
    DMA1_BASE->CCR2 = ccr;

Of course, before doing that, you should check to make sure there's
not already a device-level function for performing the same task!  (In
this case, there is. It's called :c:func:`dma_set_priority()`; see
:ref:`libmaple-dma`.) For instance, **none of the above code is
portable** to STM32F4, which uses DMA streams instead of channels for
this purpose.

Peripheral Support Routines
---------------------------

This section describes patterns to look for in peripheral support
routines.

In general, each device needs to be initialized before it can be used.
libmaple provides this initialization routine for each peripheral
``foo``; its name is ``foo_init()``.  These initialization routines
turn on the clock to a device, and restore its register values to
their default settings.  Here are a few examples::

    /* From <libmaple/dma.h> */
    void dma_init(dma_dev *dev);

    /* From <libmaple/gpio.h> */
    void gpio_init(gpio_dev *dev);
    void gpio_init_all(void);

Note that, sometimes, there will be an additional initialization
routine for all available peripherals of a certain kind.

Many peripherals also need additional configuration before they can be
used.  These functions are usually called something along the lines of
``foo_enable()``, and often take additional arguments which specify a
particular configuration for the peripheral.  Some examples::

    /* From <libmaple/usart.h> */
    void usart_enable(usart_dev *dev);

    /* From <libmaple/i2c.h> */
    void i2c_master_enable(i2c_dev *dev, uint32 flags);

After you've initialized, and potentially enabled, your peripheral, it
is now time to begin using it.  The :ref:`libmaple API pages
<libmaple-apis>` are your friends here.

.. rubric:: Footnotes

.. [#fgpio] As an exception, GPIO ports are given letters instead of
            numbers (``GPIOA`` and ``GPIOB`` instead of ``GPIO1`` and
            ``GPIO2``, etc.).
