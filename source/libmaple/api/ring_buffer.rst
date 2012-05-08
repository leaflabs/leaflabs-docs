.. highlight:: c
.. _libmaple-ring_buffer:

``<libmaple/ring_buffer.h>``
============================

Simple circular byte buffer.  This implementation is not thread-safe.
In particular, none of these functions is guaranteed to be re-entrant.

Ring Buffer Type
----------------

.. doxygenstruct:: ring_buffer

Ring Buffer Operations
----------------------

.. doxygenfunction:: rb_init
.. doxygenfunction:: rb_full_count
.. doxygenfunction:: rb_is_full
.. doxygenfunction:: rb_is_empty
.. doxygenfunction:: rb_insert
.. doxygenfunction:: rb_remove
.. doxygenfunction:: rb_safe_remove
.. doxygenfunction:: rb_safe_insert
.. doxygenfunction:: rb_push_insert
.. doxygenfunction:: rb_reset
