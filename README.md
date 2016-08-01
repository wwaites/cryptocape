# FreeBSD Beaglebone Black + Cryptocape

This directory contains materials for getting some of the
hardware on the [Cryptocape][1] working with FreeBSD. It
might also be a useful starting point for others accessing
some of the hardware features of the Beaglebone which are
not enabled by default.

To get some of the hardware to work, the pin multiplexer
must be configured. This is done, for example, to enable
UART4 to communicate with the on-board ATMega328p. The 
way this is done has changed somewhat between FreeBSD 10
and 11 and now the registers are written in the DTS 
simply by their number. The correct number can be found
in Section 9.3 of the, very long, [Technical Reference
Manual for the AM3358][2]

## Building a DTB

This should simply be done by running make in the dtb
directory, with system source code installed in the
usual place, /usr/src/sys:

    make -C dts

The resulting DTB file can then be copied to /boot/dtb.
It is necessary to instruct the boot loader to use it,
as opposed to the default device tree file by placing

    fdt_file=bbb-cryptocape.dtb

in /boot/msdos/uenv.txt

## Kernel configuration

The BBBC kernel config can be placed in
/usr/src/sys/arm/conf as usual and used to build a kernel. 
The main difference from the generic BEAGLEBONE kernel is
the inclusion of the icee EEPROM driver and the DS3231
real time clock driver.

[1]: https://cryptotronix.com/products/cryptocape/
[2]: http://www.ti.com/lit/pdf/spruh73
