.. highlight:: c
.. _libmaple-delay:

``<libmaple/delay.h>``
======================

Provides a simple busy-loop delay function. Note that this function
does not account for time spent in interrupts, so actual delay times
may vary depending on your application.

.. doxygenfunction:: delay_us
