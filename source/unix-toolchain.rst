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
   :depth: 2

Requirements
------------

You need a Maple board, a Mini-B USB cable, and root (or
Administrator) access to your computer. We assume you've had success
with the IDE on your machine (this is important on Windows, as this
document doesn't cover :ref:`driver installation
<maple-ide-install-windows-drivers>`).

On Linux and OS X, you need to know how to use a shell and edit your
shell startup script (.bashrc, .tcshrc, etc.). (The Windows
instructions are more detailed, since we assume many Windows users
will be newer to the Unix shell). Some experience using `GCC
<http://gcc.gnu.org/>`_ and `make
<http://www.gnu.org/software/make/>`_ is recommended, but is not
required.

Setup
-----

.. _toolchain-linux-setup:

Linux
^^^^^

1. Collect and Install Tools
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

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

  * `Python <http://python.org>`_ is a programming language. Our reset
    script, which sends control signals to the board which cause it to
    to reset and enter the :ref:`bootloader <bootloader>`, is written
    in Python (and works with Python 2 or 3). Most Linux distributions
    these days include Python by default.

  * `PySerial`_ is a Python library for interacting with serial port
    devices. It's needed by our reset script. PySerial can also be
    installed with `easy_install
    <http://peak.telecommunity.com/DevCenter/EasyInstall>`_.

  Optional tools:

  * `screen <http://www.gnu.org/s/screen/>`_ is a screen manager used
    here to connect to serial port devices.  (Some popular
    alternatives are `Minicom
    <http://alioth.debian.org/projects/minicom/>`_ and `Kermit
    <http://www.kermitproject.org/>`_).

2. Fetch ``libmaple`` and Compiler Toolchain
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

First, make a Git clone of :ref:`libmaple`::

  $ cd ~
  $ git clone git://github.com/leaflabs/libmaple.git libmaple

Next, download the `Linux ARM GCC toolchain
<http://static.leaflabs.com/pub/codesourcery/gcc-arm-none-eabi-latest-linux32.tar.gz>`_
you'll use to build your programs. Extract the archive into a
directory named :file:`arm`. Put resulting :file:`arm/bin`
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

3. Install udev Rules
~~~~~~~~~~~~~~~~~~~~~

From the libmaple directory, copy our udev rules [#fudev]_ to
``/etc/udev/rules.d``::

  $ sudo cp support/scripts/45-maple.rules /etc/udev/rules.d/45-maple.rules

Then restart udev.

**Debian-based distros**:

  Make sure you are in the plugdev group (e.g. by running ``$ groups``
  and seeing if the output includes "plugdev").  If not, add yourself
  to plugdev with ::

    $ sudo usermod -a -G plugdev $USER

  then log back out and log back in.

  After that's done, restart udev::

    $ sudo restart udev

**Red Hat-based distros**:

  ::

    $ udevadm control --reload-rules

After restarting ``udev``, you'll need to unplug and re-plug your
Maple.

So far, so good?
~~~~~~~~~~~~~~~~

Great! Test your setup by :ref:`compiling a sample program
<toolchain-test>`.

.. _toolchain-osx-setup:

OS X
^^^^

These instructions have been tested successfully on OS X 10.6.4.

1. Collect and Install Tools
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

First, you'll need some tools. [#fpackman]_

* `XCode <http://developer.apple.com/technologies/xcode.html>`_:
  Provides compilers and other basic tools of the trade.  XCode was
  once free of charge, but Apple has since begun charging for it. If
  you'd rather not pay, you can probably get by with just a `make
  <http://www.gnu.org/software/make/>`_ binary, but you're on your
  own.

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

  PySerial is also available via ``easy_install``, so if you're
  comfortable using that, you could alternatively install it with ::

      $ easy_install pyserial

2. Fetch ``libmaple`` and Compiler Toolchain
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

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
~~~~~~~~~~~~~~~~

Great! Test your setup by :ref:`compiling a sample program
<toolchain-test>`.

.. _toolchain-win-setup:

Windows
^^^^^^^

These instructions have been tested successfully on Windows XP SP3.

1. Collect and Install Tools
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You'll need a few software tools for compiling and uploading programs.

* `Git`_, a versioning system we use for :ref:`libmaple`.  Install Git
  using the wonderful `Windows guide on GitHub
  <https://help.github.com/articles/set-up-git#platform-windows>`_.

  .. note:: These instructions use Git Bash, the command-line
            interface to Git on Windows. You can use the GitHub for
            Windows application instead, but we haven't tried.

* `Install Python <http://python.org/download>`_.  Choose the latest
  **2.7.x version**; Python 3 might work, but it's not tested.

* `Install PySerial <http://pypi.python.org/pypi/pyserial>`_.  Choose
  the latest **pyserial-x.y-win32.exe version** (or the "py3k" version
  if you installed Python 3).

2. Fetch ``libmaple`` and Compiler Toolchain
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

First, make a Git clone of :ref:`libmaple`. Do this by running Git
Bash (which you installed in step 1), typing the following line, and
hitting return. (Do not type the "$".  We put these in to remind you
that lines like this are for the Git Bash prompt). ::

    $ git clone git://github.com/leaflabs/libmaple.git

.. note:: Keep the Git Bash window open as you go.

You now have the libmaple repository in the folder ``C:\Documents and
Settings\<Your Name>``.

Next, download the `compilers and other tools
<http://static.leaflabs.com/pub/codesourcery/gcc-arm-none-eabi-latest-win32.tar.gz>`_
you'll use to build and upload your programs.  When the download
finishes, move the file into the libmaple repository's folder. Then
type these two lines into the Git Bash prompt to go to the libmaple
folder and extract the archive::

    $ cd libmaple
    $ tar xzf gcc-arm-none-eabi-latest-win32.tar.gz

This will create a folder named "arm" inside the libmaple folder.

You'll now configure your system to use these tools. Type the
following lines into Git Bash.

.. warning:: If you've installed Bash on your computer before starting
   this guide, and have a .bashrc already, typing these lines will
   overwrite it. If that's the case, we assume you know what you're
   doing, and can modify your .bashrc appropriately.

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
look like at this point (the green prompts and output after the ``git
clone`` line will be slightly different):

.. _toolchain-git-bash-screenshot:

.. figure:: /_static/img/winxp-git-bash-screenshot.png
   :align: center
   :alt: Git Bash screenshot

3. Check Your Setup
~~~~~~~~~~~~~~~~~~~

Let's check that you completed the previous step correctly.  If you
did, there will be a file called ".bashrc" (the period is supposed to
be there) in the folder ``Documents and Settings\<Your Name>\``.  Open
this file in Notepad by right clicking on it and selecting "Open
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
the Notepad window (don't save any changes you may have accidentally
made).

So far, so good?
~~~~~~~~~~~~~~~~

Great! Go on to the next section, where you'll compile a program.

.. _toolchain-test:

Test compilation
----------------

Get back into the libmaple directory (this tutorial assumes you put it
in :file:`libmaple` under your home directory) and test that you've
installed all the compilation tools correctly::

  # Note: Use "cs-make" instead of "make" on Windows
  $ cd ~/libmaple
  $ cp main.cpp.example main.cpp
  $ make clean
  $ make

.. note:: These instructions are for the Maple.  If you're compiling
   for another board, you'll need to set a ``BOARD`` environment
   variable appropriately.  For example, to compile for Maple Mini (in
   Bash), run::

     $ export BOARD=maple_mini
     $ make

   You can also use the following, but you'll need to write the
   ``BOARD=maple_mini`` part every time you call ``make`` (for ``make
   install``, etc.)::

     $ BOARD=maple_mini make

   To get a list of all boards, run ::

     $ make list-boards

   To make this setting permanent, put the ``export BOARD=maple_mini``
   line in your .bashrc.

If all goes well, you should see a bunch of output, then something
like this::

  Final Size:
     text          data     bss     dec     hex filename
    13164          1704     552   15420    3c3c build/maple.elf

The ``dec`` field at the end gives the total program size in
bytes. The long table of object files above the ``Final Size`` shows
similar information on a per-file basis. You can use it to help slim
down programs that use too much space.

.. _toolchain-upload:

Upload a program
----------------

Let's blow away the little example program and upload the interactive
test session to your Maple.  This will let you interact with the Maple
over a :ref:`USB serial port <usb>`. If you're on Linux, then before
executing ``make install``, you'll want to have the udev rules setup
:ref:`as described above <toolchain-udev>`.

Plug in your Maple using the Mini-B USB cable, then run ::

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
device file will look something like :file:`/dev/ttyACMXXX` on Linux,
:file:`/dev/tty.usbmodemXXX` on OS X, or :file:`COMx` on Windows, but
``XXX`` will vary depending on your system.  Try using one of these to
find out which it is::

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

If the interactive test program built and uploaded correctly,
``screen`` won't report any errors, and will present you an empty
terminal.  Your board is now waiting for you to send it a command.
Type ``h`` to print a list of commands which demonstrate various
features; type any command's letter to run it.

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
it lets you use `GDB
<http://www.gnu.org/software/gdb/documentation/>`_ to single-step
through your code, inspect variables, etc.

You can build your projects for JTAG or SWD upload with the ``jtag``
Makefile target. Instead of compiling with ``make``, compile with
``make jtag``. Then use your method of choice to upload the resulting
program, which will be in ``build/<your-board>.elf`` in the libmaple
directory.

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

.. _PySerial: http://pyserial.sourceforge.net/
.. _OpenMoko: http://openmoko.com/
.. _Git: http://git-scm.com/
.. _dfu-util: http://wiki.openmoko.org/wiki/Dfu-util

.. rubric:: Footnotes

.. [#fudev] As a security precaution on Linux, unknown USB devices can
   only be accessed by root. This udev script identifies the Maple
   based on its vendor and product IDs, mounts it to
   :file:`/dev/maple`, and (for Debian-based distros) grants
   read/write permissions to the ``plugdev`` group.

.. [#fpackman] Some of these software packages might be available on
   `MacPorts <http://www.macports.org/>`_ or `Homebrew
   <http://mxcl.github.com/homebrew/>`_. The author had some bad
   experiences with MacPorts a few years ago, though, and hasn't
   touched a package manager on OS X since. Your mileage may vary.
