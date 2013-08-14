.. highlight:: sh

.. _unix-toolchain-osx-setup:

Unix Toolchain OS X Setup
=========================

This page contains instructions for setting up an OS X computer for
use with the :ref:`Unix toolchain <unix-toolchain>`. (Setup
instructions for :ref:`other operating systems <toolchain-setup>` are
also available.)

These instructions have been tested successfully on OS X 10.6.4 and
10.8.1.

.. contents:: Contents
   :local:

Collect and Install Tools
-------------------------

First, you'll need some tools. [#fpackman]_

* `XCode <https://developer.apple.com/xcode/>`_: Provides compilers
  and other basic tools of the trade.  XCode seems to only be available for
  those with Apple IDs through the Mac App Store. If you'd rather not go
  through that mechanism, you can probably get by with just a `make
  <http://www.gnu.org/software/make/>`_ binary, but you're on your own.

* `Git`_: All of our code is tracked by a distributed versioning
  system called Git. A `Mac installer
  <http://code.google.com/p/git-osx-installer/downloads/list?can=3>`_
  is available.

* `dfu-util`_: A tool from `OpenMoko`_ that we use to upload programs
  to the Maple over USB.

  .. warning:: Due to firmware bugs in our :ref:`bootloader
     <bootloader>`, you must use recent versions of ``dfu-util``, or
     uploads will not work.  ``dfu-util`` versions 0.6 and greater
     should work.

  If you prefer to compile from source, OpenMoko provides instructions
  for `building dfu-util on OS X
  <http://wiki.openmoko.org/wiki/Dfu-util#Mac>`_.

  If you're in a hurry, you can use the dfu-util binary bundled with
  `OpenMoko Flasher
  <http://www.handheld-linux.com/wiki.php?page=OpenMoko%20Flasher>`_. To
  do this, first `download OpenMoko Flasher
  <http://projects.goldelico.com/p/omflasher/downloads/>`_, then move
  it to your :file:`/Applications` folder (or wherever you
  like). Let's say you save it as :file:`/Applications/OpenMoko
  Flasher.app`.  Then the ``dfu-util`` binary resides in

      :file:`/Applications/OpenMoko Flasher.app/Contents/Mac OS/dfu-util`

  To run it from the command line, make a symbolic link to the binary
  from some place on your ``PATH``::

      $ ln -s /Applications/OpenMoko\ Flasher.app/Contents/Mac\ OS/dfu-util \
              /somewhere/on/your/PATH/dfu-util

  .. note::

    Copying the binary won't work, as it relies on dynamically linked
    libraries found elsewhere in the .app bundle.

  To make sure this worked, plug in your Maple, put it into
  :ref:`perpetual bootloader mode
  <troubleshooting-perpetual-bootloader>` (press RESET, then quickly
  press and hold BUT for several seconds), and run ::

      $ dfu-util -l

  The output should look like this::

      Found DFU: [0x1eaf:0x0003] devnum=0, cfg=0, intf=0, alt=0, name="DFU Program RAM 0x20000C00"
      Found DFU: [0x1eaf:0x0003] devnum=0, cfg=0, intf=0, alt=1, name="DFU Program FLASH 0x08005000"

* `PySerial`_: our reset script (which sends control signals over the
  USB-serial connection to restart and enter the bootloader) is
  written in Python, and requires the PySerial library. Download and
  extract the `latest version
  <http://pypi.python.org/pypi/pyserial>`_, then install with ::

      $ cd /path/to/pyserial-x.y
      $ python setup.py build
      $ sudo python setup.py install

  PySerial is also available via `easy_install`_, so if you're
  comfortable using that, you could alternatively install it with ::

      $ easy_install pyserial

Fetch ``libmaple`` and Compiler Toolchain
-----------------------------------------

First, make a `Git`_ clone of :ref:`libmaple`::

  $ cd ~
  $ git clone git://github.com/leaflabs/libmaple.git

Next, `download the cross-compilers
<http://static.leaflabs.com/pub/codesourcery/gcc-arm-none-eabi-latest-osx32.tar.gz>`_
you'll use to build libmaple and your own programs. (These are just
special-purpose versions of :ref:`GCC <arm-gcc>`).

Let's say you saved these into
:file:`~/Downloads/gcc-arm-none-eabi-latest-osx32.tar.gz`. Then unpack
the archive and tell the shell about its contents with::

  $ cd ~/Downloads
  $ tar -xvf gcc-arm-none-eabi-latest-osx32.tar.gz
  $ mv arm ~/libmaple/arm
  $ export PATH=$PATH:~/libmaple/arm/bin

After that's done, update your shell startup script so
:file:`~/libmaple/arm/bin` stays in your ``PATH``.

So far, so good?
----------------

Great! Move on by :ref:`compiling a sample program <toolchain-test>`.

.. rubric:: Footnotes

.. [#fpackman] Some of these software packages might be available on
   `MacPorts <http://www.macports.org/>`_ or `Homebrew
   <http://mxcl.github.com/homebrew/>`_. The author had some bad
   experiences with MacPorts a few years ago, though, and hasn't
   touched a package manager on OS X since. Your mileage may vary.
