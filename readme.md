# 6809PC
The 6502PC is a 6502 ATX format board with 512K RAM, 4K ROM, with a flexible programmable MMU, battery backed up RTC, 6551 UART, and 6 ISAish slots.  This computer will run a version of DOS/65 by the fantastic CUBIX operating system by Richard A. Leary.  

See this repo (https://github.com/danwerner21/6x0x-DOS65) for ROM image and operating system.

![System](images/6502PC.jpg)

## BUGS
On the V1.0 board /VMA is not asserted long enough and needs to be just tied to ground.

Patch:  Lift Pin 1 of u5 74ls02.  Tie the socket of U5 pin 1 to ground.

This is corrected on the V1.1 board.




### Jumper Settings

### Building the system



### Default Memory Map
            $0000-$E000 - RAM
            $E000-$EFFF - Memory Mapped IO
            $F000-$FFFF - ROM

### Bill Of Materials
Reference|Value|Qty|Field1|Description
---------|-----|---|------|-----------
