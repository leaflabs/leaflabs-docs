.. _stm32:

Introduction to STM32
=====================

.. FIXME [v0.0.13] Stub page.

Every Maple board is powered by an STM32 microcontroller (the chip
which controls all of the pins).  Once you're comfortable using your
Maple, you'll probably start to get curious about what's going on
under the hood.  This page is a good place to begin.  It includes an
overview of the STM32, and helps you make sense of the sometimes
dizzying array of features, libraries, and documentation that are
available to you.

The world of the STM32 is a big one, and it's only getting bigger.
With literally thousands of pages of manuals, datasheets, application
notes, etc. available for every STM32 microcontroller, and a huge
variety of categories and subcategories of STM32s available to choose
from, it's easy to get confused or feel daunted about getting started.
Don't panic!  We've got `your towel
<http://en.wikipedia.org/wiki/Know_where_one%27s_towel_is#Knowing_where_one.27s_towel_is>`_
right here.

.. contents:: Contents
   :local:

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

.. _stm32-series:
.. _stm32-series-f1-lines:

STM32 Series
------------

- Describe families, F1 lines, etc.

- Describe how a product name tells you what you need

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

``libmaple`` STM32 support
--------------------------

- Descriptions of libmaple's present support for the STM32 line
  (i.e. currently performance-line only; update when the F2 branch is
  ready to merge into master etc.).
