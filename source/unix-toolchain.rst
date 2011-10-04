.. highlight:: sh

.. _unix-toolchain:

===========================
 Unix Toolchain Quickstart
===========================

This is a tutorial for using a standard Unix toolchain (``make``,
``gcc``, etc.) with Maple.  It's intended for C and C++ programmers
who want to use :ref:`libmaple` directly. If you're just beginning, we
recommend installing :ref:`Maple IDE <maple-ide-install>` instead.

If you have success on an operating system not covered here, please
post in the `forum`_ (or email us at info@leaflabs.com), so we can
update this document.

.. contents:: Contents
   :local:

Requirements
------------

You need a Maple board, a Mini-B USB cable, and root (or
Administrator) access to your computer. We assume you've had success
with the IDE on your machine (this is important on Windows, as this
document doesn't cover :ref:`driver installation
<maple-ide-install-windows-drivers>`).

On Linux and OS X, some previous experience with editing your shell
startup script (.bashrc, .tcshrc, etc.) and using `GCC
<http://gcc.gnu.org/>`_ and `make
<http://www.gnu.org/software/make/>`_ is recommended. (The Windows
instructions are more detailed, since we assume most Windows users
will be new to the Unix shell).

Setup
-----

.. _toolchain-linux-setup:

Linux
^^^^^

**1. Collect and Install Tools**

First, you'll need some tools.

On Debian-based distributions (including Ubuntu)::

  $ sudo aptitude install build-essential git-core wget screen dfu-util \
                          openocd python python-serial

On Red Hat-based distributions (including Fedora)::

  $ yum install screen wget git python pyserial dfu-util openocd make

On other distributions, you'll need to figure this out for yourself
(let us know if you do!).

The following are **mandatory**:

* `Git <http://git-scm.com/>`_ is a distributed version control
  system. We use it to track our source code.

* `dfu-util <http://wiki.openmoko.org/wiki/Dfu-util>`_ is a tool from
  the `OpenMoko`_ project. It is used to upload programs to the Maple
  over USB.

* `make <http://www.gnu.org/software/make/>`_ is used to direct
  compilation.

* `Python <http://python.org>`_ is a programming language. Our reset
  script, which sends control signals to the board which cause it to
  to reset and enter the :ref:`bootloader <bootloader>`, is written in
  Python. (Most Linux distributions these days include Python by
  default).

* `PySerial`_ is a Python library for interacting with serial port
  devices. It's needed by our reset script. PySerial can also be
  installed with `easy_install
  <http://peak.telecommunity.com/DevCenter/EasyInstall>`_.

The following are **optional**:

* `wget <http://www.gnu.org/s/wget/>`_ is a tool for downloading files
  from the command line. You could also pull in the required downloads
  using a web browser.

* `screen <http://www.gnu.org/s/screen/>`_ is a screen manager we use
  to connect to serial port devices.  Some popular alternatives are
  Minicom and Kermit.

* `openocd <http://openocd.sourceforge.net/web/>`_ is a `JTAG
  <http://en.wikipedia.org/wiki/Joint_Test_Action_Group>`_ control
  program. It is used with an ARM JTAG device to do in-circuit
  debugging (uploading new code, connecting to `GDB
  <http://www.gnu.org/s/gdb/>`_, etc.).

.. _OpenMoko: http://openmoko.com/

**2. Fetch libmaple and Compiler Toolchain** ::

  $ cd ~
  $ git clone git://github.com/leaflabs/libmaple.git libmaple
  $ cd libmaple
  $ wget http://static.leaflabs.com/pub/codesourcery/gcc-arm-none-eabi-latest-linux32.tar.gz
  $ tar xvzf gcc-arm-none-eabi-latest-linux32.tar.gz
  $ export PATH=$PATH:~/libmaple/arm/bin # or wherever these tools ended up

In this step, you make a Git clone of the `libmaple repository
<https://github.com/leaflabs/libmaple>`_, then download and extract
the ARM compiler toolchain.

The directory :file:`arm/bin/` will need to be added to your ``PATH``;
you can check that this worked by entering ``arm-none-`` and hitting
tab to auto-complete (your shell should show a bunch of results).
Regardless of where you put the toolchain, make sure to preserve its
internal directory layout.

After you're done, you'll probably want to update your shell startup
script so :file:`~/libmaple/arm/bin` stays in your ``PATH``.

.. _toolchain-udev:

**3. Install udev Rules**

From the libmaple directory, copy our udev rules to ``/etc/udev/rules.d``::

  $ sudo cp support/scripts/45-maple.rules /etc/udev/rules.d/45-maple.rules

On Debian, run ``$ groups``. Make sure the output includes "plugdev".
If not, add yourself to that group. Then run ::

  $ sudo restart udev

On Red Hat, run ::

 $ udevadm control --reload-rules

As a security precaution on Linux, unknown USB devices can only be
accessed by root. This udev script identifies the Maple based on its
vendor and product IDs, mounts it to :file:`/dev/maple`, and (on
Debian-based distros) grants read/write permissions to the ``plugdev``
group. After restarting ``udev`` you'll need to fully unplug or power
cycle any Maples connected to the computer.

**So far, so good?**

Great! Test your setup by :ref:`compiling a sample program
<toolchain-test>`.

.. _toolchain-osx-setup:

OS X
^^^^

These instructions have been tested successfully on OS X 10.6.4.

**1. Collect and Install Tools**

You will need the following tools\ [#fpackman]_ to get started:

* `XCode <http://developer.apple.com/technologies/xcode.html>`_: If
  you're reading this, you've probably already got this. Provides
  compilers and other basic tools of the trade.  While XCode was once
  free of charge, Apple has since begun charging for it; if you'd
  rather not pay, you can probably get by with just a `make
  <http://www.gnu.org/software/make/>`_ binary.

* `Git <http://git-scm.com/>`_: All of our code is tracked by a
  distributed versioning system called Git. A `Mac installer
  <http://code.google.com/p/git-osx-installer/downloads/list?can=3>`_
  is available.

* `dfu-util <http://wiki.openmoko.org/wiki/Dfu-util>`_: A tool from
  `OpenMoko`_ that we use to upload programs to the Maple over USB.

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
  untar the `latest version <http://pypi.python.org/pypi/pyserial>`_,
  then install with ::

      $ cd /path/to/pyserial-x.y
      $ python setup.py build
      $ sudo python setup.py install

  PySerial is also available via ``easy_install``, so if you're
  comfortable using that, you could alternatively install it with ::

      $ easy_install pyserial

**2. Fetch libmaple and Compiler Toolchain**

You first need to clone libmaple::

  $ cd ~
  $ git clone git://github.com/leaflabs/libmaple.git

Next, `download the cross-compilers
<http://static.leaflabs.com/pub/codesourcery/gcc-arm-none-eabi-latest-osx32.tar.gz>`_
you'll use to build libmaple and your own programs. (These are just
special-purpose versions of GCC). Let's say you saved these as

  :file:`~/Downloads/gcc-blah-blah-osx32.tar.gz`

You can unpack the archive and let the shell know where everything
lives with ::

  $ cd ~/Downloads
  $ tar -xvzf gcc-blah-blah-osx32.tar.gz
  $ mv arm ~/libmaple/arm
  $ export PATH=$PATH:~/libmaple/arm/bin

After that's done, you'll probably want to update your shell startup
script so :file:`~/libmaple/arm/bin` stays in your ``PATH``.

**So far, so good?**

Great! Test your setup by :ref:`compiling a sample program
<toolchain-test>`.

.. _toolchain-win-setup:

Windows
^^^^^^^

These instructions have been tested successfully on Windows XP SP3.

1. First, you'll need Git, a distributed versioning system we use to
track our source code. Follow the steps in `this great guide from
GitHub <http://help.github.com/win-set-up-git/>`_.

2. `Install Python <http://python.org/download>`_.  Choose the latest
**2.7.x version**; Python 3 will not work.

3. `Install PySerial <http://pypi.python.org/pypi/pyserial>`_.  Choose
the latest **pyserial-x.y-win32.exe version**; the "py3k" version will
not work.

4. Run Git Bash, and get :ref:`libmaple` by typing the following line
and hitting return. (Do not type the "$".  We put these in to remind
you that lines like this are for the Git Bash prompt). ::

    $ git clone git://github.com/leaflabs/libmaple.git

.. note:: Keep the Git Bash window open as you go.

You now have the libmaple repository in the folder ``Documents and
Settings\<Your Name>``.

5. Download this `archive of the CodeSourcery compiler toolchain
<http://static.leaflabs.com/pub/codesourcery/gcc-arm-none-eabi-latest-win32.tar.gz>`_.
When the download finishes, move the file into the libmaple directory.

6. Type these two lines into the Git Bash prompt to go to the libmaple
folder and extract the archive::

    $ cd libmaple
    $ tar xzf gcc-arm-none-eabi-latest-win32.tar.gz

This will create a folder named "arm" inside the libmaple folder.

7. Now you'll configure your system to use these tools. Type the
following lines into the Git Bash prompt.

.. warning:: If you've installed Bash on your computer before starting
   this guide, and have a ~/.bashrc already, these instructions will
   overwrite it. If that is the case, we assume you know what you're
   doing, and can modify the shell commands in this step appropriately
   for your system.

   If you're using Bash for the first time, don't worry about this
   warning.

::

    $ cat >~/.bashrc <<EOF
    > export PATH=\$PATH:~/libmaple/arm/bin/
    > EOF

.. note:: The "> " at the beginning of the second and third lines will
   appear automatically.

In case that's hard to read, the part of the first line between
``cat`` and ``bashrc`` is these five characters: space ( ), right
angle bracket (>), tilde (~), forward slash (/), and period (.).

For reference, here's a screenshot of what your Git Bash window should
look like at this point (the output after the ``git clone`` line will
be slightly different):

.. _toolchain-git-bash-screenshot:

.. figure:: /_static/img/winxp-git-bash-screenshot.png
   :align: center
   :alt: Git Bash screenshot

8. Let's check that you completed the previous step correctly.  If you
did, there should be a file called ".bashrc" (the period is supposed
to be there) in the folder ``Documents and Settings\<Your Name>\``.
Open this file in Notepad by right clicking on it and selecting "Open
With...", like so:

.. figure:: /_static/img/winxp-open-bashrc-with.png
   :align: center
   :alt: Open .bashrc With

Choose "Notepad" from the resulting pop-up window, and click "OK".
The Notepad window should look like this:

.. figure:: /_static/img/winxp-bashrc-notepad.png
   :align: center
   :alt: .bashrc in Notepad

The little box at the end of the line is supposed to be there. Close
the Notepad window (do not save any changes you may have made by
accident).

9. TODO download dfu-util.exe and put it in ``libmaple\arm\bin``.

**So far, so good?**

Great! Go on to the next section, where you'll compile a program.

.. _toolchain-test:

Test compilation
----------------

Get back into the libmaple directory (this tutorial assumes you put it
in :file:`~/libmaple`) and test that you've installed all the
compilation tools correctly (Windows users: use ``cs-make`` instead of
``make``)::

  $ cd ~/libmaple
  $ cp main.cpp.example main.cpp
  $ make clean
  $ make

.. note:: These instructions are for the Maple.  If you're compiling
   for another board, you'll need to set a ``BOARD`` environment
   variable appropriately.  For example, to compile for Maple Mini (in
   Bash), ::

       $ export BOARD=maple_mini
       $ make

   The ``BOARD`` for Maple RET6 edition is ``maple_RET6``.  You can
   also use ::

       $ BOARD=maple_mini make

   This will only set the environment variable for the duration of
   that single compile.

If it all works out, you should end up seeing something like this::

  find build -iname *.o | xargs arm-none-eabi-size -t
     text    data     bss     dec     hex filename
      482       4      24     510     1fe build/wirish/comm/HardwareSerial.o
      260       0       0     260     104 build/wirish/comm/HardwareSPI.o
       60       0       0      60      3c build/wirish/wirish.o

  [...]

     2196       0       1    2197     895 build/libmaple/usb/usb_lib/usb_core.o
     1904       0       0    1904     770 build/libmaple/usb/usb_lib/usb_regs.o
       56       0       0      56      38 build/libmaple/usb/usb_lib/usb_init.o
      344       0       0     344     158 build/libmaple/usb/usb_hardware.o
     6637       0      58    6695    1a27 build/main.o
    21499     201     391   22091    564b (TOTALS)

  Final Size:
  arm-none-eabi-size build/maple.out
     text    data     bss     dec     hex filename
    21824     200     552   22576    5830 build/maple.out
  Flash build

The ``dec`` field at the end gives the total program size in
bytes. The long listing of object files above the ``Final Size`` helps
to identify bloated code.  As you write larger projects, you may find
that they use too much space. If that happens, the file-by-file
listing will help you track down the culprits.

.. _toolchain-upload:

Upload a program
----------------

Let's blow away the little example program and upload the interactive
test session to your Maple.  This will let you interact with the Maple
over a :ref:`USB serial port <usb>`. If you're on Linux, then before
executing ``make install``, you'll want to have the udev rules setup
:ref:`as described above <toolchain-udev>`.

Plug in your Maple using the Mini-B USB cable; then run ::

  $ cd ~/libmaple
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

Now let's try out the interactive test session.  The serial port
device file should look something like :file:`/dev/ttyACMXXX` on Linux
or :file:`/dev/tty.usbmodemXXX` on OS X, but ``XXX`` will vary
depending on your system.  Try using one of these to find out which it
is::

  # Linux
  $ ls /dev/ttyACM*

  # OS X
  $ ls /dev/tty.usbmodem*

To open up a session, run ::

  $ screen /dev/ttyXXX

If the interactive test program built and uploaded correctly,
``screen`` won't report any errors, and will present you an empty
terminal.  Your board is now waiting for you to send it a command.
Type ``h`` to print a list of commands which demonstrate various
features; type any command's letter to run it.

To exit the screen session, type :kbd:`C-a C-\\` (control-a, followed
by control-backslash) on Mac, or :kbd:`C-a k` (control-a k) on Linux,
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

At a minimum, your include path should contain the directories
:file:`~/libmaple/libmaple` and :file:`~/libmaple/wirish/`.  If you
want to use one of the officially supported :ref:`libraries
<libraries>`, those live under :file:`~/libmaple/libraries/`.  The
main include file for the Wirish library is
:file:`~/libmaple/wirish/wirish.h`.

Get updates
-----------

We update libmaple fairly frequently with bugfixes and other
improvements.  In order get access to these in your local copy of
the repository, you should periodically update it with::

  $ cd ~/libmaple
  $ git pull

We keep releases of libmaple and the Maple IDE in lockstep, so any
IDE updates will have corresponding library updates.  Our `blog
<http://leaflabs.com/blog/>`_ is the place to watch for major
releases; an `RSS feed <http://leaflabs.com/blog/feed/>`_ is
available.

You can sign up for a free `GitHub <https://github.com/plans>`_
account and `watch libmaple
<https://github.com/leaflabs/libmaple/watchers>`_ to receive
notifications about bleeding-edge development.

.. _toolchain-openocd:

Debug with OpenOCD
------------------

TODO. For now see `this great guide
<http://fun-tech.se/stm32/OpenOCD/index.php>`_ from fun-tech.se, and
the ``jtag`` Makefile target.  There is also a `JTAG How-To
<http://wiki.leaflabs.com/index.php?title=Maple_JTAG_How_To>`_ page on
our `wiki <http://wiki.leaflabs.com>`_ which you may find useful.

.. _toolchain-exuberantly:

Go forth exuberantly!
---------------------

Let us know what you come up with! Mention `@leaflabs on Twitter
<http://twitter.com/#!/leaflabs>`_, post in the `forum`_, join the the
#leafblowers IRC channel on `freenode
<http://freenode.net/irc_servers.shtml>`_, whatever. We love projects!

.. _PySerial: http://pyserial.sourceforge.net/

.. rubric:: Footnotes

.. [#fpackman] Some of these software packages might be available on
   `MacPorts <http://www.macports.org/>`_ or `Homebrew
   <http://mxcl.github.com/homebrew/>`_. The author had some bad
   experiences with MacPorts a few years ago, though, and hasn't
   touched a package manager on OS X since. Of course, your mileage
   may vary.
