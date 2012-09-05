.. highlight:: sh

.. _unix-toolchain-win-setup:

Unix Toolchain Windows Setup
============================

This page contains instructions for setting up a Windows computer for
use with the :ref:`Unix toolchain <unix-toolchain>`.  (Setup
instructions for :ref:`other operating systems <toolchain-setup>` are
also available.)

These instructions have been tested successfully on Windows 7 Home
Premium.

.. contents:: Contents
   :local:

Collect and Install Tools
-------------------------

First, you'll need some tools.

* `GitHub for Windows <http://windows.github.com/>`_: this is a GUI
  for `Git`_, the version control system we use for :ref:`libmaple`.

  If you don't have one, you need to sign up for a (free) `GitHub
  account <https://github.com/signup/free>`_.

  .. note:: If you use Git from the command line, you can clone
            libmaple with::

              $ git clone git://github.com/leaflabs/libmaple.git

            If you go this route, you don't need a GitHub account.

* `Python`_: choose the **latest 2.7.x version**. (Python 3 works, but
  you're on your own.)

* `PySerial`_:  Choose the latest **pyserial-x.y-win32.exe version**.

Fetch ``libmaple`` and Compiler Toolchain
-----------------------------------------

First, make a Git clone of the :ref:`libmaple` repository with the
following steps:

1. **Run GitHub for Windows**, and **sign in** using your GitHub
   account.
2. **Visit** `libmaple's GitHub page
   <https://github.com/leaflabs/libmaple/>`_, and **sign in** to
   GitHub in your web browser as well.
3. **Click on the "Clone in Windows" button** on libmaple's GitHub
   page, which looks like this:

     .. figure:: /_static/img/github-clone-in-windows.png

   Your browser may prompt you about what to do when you click the
   "Clone in Windows" button. Choose the option that launches the
   GitHub for Windows application.

Next, you'll need to get some cross-compilers and other tools for
building and uploading your programs:

- `Download a .zip of the latest tools
  <http://static.leaflabs.com/pub/codesourcery/gcc-arm-none-eabi-latest-win32.zip>`_.

- Extract the .zip, and **move the extracted "arm" folder into the
  libmaple repository's folder**.

  You can open the libmaple repository folder by right-clicking
  libmaple in the main GitHub for Windows screen and choosing "open in
  explorer":

  .. figure:: /_static/img/win7-github-open-in-explorer.png
     :align: center

Update your PATH
----------------

You'll next need to configure your system to use the various tools
you've downloaded and installed. Do that by adding the Python and
``arm\bin`` directories to your PATH environment variable.

If you've never set environment variables before, this section
explains what to do.

**Add Python to your PATH**:

  Start by navigating to the folder where Python is installed on your
  system (this is probably ``C:\Python27``). Right click on the folder
  address, then choose "Copy address as text":

  .. figure:: /_static/img/win7-copy-python-address.png
     :align: center

  Next, open your environment variables window: from the Start/Windows
  menu, right click on Computer, then choose Properties > Advanced
  System Settings > Environment Variables. Under the "User variables
  for YOUR_USERNAME", look for PATH.

  - If PATH is missing from the list, click "New...".

    Under "Variable Name", write PATH. Under "Variable value", paste
    the Python address you just copied, and click OK. The result looks
    like this:

    .. figure:: /_static/img/win7-python-path.png
       :align: center

  - If PATH is present in the list, click on it and choose "Edit...".

    Go to the end of the "Variable value:" text box, type a semicolon
    (the ``;`` character), and then paste the path you just
    copied. Click OK.

  Test that this worked by running the Git Shell program that came with
  GitHub for Windows, then running ``python`` at the command prompt. You
  should get a Python interpreter that looks like this:

  .. figure:: /_static/img/win7-python-prompt.png
     :align: center

  If that worked, then close the window.

**Add compiler toolchain to your PATH**:

  Do this by adding the ``arm\bin`` directory (earlier instructions
  had you move ``arm`` to the libmaple repository folder) to your PATH
  environment variable in the same way you added Python.

  Copy the address of the ``arm\bin`` folder by right-clicking on it
  after navigating to it:

  .. figure:: /_static/img/win7-copy-arm-bin-address.png
     :align: center

  The PATH environment variable should exist from when you added
  Python to it, so make sure you choose "Edit..."  from the
  environment variables window. Then paste the ``arm\bin`` address you
  copied after typing a semicolon. The final result will look
  something like this:

  .. figure:: /_static/img/win7-python-arm-bin-path.png
     :align: center

  Click OK.

So far, so good?
----------------

Great! Open a new Git Shell, then type this at the prompt and hit
return to get to the libmaple directory::

  cd libmaple

.. warning:: You must open a new Git Shell window. If you use a shell
             that's already open, then the changes to PATH you just
             made won't be available, and the instructions in the next
             section won't work.

Now you're ready to move on by :ref:`compiling a sample program
<toolchain-test>`.
