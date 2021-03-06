Ubertooth Host
==============
This is host code for use with bluetooth_rxtx firmware.


REQUIRED SOFTWARE
-----------------
These tools link to libbtbb  (http://libbtbb.sourceforge.net/).
The versions tend to be matched, git should always work with git and all
releases should come in matched pairs (until the interface stabilizes).
Libbtbb can be retrieved from git and built as follows:
```
$ git clone git://git.code.sf.net/p/libbtbb/code libbtbb
$ cd libbtbb/
$ make
$ sudo make install
```
This software also requires libusb 1.0 or higher, which can be found at
http://www.libusb.org or installed from your OS's package repository.


Building
--------
Build the library and tools using the following steps:
```
$ mkdir build
$ cd build
$ cmake ..
$ make
$ make install (may require root privileges)
```

THE TOOLS
---------
ubertooth-util: various utility functions including reboot into bootloader DFU
mode.

ubertooth-rx: a general purpose Bluetooth sniffing tool, will promiscuously
find LAPs or, if given a LAP, will determine a UAP.  Given both a LAP and a UAP
it will attempt to calculate a clock and hop along with the piconet.

ubertooth-dump: dumps a raw Bluetooth symbol stream from an Ubertooth board.
If you pipe it into xxd, you should see various ones and zeros.  If you pipe it
into dd, you can find out the transfer rate (should be 1 MB/s).  Timestamps are
dumped to stderr.

ubertooth-specan: ouputs signal strength data suitable for feeding into spectrum
analyser software. e.g.

```
ubertooth-specan -G -q | feedgnuplot --stream 0.5 --domain --3d 
```

will use feedgnuplot to drive gnuplot to draw a realtime animated 3D plot of the
frequency spectrum.


PRIVLEDGE REDUCTION
-------------------
If you desire to run any program which accesses the ubertooth hardware as a user
you may do so by copying 40-ubertooth.rules to wherever your distro keeps udev
rules, typically /lib/udev/rules.d

This action will allow any user in the "usb" group to access the ubertooth
hardware. If you want to give access to a different group you can easily edit
the rules file and change usb to whatever group you prefer.
