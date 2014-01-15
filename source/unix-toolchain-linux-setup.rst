.. highlight:: sh

.. _unix-toolchain-linux-setup:

Unix Toolchain Linux Setup
==========================

This page contains instructions for setting up a Linux computer for
use with the :ref:`Unix toolchain <unix-toolchain>`. (Setup
instructions for :ref:`other operating systems <toolchain-setup>` are
also available.)

These instructions have been tested successfully on:

- Ubuntu 10.04 and 12.04 (32- and 64-bit)
- Fedora 17 (64-bit)
- Debian Wheezy 64-bit

Generic instructions for other distributions are also provided. Please
`contact`_ us with any updates for distros not already covered!

.. contents:: Contents
   :local:

Collect and Install Tools
-------------------------

First, you'll need some tools.

.. warning:: Due to firmware bugs in our :ref:`bootloader
   <bootloader>`, you must use recent versions of ``dfu-util``, or
   uploads will not work.  ``dfu-util`` versions 0.6 and greater
   should work.

**Debian-based distributions (Debian, Ubuntu, Mint, etc.)**:

  Install mandatory and optional tools with ::

    $ sudo apt-get install build-essential git-core screen dfu-util python python-serial

  On *64-bit distros only*, you will also need to install some 32-bit
  libraries needed by the LeafLabs-supported :ref:`ARM GCC toolchain
  <arm-gcc>` with ::

    # 64-bit systems only!
    $ sudo apt-get install ia32-libs

    # As of Ubuntu 13, you should do this instead:
    $ sudo apt-get install lib32z1 lib32ncurses5 lib32bz2-1.0

  You may also need to remove `brltty <http://mielke.cc/brltty/>`_
  with ::

    # Optional
    $ sudo apt-get remove brltty

  Brltty provides braille access to the console.  It has been reported
  to cause conflicts with Maple.

**Red Hat-based distributions (RHEL, Fedora, Centos, etc.)**:

  Install mandatory and optional tools with ::

    $ sudo yum install screen git python pyserial dfu-util make

  On *64-bit distros only*, you will also need to install 32-bit
  libraries needed by the LeafLabs-supported :ref:`ARM GCC toolchain
  <arm-gcc>` with ::

    # 64-bit systems only!
    $ sudo yum install glibc.i686

  You may also need to remove `brltty <http://mielke.cc/brltty/>`_
  with one of these::

    # Optional, 64-bit systems:
    $ sudo yum erase brltty.x86_64

    # Optional, 32-bit systems:
    $ sudo yum erase brltty.i686

  Brltty provides braille access to the console.  It has been
  reported to cause conflicts with Maple.

**Other Linux distributions**:

  On other distributions, you'll need to figure this out for yourself
  (please `contact`_ us if you have instructions for distros not
  covered here!).

  Mandatory tools:

  * `Git`_ is a distributed version control system. We use it to track
    our source code.

  * `dfu-util`_ is a tool from the `OpenMoko`_ project. It is used to
    upload programs to the Maple over USB.

  * `Make <http://www.gnu.org/software/make/>`_ is used to direct
    compilation.

  * `Python`_ is a programming language. Our reset script, which sends
    control signals to the board which cause it to to reset and enter
    the :ref:`bootloader <bootloader>`, is written in Python (and
    works with Python 2 or 3). Most Linux distributions these days
    include Python by default.

  * `PySerial`_ is a Python library for interacting with serial port
    devices. It's needed by our reset script. PySerial can also be
    installed with `easy_install`_.

  Optional tools:

  * `screen <http://www.gnu.org/s/screen/>`_ is a screen manager used
    here to connect to serial port devices.  (Some popular
    alternatives are `Minicom
    <http://alioth.debian.org/projects/minicom/>`_ and `Kermit
    <http://www.kermitproject.org/>`_).

Fetch ``libmaple`` and Compiler Toolchain
-----------------------------------------

First, make a Git clone of :ref:`libmaple`::

  $ cd ~
  $ git clone git://github.com/leaflabs/libmaple.git libmaple

Next, download the `Linux ARM GCC toolchain
<http://static.leaflabs.com/pub/codesourcery/gcc-arm-none-eabi-latest-linux32.tar.gz>`_
you'll use to build your programs. Extract the archive into a
directory named :file:`arm`. Put the resulting :file:`arm/bin`
subdirectory somewhere in your ``PATH``. For example, if you have
`wget <http://www.gnu.org/software/wget/>`_ installed, you can run::

  $ cd ~/libmaple
  $ wget http://static.leaflabs.com/pub/codesourcery/gcc-arm-none-eabi-latest-linux32.tar.gz
  $ tar xvf gcc-arm-none-eabi-latest-linux32.tar.gz
  $ export PATH=$PATH:~/libmaple/arm/bin

You can check that this worked by entering ``arm-none-`` and hitting
tab to auto-complete; your shell should show a bunch of results. After
you're done, you'll probably want to update your shell startup script
so the :file:`arm/bin` directory stays in your ``PATH``.

.. _toolchain-udev:

Install udev Rules
------------------

From the libmaple directory, copy our udev rules [#fudev]_ to
``/etc/udev/rules.d``::

  $ sudo cp support/scripts/45-maple.rules /etc/udev/rules.d/45-maple.rules

Then restart udev.

**Ubuntu (NOT Debian)**:

  Make sure you are in the plugdev group (e.g. by running ``$ groups``
  and seeing if the output includes "plugdev").  If not, add yourself
  to plugdev with ::

    $ sudo usermod -a -G plugdev $USER

  then log out and log back in.

  After that's done, restart udev::

    $ sudo restart udev

**Debian (NOT Ubuntu)**:

  Make sure you're in the dialout group. If not, add yourself with ::

    $ sudo usermod -a -G dialout $USER

  then log out and log back in.

  After that's done, restart udev::

    $ sudo /etc/init.d/udev restart

**Red Hat-based distros**:

  ::

    $ udevadm control --reload-rules

After restarting ``udev``, you'll need to unplug and re-plug your
Maple.

So far, so good?
----------------

Great! Move on by :ref:`compiling a sample program <toolchain-test>`.

.. rubric:: Footnotes

.. [#fudev] As a security precaution on Linux, unknown USB devices can
   only be accessed by root. This udev script identifies the Maple
   based on its vendor and product IDs, mounts it to
   :file:`/dev/maple`, and (for Debian-based distros) grants
   read/write permissions to the ``plugdev`` group.
