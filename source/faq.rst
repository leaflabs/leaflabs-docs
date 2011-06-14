.. _faq:

==================================
 Frequently Asked Questions (FAQ)
==================================

.. contents:: Contents
   :local:

.. _faq-atoi:

How can I use ``atoi()``?
-------------------------

The :ref:`CodeSourcery GCC compiler <arm-gcc>` used to compile your
programs is configured to link against the `newlib
<http://sourceware.org/newlib/>`_ C library, and allows the use of any
of its headers.

.. _faq-dynamic-memory:

Why don't ``malloc()``/``new`` work?
------------------------------------

Due to our newlib configuration, dynamic memory allocation is
currently not available.

.. _faq-flash-tables:

How do I replace ``PROGMEM``/put data into Flash?
-------------------------------------------------

See :ref:`this note <arm-gcc-attribute-flash>`.
