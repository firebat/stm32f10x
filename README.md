# Requirement

## Software

    $ cat /etc/apt/sources.list
    deb http://mirrors.ustc.edu.cn/debian testing main non-free contrib
    deb http://http.debian.net/debian jessie-backports main

    $ apt-get install gcc-arm-none-eabi gdb-arm-none-eabi cmake openocd

Download "STM32F10x standard peripheral library" from http://www.st.com/web/en/catalog/tools/PF257890 and unzip
to ~/libraries/STM32F10x_StdPeriph_Lib_V3.5.0/

# Build

    $ mkdir build
    $ cd build
    $ cmake ../hello
    $ make

# Download

    $ openocd -f ../openocd.cfg

    $ telnet localhost 4444
    > halt
    target state: halted
    target halted due to debug-request, current mode: Thread
    xPSR: 0x01000000 pc: 0x080001f8 msp: 0x20001fe8
    > flash write_image main.bin 0x08000000
    wrote 1200 bytes from file main.bin in 0.064027s (18.303 KiB/s)
    >

# Debug

    $ arm-none-eabi-gdb main.elf
    (gdb) target remote localhost:3333
    Remote debugging using localhost:3333
    0x080001da in inc () at /home/tom/Desktop/stm32/demo/hello/main.c:6
    6     i+=off;
    (gdb) monitor reset halt
    ...
    (gdb) load
    Loading section .text, size 0x498 lma 0x8000000
    Loading section .data, size 0x18 lma 0x8000498
    Start address 0x8000214, load size 1200
    Transfer rate: 2 KB/sec, 600 bytes/write.

    (gdb) p i
    $1 = 0
    (gdb) p off
    $2 = 5

    (gdb) continue
    ...

# Others
- http://milksnot.com/content/arm-cortex-m3-getting-started
- Discovering the STM32 Microcontroller
- The Definitive Guide to the ARM Cortex M3
- Cortex-M3 Technical Reference Manual
- Linker & Loader