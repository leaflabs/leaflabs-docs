.. highlight:: c
.. _libmaple-util:

``util.h``
==========

.. TODO [0.2.0?] clean this up.

Miscellaneous utility macros and procedures.

.. contents:: Contents
   :local:

Bit Manipulation
----------------

::

    #define BIT(shift)                     (1UL << (shift))
    #define BIT_MASK_SHIFT(mask, shift)    ((mask) << (shift))
    /** Gets bits m to n of x */
    #define GET_BITS(x, m, n) ((((uint32)x) << (31 - (n))) >> ((31 - (n)) + (m)))
    #define IS_POWER_OF_TWO(v)  (v && !(v & (v - 1)))

Failure Routines
----------------

.. doxygenfunction:: throb

Asserts and Debug Levels
------------------------

The level of libmaple's assertion support is determined by
``DEBUG_LEVEL``, as follows:

.. doxygendefine:: DEBUG_LEVEL

The current assert macros are ``ASSERT()`` and ``ASSERT_FAULT()``.
``ASSERT()`` is checked when ``DEBUG_LEVEL >= DEBUG_ALL``.
``ASSERT_FAULT()`` is checked whenever ``DEBUG_LEVEL >= DEBUG_FAULT``.

As explained above, an assert macro is checked when the current
``DEBUG_LEVEL`` is high enough.  If the debug level is too low, the
macro expands  into a no-op that gets compiled away.

If an assertion fails, execution is halted at the point of the failed
assertion.  When libmaple has been configured properly (Wirish
performs this configuration by default), the built-in LED throbs in a
smooth pattern to signal the failed assertion (using
:c:func:`throb()`), and the file and line where the assert failed are
transmitted to the user as detailed in :ref:`lang-assert`.
