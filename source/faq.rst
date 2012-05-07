.. highlight:: cpp

.. _faq:

==================================
 Frequently Asked Questions (FAQ)
==================================

.. contents:: Contents
   :local:

.. _faq-atoi:

Can I use ``atoi()``, ``strol()``, etc.?
----------------------------------------

Just ``#include <stdlib.h>``.  See :ref:`arm-gcc-libc` for more
information.

.. _faq-dynamic-memory:

Can I use ``malloc()``/``new``?
-------------------------------

For ``malloc()``, just ``#include <stdlib.h>``, and everything should
work fine.  Be careful, though!  This isn't like C programming on a
PC.  You're on the bare metal, and probably shouldn't be using dynamic
memory unless you know what you're doing.

``new`` should work out of the box (the warning about knowing what
you're doing applies here as well).  If you find that ``new`` (or
``new[]``, ``delete``, etc.) is broken in some way, that's a bug;
please let us know in the `forum`_.

Some information on the heap: on boards with an external SRAM chip
(like Maple Native), the heap is located on external SRAM by default.
For other boards, the heap is located immediately after ``.bss``, and
grows towards the stack.  (In all cases, statically allocated
variables and the stack are located on internal SRAM, for performance
reasons).

.. _faq-flash-tables:

How do I replace ``PROGMEM``/put data into Flash?
-------------------------------------------------

See :ref:`this note <arm-gcc-attribute-flash>`.

How do I write to a pin at high speed?
--------------------------------------

Sometimes, :ref:`lang-digitalwrite` just isn't fast enough.  If that's
your situation, you should first try using fast GPIO writes using the
low-level :ref:`libmaple-gpio` interface.  This FAQ entry explains
how.

You'll need to look up the :ref:`GPIO port and bit <gpio-ports>` which
correspond to the pin you want to write to.  If you don't know what
that means, don't worry.  We'll go through an example here.

Let's say you want to write to pin 4 on the Maple.  In order to find
out the port and bit number, take look at the Maple's :ref:`master pin
map <maple-pin-map-master>` next to "D4".  You'll see that in the
"GPIO" column, there's "PB5".  That's short for "**P**\ ort **B**, bit
**5**".  So the GPIO port is "B", and the bit is "5".  (If you're not
on the Maple, you can find your board's pin map :ref:`from here
<gpio-pin-maps>`).

That's all you need to know.  Now you can use the function
``gpio_write_bit()`` to quickly write to the pin.  The way you call it
is by writing ``gpio_write_bit(GPIO<port>, <bit>, HIGH/LOW)``, where
``<port>`` is the GPIO port, ``<bit>`` is the bit, and ``HIGH`` or
``LOW`` is the level you want to write to the pin.  Here's an example
program which writes pin 4 (GPIOB, bit 5) ``HIGH`` and then ``LOW``
several times in a row each time it :ref:`lang-loop`\ s::

    /*
       Fast pin writing example, for Maple.

       This example works for pin 4 (PB5 on Maple).  If you want to
       use another pin (or are on another board), just change PIN,
       PIN_PORT, and PIN_BIT as described above.
    */

    #define PIN 4
    #define PIN_PORT GPIOB
    #define PIN_BIT 5

    void setup() {
        pinMode(PIN, OUTPUT);
    }

    void loop() {
        gpio_write_bit(PIN_PORT, PIN_BIT, HIGH);
        gpio_write_bit(PIN_PORT, PIN_BIT, LOW);
        gpio_write_bit(PIN_PORT, PIN_BIT, HIGH);
        gpio_write_bit(PIN_PORT, PIN_BIT, LOW);
    }

Now, if you've already tried this and you still can't get enough
speed, there are some threads on the `forum`_ which might help you
squeeze a little extra out of your board.  First, a `general summary
<http://forums.leaflabs.com/topic.php?id=860>`_ of other things to
try, with measurements of the speed you'll get.  Next, a thread
featuring a `detailed discussion on pin capability
<http://forums.leaflabs.com/topic.php?id=774>`_, with a focus on
writes.  And finally, `another thread
<http://forums.leaflabs.com/topic.php?id=895>`_ on the subject which
summarizes a variety of other threads on doing I/O quickly.

Can I use Maple without Maple IDE?
----------------------------------

Yes. See :ref:`unix-toolchain` for the details.

