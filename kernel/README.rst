These files go in the kernel source tree after patching with this:

https://github.com/philmmanjaro/linux-bootsplash

Then copy the logo.gif file and build script to the ``tools/bootsplash``
directory in the kernel source tree, then ``make menuconfig`` and select
the BOOTSPLASH option under the console framebuffer section in graphics
device drivers.  Build a new kernel, then cd into tools/bootsplash and
run the build script::

  # cd tools/bootsplash
  # ./bootsplash-orchard.sh

to build the ``bootsplash`` binary, then copy it to somwhere under the
``/lib/firmware`` path such as::

  # mkdir /lib/firmware/bootsplash
  # cp bootsplash /lib/firmware/bootsplash/mybootsplash

Finally, configure grub to add the bootsplash path to the kernel cmdline.
Remove any existing splash arguments for fbsplash or plymouth, then add
``bootsplash.bootfile=bootsplash/mybootsplash`` where the path is relative
to the ``/lib/firmware`` directory.

.. note:: The bootsplash bin needs to be rebuilt using the tools in the
          kernel source tree if logo.gif is changed.
