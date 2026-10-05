# Bare-metal compression sample

This sample demonstrates compressing the RW data and using a decompressor routine at startup to build a smaller boot image.

The use of the inner and outer linker scripts allows the program to use RW variables without extra modification, as the
compressed rodata is decompressed into the expected address space before other code runs.

Notes:
- The decompressor code must be standalone and should not depend on any other code/data that may still be compressed
- QEMU is run with cpu-num=0 to start at the ELF entry point specified by the outer.ld phase (which corresponds to decompress.S)
  rather than the reset address.

This sample uses semihosting with
[QEMU Arm System emulator](https://www.qemu.org/docs/master/system/target-arm.html)
targeting the
[micro:bit board model](https://www.qemu.org/2019/05/22/microbit/).

Running the sample using `make run` should print the message found in demo.c