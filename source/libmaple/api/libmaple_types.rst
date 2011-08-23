.. highlight:: c
.. _libmaple-libmaple_types:

``libmaple_types.h``
====================

Defines the base types and type-related macros used throughout the
rest of libmaple.

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

.. c:macro:: __io

   This is a macro for ``volatile`` which is used to denote that the
   variable whose type is being qualified is IO-mapped.  Its most
   common use is in the individual members of each :ref:`register map
   <libmaple-overview-regmaps>` struct.

.. c:macro:: __attr_flash

   This is a macro for a GCC ``__attribute__`` which (when using the
   linker scripts provided with libmaple) will cause the variable
   being marked to be stored in Flash, rather than SRAM.  The
   variable's value may be read like that of any other variable, but
   it may not be written.

Other typedefs
--------------

.. doxygentypedef:: voidFuncPtr
