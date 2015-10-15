# arch-esp8266-packages
Packages to compile ESP8266 programs on ArchLinux.

# Compilation notes
There is a cyclical dependency regarding newlib and gcc:
* NewLib requires a working C compiler to compile.
* Gcc C++ standard library requires a working Newlib to compile.

There are several ways to break this cycle:

## Compiling from scratch
* First compile and install xtensa-lx106-elf-binutils
* Edit xtensa-lx106-elf-gcc and \_bootstrap=0 to \_bootstrap=1, so it will only compile for C.
* Compile and install the changed xtensa-lx106-elf-gcc
* Compile and install newlib (I recommend the projectgus version)
* Compile and install the original unchanged xtensa-lx106-elf-gcc.

## Upgrading
Upgrading each individual package should be possible, given that you don't uninstall any of the other packages. If you'd like to be absolutely sure you have the latest version of everything, follow these steps:
* Compile and install the new newlib package (will compile with old GCC)
* Compile and install the new GCC package
* Compile and install the new newlib package again (will compile with new GCC)

## Using a precompiled package
If you have a precompiled package for either GCC or newlib you can use that to bootstrap the other, and work from there.
