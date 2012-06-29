.. highlight:: c
.. _libmaple-libmaple_types:

``<libmaple/libmaple_types.h>``
===============================

Defines the base types and type-related macros used throughout the
rest of libmaple.

.. contents:: Contents
   :local:

Integral Types
--------------

.. doxygentypedef:: uint8
.. doxygentypedef:: uint16
.. doxygentypedef:: uint32
.. doxygentypedef:: uint64
.. doxygentypedef:: int8
.. doxygentypedef:: int16
.. doxygentypedef:: int32
.. doxygentypedef:: int64

Attributes and Type Qualifiers
------------------------------

In the case of macros for GCC's ``__attribute__``\ s, we have our own
macros mostly to save typing, but also in hopes that they might be
expressible using different compiler extensions, or to give them
different interpretations when running e.g. Doxygen on libmaple.

.. c:macro:: __always_inline

   Macro for ``inline __attribute__((always_inline))``. This can be
   used to defeat GCC's ``-Os`` when you Really Mean Inline.

.. c:macro:: __attr_flash

   Macro for a GCC ``__attribute__`` which (when using libmaple's
   linker scripts) will cause the variable being marked to be stored
   in Flash, rather than SRAM. It's useful for read-only variables
   like look-up tables.

.. c:macro:: __deprecated

   Macro for ``__attribute__((deprecated))``. Its use causes GCC to
   emit deprecation warnings when the deprecated functionality is
   used. It's not used for everything that gets deprecated, so don't
   rely on it to catch all uses of deprecated APIs.

.. c:macro:: __packed

   Macro for ``__attribute__((packed))``.

.. c:macro:: __io

   Macro for ``volatile`` which denotes that the variable whose type
   is being qualified is IO-mapped.  Its most common use is in the
   individual members of each :ref:`register map
   <libmaple-overview-regmaps>` struct.

.. c:macro:: __weak

   Macro for ``__attribute__((weak))``.

.. c:macro:: __unused

   Macro for ``__attribute__((unused))``. This can be used
   (sparingly!) to silence unused function warnings when GCC is
   mistaken.

Miscellaneous
-------------

.. doxygentypedef:: voidFuncPtr

.. c:macro:: offsetof(type, member)

   If left undefined, this is defined to ``__builtin_ofsetof(type,
   member)``.

.. c:macro:: NULL

   If left undefined, this is defined to ``0``.
