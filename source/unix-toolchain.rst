.. highlight:: sh

.. _unix-toolchain:

===========================
 Unix Toolchain Quickstart
===========================

This is a tutorial for using a standard Unix toolchain (``make``,
``gcc``, etc.) with Maple.  It's intended for C and C++ programmers
who want to use :ref:`libmaple` directly. If you're just beginning, we
recommend installing :ref:`Maple IDE <maple-ide-install>` instead.

.. contents:: Contents
   :local:

Requirements
------------

We assume you've had success with the :ref:`Maple IDE <ide>` (this is
important on Windows, as this document doesn't cover :ref:`driver
installation <maple-ide-install-windows-drivers>`).

At a minimum, you need:

* Maple board
* Mini-B USB cable
* root (or Administrator) access to your computer.

On Linux and OS X, you need to know how to use `bash
<http://www.gnu.org/software/bash/>`_, and how to edit your .bashrc.
Some experience using `GCC <http://gcc.gnu.org/>`_ and `make
<http://www.gnu.org/software/make/>`_ is recommended, but is not
required.

.. _toolchain-linux-setup:
.. _toolchain-osx-setup:
.. _toolchain-win-setup:
.. _toolchain-setup:

Setup
-----

You first need to set up your computer by installing and configuring
various things. Don't fret! We've got detailed instructions, just for
you.

* :ref:`Linux <unix-toolchain-linux-setup>`
* :ref:`OS X <unix-toolchain-osx-setup>`
* :ref:`Windows <unix-toolchain-win-setup>`

Come back when you're ready. We'll wait.

.. _toolchain-test:

Test compilation
----------------

Test that you've installed all the compilation tools correctly by
running the following commands in your shell.

Windows users:

  - Don't type the ``$``'s, just the parts that come after.
  - First get to libmaple by opening a Git Shell, then running ``cd libmaple``.
  - **Always type** ``cs-make`` **instead of** ``make``.

Linux and OS X users:

  - Run these from the top-level libmaple directory.

::

  $ cp main.cpp.example main.cpp
  $ make clean
  $ make

If all goes well, you should see a bunch of output, then something
like this::

  Final Size:
     text          data     bss     dec     hex filename
    13164          1704     552   15420    3c3c build/maple.elf

Hurray! You've just compiled your first program for Maple.

**Important: if you're not using Maple (Maple Mini, etc.), make sure
to read the following note before moving on**.

You can now move on to :ref:`uploading a program <toolchain-upload>`,
or take a quick detour to learn :ref:`more about the build output
<toolchain-build-info>`.

.. _toolchain-setting-board:

.. note:: This tutorial assumes you're using a Maple.  If you're
   compiling for another board, you'll need to set a ``BOARD``
   environment variable appropriately.

   To get a list of values for ``BOARD``, run ::

     $ make list-boards

   For example, to compile for Maple Mini:

   * On OS X or Linux, run::

      $ export BOARD=maple_mini
      $ make

   * On Windows, set a new environment variable named ``BOARD`` to
     value ``maple_mini``, then open a new Git Shell, and run ``cd
     libmaple`` followed by ``cs-make`` as explained above.

   You can check that this worked by making sure that the final
   program file is named ``build/maple_mini.elf`` instead of
   ``maple.elf``::

     Final Size:
        text       data     bss     dec     hex filename
       16848       2696     704   20248    4f18 build/maple_mini.elf

   Other notes for OS X and Linux:

   - You can also use the following, but you'll need to write the
     ``BOARD=maple_mini`` part every time you call ``make`` (for
     ``make install``, etc.)::

       $ BOARD=maple_mini make

   - To make the board setting permanent, add this line to your
     .bashrc::

       export BOARD=maple_mini

.. warning:: You must start from a clean build after each time you
   change ``BOARD`` (advanced users: or ``MEMORY_TARGET``). For
   example, if you compile a program for Maple, then you want to
   compile another program for Maple Mini, you must run ``$ make
   clean`` **before** you compile the second program. If you do not,
   you will experience strange errors.

.. _toolchain-build-info:

Notes about the ``libmaple`` build
----------------------------------

These are just some miscellaneous notes that are good to know. Feel
free to skip reading this section.

- The ``dec`` field at the end of the build output under ``Final
  Size:`` gives the total program size in bytes.  The ``text``,
  ``data``, and ``bss`` fields respectively break down the size of the
  program into `code <http://en.wikipedia.org/wiki/Code_segment>`_,
  `initialized data <http://en.wikipedia.org/wiki/Data_segment>`_, and
  `zero-valued data <http://en.wikipedia.org/wiki/.bss>`_.

- The long list of object files above the ``Final Size`` shows similar
  information on a per-file basis. You can use it to help slim down
  programs that use too much space.

- ``build/$BOARD.elf`` is the final build result (where ``BOARD`` is
  ``maple``, ``maple_mini``, etc. :ref:`depending on your build
  <toolchain-setting-board>`).

- There are other files under ``build`` you may be interested in, like
  disassembly and map files.

- If you want quicker build times, you should check out our blog post,
  `Making libmaple compile faster
  <http://leaflabs.com/2012/08/2549/>`_.

.. _toolchain-upload:

Upload a program
----------------

Let's blow away the little example program and upload the interactive
test session to your Maple.  This will let you interact with the Maple
over a :ref:`USB serial port <usb>`.

* Linux: you need udev rules set up :ref:`as described in the setup
  doc <toolchain-udev>`.

* Windows: you need to :ref:`install the Maple's device drivers
  <maple-ide-install-windows-drivers>`.

* OS X: everything Just Works for you. Aren't you special?

Plug in your Maple using a Mini-B USB cable, then run ::

  # Window users: as usual, use cs-make instead of make.

  $ cp examples/test-session.cpp main.cpp
  $ make clean
  $ make
  $ make install

A number of things can go wrong at this stage.  Simple debugging steps
include using :ref:`perpetual bootloader mode
<troubleshooting-perpetual-bootloader>`, restarting the Maple a couple
times, ``make clean``, etc. If nothing works, the `forum`_ is your
friend.

.. _toolchain-serialusb:

Communicate over USB-Serial
---------------------------

Now let's try out the interactive test session.  You need to connect
to the board's serial port device file.

* Linux: this looks like :file:`/dev/ttyACM*`.
* OS X: it looks like :file:`/dev/tty.usbmodem*`.
* Windows: it will be :file:`COMx`, where ``x`` is some number.

Try using one of these to find out which it is::

  # Linux
  $ ls /dev/ttyACM*

  # OS X
  $ ls /dev/tty.usbmodem*

  # Windows, works from libmaple directory
  $ python support/scripts/win-list-com-ports.py

To open up a session on Linux or OS X, run ::

  $ screen /dev/ttyXXX

(On Windows, you will need to use a separate program, such as Maple
IDE's serial console or `PuTTY
<http://www.chiark.greenend.org.uk/~sgtatham/putty/>`_.)

``screen`` will present you an empty terminal.  Your board is waiting
for you to send it a command.  Type ``h`` to print a list of commands;
type any command's letter to run it.

.. highlight:: none

Example output (for Maple)::

    > u
    Hello World!
    > b
    Board information
    =================
    * Clock speed (MHz): 72
    * BOARD_LED_PIN: 13
    * BOARD_BUTTON_PIN: 38
    * GPIO information (BOARD_NR_GPIO_PINS = 44):
            ADC pins (15): 0, 1, 2, 3, 10, 11, 12, 15, 16, 17, 18, 19, 20, 27, 28
            PWM pins (15): 0, 1, 2, 3, 5, 6, 7, 8, 9, 11, 12, 14, 24, 27, 28
            Used pins (7): 13, 38, 39, 40, 41, 42, 43``

.. highlight:: sh

To exit the screen session, type :kbd:`C-a k` (control-a k) on Linux,
or :kbd:`C-a C-\\` (Control-a, followed by Control-backslash) on OS X,
and type ``y`` when prompted if you're sure.

.. note::

   Using ``screen`` sometimes messes up your terminal session on OS X.
   If your shell starts acting funny after you exit ``screen``, you
   should be able to fix it with ::

       $ reset && clear

   If that doesn't work, just close the Terminal window and open up a
   new one.

.. _toolchain-projects:

Start your own project
----------------------

So everything worked, and you want to start your own project? Great!
There are two ways to go about it.

If your project is small, all you have to do is replace
:file:`~/libmaple/main.cpp` with your own code, and you're free to use
``make`` and ``make install`` in the same way you did when you first
:ref:`uploaded a program <toolchain-upload>`.

If you have a more complicated project, with its own Makefile and
multiple source files, or if you're using an IDE that creates its own
Makefile, you'll probably want to load libmaple from an archive (a
build-time library, not a DLL).

To create an archive, use the ``library`` Makefile target::

  $ cd ~/libmaple
  $ make library

This will produce a build-time library in the file
:file:`~/libmaple/build/libmaple.a`.  To use it, make sure that you
link against that library, and that the libmaple sources are in your
include path.

There is also a page on `starting a project with the Unix toolchain
<http://wiki.leaflabs.com/index.php?title=Starting_A_Project_%28No_IDE%29>`_
on the `LeafLabs wiki <http://wiki.leaflabs.com>`_ that you may find
useful.

Get updates
-----------

We update libmaple fairly frequently with bugfixes and other
improvements.  In order get access to these in your local copy of the
repository, you should periodically update it with::

  $ cd ~/libmaple
  $ git pull

We do our best to keep the master libmaple branch on GitHub free from
broken or half-finished code, so don't be too scared running the
latest and greatest. If you do, please report any bugs or regressions!

We keep releases of libmaple and the Maple IDE in lockstep, so any IDE
updates will have corresponding library updates.  Our `blog
<http://leaflabs.com/blog/>`_ is the place to watch for major
releases; an `RSS feed <http://leaflabs.com/blog/feed/>`_ is
available.

You can sign up for a free `GitHub <https://github.com/plans>`_
account and `watch libmaple
<https://github.com/leaflabs/libmaple/watchers>`_ to receive
notifications about bleeding-edge development.

.. _toolchain-openocd:

(Optional) Upload/Debug with JTAG/SWD
-------------------------------------

Advanced users will wish to use a JTAG (or SWD) dongle for uploading
and debugging their programs. A big advantage to this approach is that
it lets you use `GDB <http://www.gnu.org/software/gdb/>`_ to
single-step through your code, inspect variables, etc.

You can build your projects for JTAG or SWD upload with the ``jtag``
Makefile target. That is, instead of compiling with ``make``, compile
with ::

  # (This is equivalent to $ MEMORY_TARGET=jtag make)
  $ make jtag

Then use your favorite JTAG/SWD dongle and driver software to upload
the resulting program. An `ELF
<http://en.wikipedia.org/wiki/Executable_and_Linkable_Format>`_
suitable for upload is in :file:`build/$BOARD.elf`; the raw binary you
can copy directly to address 0x0 is :file:`build/$BOARD.bin`.

.. warning:: Uploading code built with the ``jtag`` target will
   overwrite the :ref:`bootloader <bootloader>`. This is a good thing
   -- since you're using another upload method, this lets you use the
   Flash and RAM the bootloader ordinarily reserves for itself. You
   can always :ref:`reflash the bootloader <bootloader-reflashing>`
   later.

While LeafLabs doesn't officially support any particular way of using
JTAG with Maple, there is a `JTAG How-To
<http://wiki.leaflabs.com/index.php?title=Maple_JTAG_How_To>`_ on the
`LeafLabs wiki <http://wiki.leaflabs.com>`_ that you may find useful.

.. _toolchain-exuberantly:

Go forth exuberantly!
---------------------

Let us know what you come up with! Mention `@leaflabs on Twitter
<http://twitter.com/#!/leaflabs>`_, post in the `forum`_, join the the
#leafblowers IRC channel on `freenode
<http://freenode.net/irc_servers.shtml>`_, whatever. We love projects!
