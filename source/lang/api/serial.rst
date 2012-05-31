.. FIXME [0.0.13] This doesn't include UART4/5, or USART6
.. highlight:: cpp

.. _lang-serial:

Serial Ports (``Serial1``, ``Serial2``, ``Serial3``)
====================================================

This page describes how to use the built-in serial ports (also known
as USARTs).  For more information about serial ports, see
:ref:`usart`.

.. contents:: Contents
   :local:

Getting Started
---------------

First, decide which serial port you wish to use, and :ref:`connect its
pins to the device you're communicating with <usart-circuit>`. (The TX
and RX pins for a serial port are labeled on your board's silkscreen;
for example, serial port 2 has pins labeled "TX2" and "RX2").

The variable for controlling a serial port is the word ``Serial``,
plus the serial port's number.  For example, you can control serial
port 1 with the variable ``Serial1``, serial port 2 with ``Serial2``,
and so on.

In order to get started using your serial port, you'll first need to
turn it on.  Do this by calling your serial port's ``begin()``
function, giving it the baud rate you wish it to communicate at.  If
you're not sure what baud rate to use, 9600 is a safe (although slow)
value to try.  Put this call to ``begin()`` in your :ref:`lang-setup`,
like in the following example::

    void setup() {
        // 9600 is the baud rate to use.  The baud rate determines how
        // fast the communication goes.
        Serial2.begin(9600);
    }

    void loop() {
        // Communicate using Serial2 here
    }

Communicating Over Serial
-------------------------

Now that your serial port is set up, it's time to start communicating.

One common use for serial ports is to print strings and other
debugging information to a computer.  You can print numbers or strings
using ``print()`` and ``println()``, like this::

    void printSomeInformation() {
        Serial2.print("First, print this string.  Then print a number: ");
        Serial2.print(42);
        Serial2.print(".  You can print floating point values, too: ");
        Serial2.print(3.14);
        Serial2.println(". Using println() instead of print() ends the line.");
        Serial2.println("This sentence starts on a new line.");
    }

This sort of communication can go both ways: you can send characters
from a computer to a serial port as well.  You can check how many
characters are waiting for you to read using the ``available()``
function, and read them out one at a time using ``read()``.  The
following example program uses these functions to "echo" back anything
sent to ``Serial2``::

    void setup() {
        Serial2.begin(9600);
    }

    void echoCharacter() {
        // Check to see if we have received any information.  numUnread
        // will hold the number of bytes we've received, but haven't
        // looked at yet.
        int numUnread = Serial2.available();

        // numUnread > 0 means that there are some unread bytes waiting
        if (numUnread > 0) {
            // Read a single byte out:
            byte b = Serial2.read();
            // And then print it back:
            Serial2.print(b);
        }
    }

    void loop() {
        echoCharacter();
    }

Function Reference
------------------

This section gives a full listing of functions available for use with
serial ports.

Library Documentation
---------------------

All of the ``Serial[1,2,3]`` objects are instances of the
``HardwareSerial`` class, which is documented in this section.  (This
means that you can use any of these functions on any of ``Serial1``,
``Serial2``, and ``Serial3``).

.. cpp:class:: HardwareSerial

   Serial port class.  Predefined instances are ``Serial1``,
   ``Serial2``, and ``Serial3``.

.. cpp:function:: void HardwareSerial::begin(unsigned int baud)

   Set up a ``HardwareSerial`` object for communications.  This method
   must be called before attempting to use the ``HardwareSerial``
   object (typically, you call this in your :ref:`setup()
   <lang-setup>` function).

.. cpp:function:: void HardwareSerial::end()

   Disables the USART associated with this object, allowing any
   associated communication pins to be used for other purposes.

.. cpp:function:: unsigned int HardwareSerial::available()

   Returns the number of bytes available for reading.

.. cpp:function:: unsigned char HardwareSerial::read()

   Returns the next available, unread character.  If there are no
   available characters (you can check this with :cpp:func:`available
   <HardwareSerial::available>`), the call will block until one
   becomes available.

.. cpp:function:: void HardwareSerial::flush()

   Throw away the contents of the serial port's receiver (RX) buffer.
   That is, clears any buffered characters, so that the next character
   read is guaranteed to be new.

.. cpp:function:: void HardwareSerial::print(unsigned char b)

   Print the given byte over the USART.

.. cpp:function:: void HardwareSerial::print(char c)

   Print the given character over the USART.  7-bit clean characters
   are typically interpreted as ASCII text.

.. cpp:function:: void HardwareSerial::print(const char *str)

   Print the given null-terminated string over the USART.

.. cpp:function:: void HardwareSerial::print(int n)

   Print the argument's digits over the USART, in decimal format.
   Negative values will be prefixed with a ``'-'`` character.

.. cpp:function:: void HardwareSerial::print(unsigned int n)

   Print the argument's digits over the USART, in decimal format.

.. cpp:function:: void HardwareSerial::print(long n)

   Print the argument's digits over the USART, in decimal format.
   Negative values will be prefixed with a ``'-'`` character.

.. cpp:function:: void HardwareSerial::print(unsigned long n)

   Print the argument's digits over the USART, in decimal format.

.. cpp:function:: void HardwareSerial::print(long n, int base)

   Print the digits of ``n`` over the USART, in base ``base`` (which
   may be between 2 and 16).  The ``base`` value 2 corresponds to
   binary, 8 to octal, 10 to decimal, and 16 to hexadecimal.  Negative
   values will be prefixed with a ``'-'`` character.

.. cpp:function:: void HardwareSerial::print(double n)

   Print ``n``, accurate to 2 digits after the decimal point.

.. _lang-serial-println:

.. cpp:function:: void HardwareSerial::println(char c)

   Like ``print(c)``, followed by ``"\r\n"``.

.. cpp:function:: void HardwareSerial::println(const char *c)

   Like ``print(c)``, followed by ``"\r\n"``.

.. cpp:function:: void HardwareSerial::println(unsigned char b)

   Like ``print(b)``, followed by ``"\r\n"``.

.. cpp:function:: void HardwareSerial::println(int n)

   Like ``print(n)``, followed by ``"\r\n"``.

.. cpp:function:: void HardwareSerial::println(unsigned int n)

   Like ``print(n)``, followed by ``"\r\n"``.

.. cpp:function:: void HardwareSerial::println(long n)

   Like ``print(n)``, followed by ``"\r\n"``.

.. cpp:function:: void HardwareSerial::println(unsigned long n)

   Like ``print(n)``, followed by ``"\r\n"``.

.. cpp:function:: void HardwareSerial::println(long n, int base)

   Like ``print(n, b)``, followed by ``"\r\n"``.

.. cpp:function:: void HardwareSerial::println(double n)

   Like ``print(n)``, followed by ``"\r\n"``.

.. cpp:function:: void HardwareSerial::println()

   Prints ``"\r\n"`` over the USART.

.. cpp:function:: void HardwareSerial::write(unsigned char ch)

   Sends one character over the USART.  This function is currently
   blocking.

   This is a low-level function.  One of the ``print()`` or
   ``println()`` functions is likely to be more useful when printing
   multiple characters, when formatting numbers for printing, etc.

.. cpp:function:: void HardwareSerial::write(const char* str)

   Send the given null-terminated character string over the USART.

   This is a low-level function.  One of the ``print()`` or
   ``println()`` functions is likely to be more useful when printing
   multiple characters, when formatting numbers for printing, etc.

.. cpp:function:: void HardwareSerial::write(void *buf, unsigned int size)

   Writes the first ``size`` bytes of ``buf`` over the USART.  Each
   byte is transmitted as an individual character.

   This is a low-level function.  One of the ``print()`` or
   ``println()`` functions is likely to be more useful when printing
   multiple characters, when formatting numbers for printing, etc.

.. cpp:function:: int HardwareSerial::txPin()

   Return the number of the TX (transmit) pin.

.. cpp:function:: int HardwareSerial::rxPin()

   Return the number of the RX (receive) pin.

Arduino Compatibility Note
--------------------------

Unlike the Arduino, none of the Maple's serial ports is connected to
the USB port on the Maple board.  If you want to communicate using the
built-in USB port, use :ref:`SerialUSB <lang-serialusb>` instead.  You
will need an additional USB-to-serial adapter to communicate between a
USART and your computer.

.. FIXME [0.1.0] port these examples over

.. Examples
.. --------

.. -  `ASCII Table <http://arduino.cc/en/Tutorial/ASCIITable>`_
.. -  `Dimmer <http://arduino.cc/en/Tutorial/Dimmer>`_
.. -  `Graph <http://arduino.cc/en/Tutorial/Graph>`_
.. -  `Physical Pixel <http://arduino.cc/en/Tutorial/PhysicalPixel>`_
.. -  `Virtual Color Mixer <http://arduino.cc/en/Tutorial/VirtualColorMixer>`_
.. -  `Serial Call Response <http://arduino.cc/en/Tutorial/SerialCallResponse>`_
.. -  `Serial Call Response ASCII <http://arduino.cc/en/Tutorial/SerialCallResponseASCII>`_

.. include:: /arduino-cc-attribution.txt
