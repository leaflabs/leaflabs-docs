.. highlight:: sh

.. _libmaple:

``libmaple``
============

LeafLabs' libmaple is the open source library we have developed for
programming the `STM32 <http://www.st.com/stonline>`_ line of
microcontrollers.  Libmaple's `source is on GitHub
<https://github.com/leaflabs/libmaple>`_; :ref:`patches are welcome
<libmaple-contributing>`.

.. _libmaple-vs-wirish:

Libmaple is split into two pieces: 

- A low-level layer, written in C, called *libmaple proper*, located
  in the `libmaple/
  <https://github.com/leaflabs/libmaple/tree/master/libmaple>`_
  subdirectory of the source repository.

- A high-level layer, written in C++, called *wirish*, in the `wirish/
  <https://github.com/leaflabs/libmaple/tree/master/wirish>`_
  subdirectory.

Wirish is :ref:`largely compatible <arduino-compatibility>` with the
AVR libraries written for the `Arduino <http://arduino.cc>`_ and
`Wiring <http://wiring.org.co/>`_ development boards. The Wirish
:ref:`language` page is a good summary of what Wirish provides; a
:ref:`complete Wirish API index <language-index>` is also
available. :ref:`Wirish libraries <libraries>` are documented
separately.

libmaple is bundled with the :ref:`Maple IDE <ide>`.  However, we
develop it separately, and :ref:`release it standalone
<unix-toolchain>` for users who might chafe at the "sketch"
programming model of the IDE. The following pages document libmaple
proper. As such, they're intended for advanced users who know how to
write C.

.. toctree::
   :maxdepth: 1

   libmaple/overview
   libmaple/apis
   libmaple/contributing
   libmaple/coding-standard
