.. _stm32:

Introduction to the STM32
=========================

.. FIXME [v0.0.13] Stub.

Stub. To fill in:

.. _stm32-general:

General Information
-------------------

- Description of the history and present state of the STM32 line. ARM
  Cortex-M series etc.

- Introduction and pointers to ARM Cortex-M docs and other good books
  on the subject.

- Pointers to ST reference manuals. Note that the appropriate
  reference manual for each board is always documented in that board's
  hardware page.

ST's Documentation
------------------

- Classes of documentation: product flyer, datasheet, reference
  manual, programming manual, application note.

.. _stm32-registers:

Registers and Register Maps
---------------------------

- General purpose registers vs. peripheral registers.

Perhaps you haven't read it in detail, but maybe you've at least
thumbed through a few of the sections, trying to gain some
understanding of what's going on.  If you've done that (and if you
haven't, just take our word for it), then you know that underneath the
covers, *everything* is controlled by messing with bits in the
seemingly endless collections of registers specific to every
peripheral.  The :ref:`USARTs <usart>` have data registers; (some of
the) the :ref:`timers <timers>` have capture/compare registers, the
:ref:`GPIOs <gpio>` have output data registers, etc.

- Peripheral register maps; how they're duplicated for each peripheral

- Portability concerns across series

.. _stm32-libmaple-support:

``libmaple``\ 's STM32 support
------------------------------

- Descriptions of libmaple's present support for the STM32 line
  (i.e. currently performance-line only; update when the F2 branch is
  ready to merge into master etc.).
