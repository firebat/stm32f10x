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
