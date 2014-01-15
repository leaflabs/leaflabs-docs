This file contains information useful for the documentation's
maintainers. As such, it's probably only useful to LeafLabs
developers. Users can read the HTML for the latest release here:

    http://leaflabs.com/docs/

Things you can learn how to do from this file:

- Cut a release version
- Fix errors in/otherwise maintain the current docs release
- Add docs for a new board

Building Documentation for a Release
------------------------------------

This is the procedure to follow when building the documentation for a
versioned release.

Read the following "Background" section if you've never done this
before (or haven't done it in a while; things change).  Then do the
steps in the "Preparation" and "Cutting the Release" sections that
follow it.

If you're bugfixing the docs for a release that's already been
shipped, skip to "Maintaining a Release", below.

   ~~~~~~~~~~
   Background
   ~~~~~~~~~~

As a lightweight form of issue tracking, the documentation sources are
sprinkled (not to say "littered") with comments that begin with FIXME
or TODO, optionally followed by [milestone].

Here's a hypothetical example:

    .. TODO [1.4.0] Replace this section; new API is incompatible with 1.3.7

This means you should replace the docs section following the comment
before you build the HTML for version 1.4.0.

Here's a command line you can use to list the TODOs in the
documentation sources (run it from the top-level directory in the
repository):

    $ git grep -n 'FIXME\|TODO'

You can use the following to temporarily alias the above mouthful to
'todos':

    $ alias todos="git grep -n 'FIXME\|TODO'"

Then you can just run

    $ todos

to measure the joy that awaits you.

    ~~~~~~~~~~~
    Preparation
    ~~~~~~~~~~~

- FINISH THE FIXMEs/TODOs FOR THE CURRENT RELEASE!

  You may violate assumptions made elsewhere in the documentation if
  you don't.  This can lead to incoherent or incorrect documentation,
  which is usually worse than none at all.

  If the release you're building is vA.B.C, you can see the relevant
  TODOs with:

      $ todos | grep A\.B\.C

  If you find that you really can't finish the TODO, you should bump
  the version number in the comment.  Don't do this out of laziness.
  Seriously, don't.  We may have made promises to the users about what
  would happen when, and you might be breaking them.

- Pick the low-hanging fruit on any other FIXMEs/TODOs.

- Ask Git to tell you what's happened since the most recent libmaple
  release, and make sure that any major, potentially
  backwards-incompatible, etc. changes are appropriately documented.

  You can use three dots ("...") between the git tags for those
  releases in concert with "git log --oneline" to do this.

  For instance, from the libmaple repository, you can use the
  following to tell you what happened in between 0.0.9 and 0.0.10:

      $ git log --oneline 0.0.9...0.0.10

  As an example of what the output might cause you to do, consider the
  following line (which appears in the output for 0.0.9...0.0.10):

      4941335 Adding rcc_dev_clk(), an accessor for a peripheral's clock line.

  Did the author of that commit (or some other interested party)
  remember to pull in the documentation for rcc_dev_clk() into the
  libmaple API page for rcc.h?  Go check!

- Do something similar for Maple IDE.  The IDE changes a lot more
  slowly, so there should be less to do.

    ~~~~~~~~~~~~~~~~~~~
    Cutting the Release
    ~~~~~~~~~~~~~~~~~~~

- Make a release branch in Git.  For release A.B.C, call it
  vA.B.C-maintenance.  You spell that

      $ git checkout -b vA.B.C-maintenance

  DON'T MAKE A TAG.  There are inevitably mistakes in the docs, some
  of which will be noticed and corrected, making a fixed tag useless.
  When you correct the errors, you'll need to update this branch,
  possibly also cherry-picking or otherwise adding into master.  See
  "Maintaining the Release", below.

- Do all the TODOs which must happen for _every_ release. (These are
  distinct from the ones that must happen for some _particular_
  release).  You can find most of these with

      $ todos | grep RELEASE

  However, you'll also need to check source/conf.py, as e.g. a
  release's configuration file needs to have a version entered into
  it.

  DON'T FORGET TO COMMIT YOUR CHANGES.

- Run "$ make mrproper" from the libmaple directory, and "$ make
  clean" from this directory, in order to wipe out existing old docs.

- Run "$ make doxygen" from the libmaple directory, and copy its
  doxygen/xml directory to doxygen/xml in this directory, and commit
  it in the vA.B.C-maintenance branch.

  (This makes later maintenance commits easier, and keeps a single

- Finally, you can actually build the docs. (See README-building.txt
  for instructions if you've never done this before.)

  DON'T FORGET TO PUSH THE RELEASE BRANCH TO GITHUB.

Maintaining a Release
---------------------

So a released version's documentation contains unforgivable lies, huh?
It needs to be updated RIGHT AWAY, you say?  Here's what you do:

- Check out the release branch for the version of the docs you care
  about (see "Cutting the Release", above).

- Make your changes.

- Rebuild the docs (see the last two steps in "Cutting the Release")
  and look at the changed pages.

- If your changes also need to happen on the master branch, make them
  appropriately.

  Advice: git cherry-pick is your friend.  Let's say you're on branch
  "vX.Y.Z-maintenance", and you want to get commit C onto master:

             o---C  vX.Y.Z-maintenance
            /
      -o---o---o---o  master

  The recipe is:

      $ git checkout master
      $ git cherry-pick C

  Which (if there are no conflicts) will result in:

             o---C  vX.Y.Z-maintenance
            /
      -o---o---o---o---C'  master

  Where C' performs the same changes as C.

- Push your fixes to GitHub.

- Distribute the updated docs.  These are world-visible here:

      http://static.leaflabs.com/pub/leaflabs/maple-docs/

Adding a New Board
------------------

Adding documentation for a new board is not just a matter of shoving a
file for it into source/hardware/!

Other things you must consider:

- Various places in the docs link to particular kinds of pin maps for
  each board.  When you add a new board, you must update these as
  well.  Here's the list; please keep it current (files are relative
  to the source/ directory):

  * external-interrupts.rst: EXTI line pin maps
  * timers.rst: timer pin maps
  * adc.rst: low-noise ADC banks
  * usart.rst: USART pin maps
  * gpio.rst: master pin maps
  * bootloader.rst: flashing a custom bootloader

- The quickstart document may not explain how to use the new board.
  If the board is different enough, a new, special-purpose quickstart
  may need to be written for it.  Therefore, read the quickstart in
  its entirety and update it appropriately.

  Take this step seriously.  The quickstart is the first thing users
  read when starting out, and first impressions matter.
