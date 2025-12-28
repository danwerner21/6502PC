# 6809PC
The 6502PC is a 6502 ATX format board with 512K RAM, 4K ROM, with a flexible programmable MMU, battery backed up RTC, 6551 UART, and 6 ISAish slots.  This computer will run a version of DOS/65 by the fantastic CUBIX operating system by Richard A. Leary.  

See this repo (https://github.com/danwerner21/6x0x-DOS65) for ROM image and operating system.

![System](images/6502PC.jpg)

## BUGS
On the V1.0 board /VMA is not asserted long enough and needs to be just tied to ground.

Patches:
 Lift Pin 1 of u5 74ls02.  Tie the socket of U5 pin 1 to ground.
 U47 SCRATCH CONNECTION TO PIN 3 ON BOTTOM OF PCB.  TIE U47 PIN 3 TO +5V (DO NOT USE PIN 18 OF U47)

Contrary to what is on the Schematic, the battery connector will not support a supercap, a battery is required.


This is corrected on the V1.1 board.




### Jumper Settings
        J1 - IRQ ASSIGNMENT FOR SLOT J2
        J2 - IRQ ASSIGNMENT FOR SLOT J4
        J5 - IRQ ASSIGNMENT FOR SLOT J6
        J7 - IRQ ASSIGNMENT FOR SLOT J8
        J9 - IRQ ASSIGNMENT FOR SLOT J10        
        J13 - IRQ ASSIGNMENT FOR SLOT J14
        
        K1 - ROM BANK SELECT 1&2-ROM IMAGE AT $6000-$6FFF  3&4-ROM IMAGE AT $7000-$7FFF
        P12- POWER SWITCH (MOMENTARY, ATX CASE SWITCH)
        JP1- RESET SWITCH (MOMENTARY, ATX CASE SWITCH)
        P16- BATTERY CONNECTION, P1=+ P2-4=-  (NON RECHARGEABLE)
        JP3- CTS FORCE HIGH
        P18- CONSOLE SERIAL CONNECTOR
        J11- TTL CONSOLE SERIAL CONNECTOR
        J12- ENABLE POWER TO TTL CONSOLE SERIAL CONNECTOR
        

### Building the system

### Default Memory Map
            $0000-$E000 - RAM
            $E000-$EFFF - Memory Mapped IO
            $F000-$FFFF - ROM
#### IO MEMORY MAP
            $E000-$EF7F - ISA IO SPACE
            $EF80-$EF8F - ACIA
            $EF90-$EF9F - RTC
            $EFA0-$EFAF - OPEN
            $EFB0-$EFBF - OPEN
            $EFC0-$EFCF - OPEN
            $EFD0-$EFDF - MMU TASK MAP
            $EFE0-$EFEF - MMU REGISTERS
            $EFF0-$EFFF - OPEN


### Bill Of Materials
Reference|Value|Qty|Field1|Description
---------|-----|---|------|-----------
C1-C4,C17|22 uF|5||Polarized capacitor
C5-C16,C18-C27,C29-C33,C36-C54,C56,C58,C62|0.1 uF|49||Unpolarized capacitor
C28|1uF|1||Polarized capacitor
C35|10uF|1||Polarized capacitor
C57|0.01 uF|1||Unpolarized capacitor
C59,C60|15pf|2||Unpolarized capacitor
C61,C63-C66|1.0 uF|5||Polarized capacitor
D1,D2|1N4148|2||Diode
D3,D4|D|2||Diode
J1,J2,J5,J7,J9,J13|IRQ Selection|6||Generic connector, double row, 02x06, odd/even pin numbering scheme (row 1 odd numbers, row 2 even numbers), script generated (kicad-library-utils/schlib/autogen/connector/)
J3,J4,J6,J8,J10,J14|Bus_ISA_8bit|6||8-bit ISA-PC bus connector
J11|TTL SERIAL CONSOLE|1||Generic connector, single row, 01x06, script generated (kicad-library-utils/schlib/autogen/connector/)
J12|TTL CONSOLE PWR|1||Generic connector, single row, 01x02, script generated (kicad-library-utils/schlib/autogen/connector/)
JP1,JP3|JUMPER|2||Generic connector, single row, 01x02, script generated (kicad-library-utils/schlib/autogen/connector/),Jumper, 2-pole, open
K1|ROM SELECT|1||Generic connector, single row, 01x03, script generated (kicad-library-utils/schlib/autogen/connector/)
P1|SHADOW ADDR|1||Generic connector, double row, 02x04, odd/even pin numbering scheme (row 1 odd numbers, row 2 even numbers), script generated (kicad-library-utils/schlib/autogen/connector/)
P11|CONN_10X2|1||Generic connector, double row, 02x10, odd/even pin numbering scheme (row 1 odd numbers, row 2 even numbers), script generated (kicad-library-utils/schlib/autogen/connector/)
P12|POWER_SW|1||Generic connector, single row, 01x02, script generated (kicad-library-utils/schlib/autogen/connector/)
P13|14.31818 MHz CLK|1||
P14|16.000Mhz|1||
P15|CPU CLOCK SPEED|1||Generic connector, double row, 02x04, odd/even pin numbering scheme (row 1 odd numbers, row 2 even numbers), script generated (kicad-library-utils/schlib/autogen/connector/)
P16|CONN_4|1||Generic connector, single row, 01x04, script generated (kicad-library-utils/schlib/autogen/connector/)
P17|1.8432 MHz CLK|1||
P18|SERIAL|1||Generic connector, double row, 02x05, odd/even pin numbering scheme (row 1 odd numbers, row 2 even numbers), script generated (kicad-library-utils/schlib/autogen/connector/)
R1,R3|10k|2||Resistor
R2|470|1||Resistor
R4,R7,R26|4.7K|3||Resistor
R5,R6,R8|1000|3||Resistor
RR1|2200|1||9 resistor network, star topology, bussed resistors, small symbol
RR2|22K|1||9 resistor network, star topology, bussed resistors, small symbol
SW1|POWER|1||Push button switch, generic, two pins
SW2|RESET|1||Push button switch, generic, two pins
U1|74LS04|1||Hex Inverter
U2,U34,U36,U39,U45,U46|74LS244|6||Octal Buffer and Line Driver With 3-State Output, active-low enables, non-inverting outputs
U3|74LS682|1||
U4|74LS86|1||Quad 2-input XOR
U5|74LS02|1||quad 2-input NOR gate
U6,U21|74LS00|2||quad 2-input NAND gate
U7,U10,U16|74LS32|3||Quad 2-input OR
U8|SRAM_512K|1||512K x 8 Low Power CMOS RAM, DIP-32
U9,U15|74LS08|2||Quad And2
U11|27C256|1||OTP EPROM 256 KiBit
U12,U22|74LS74|2||Dual D Flip-flop, Set & Reset
U13|6502|1||8-bit NMOS Microprocessor, 64K, DIP-40
U17|74LS14|1||Hex inverter schmitt trigger
U18|74LS06|1||Inverter Open Collect
U19|74HCT14|1||Hex inverter schmitt trigger
U23|74LS688|1||8-bit magnitude comparator
U24,U42|74LS138|2||Decoder 3 to 8 active low outputs
U25-U28,U32,U41|74LS245|6||Octal BUS Transceivers, 3-State outputs
U29|DS1233|1||
U30|74LS163|1||Synchronous 4-bit programmable binary Counter
U31|74LS240|1||Octal Buffer and Line Driver With 3-State Output, active-low enables, inverting outputs
U35|74LS174|1||Hex D-type Flip-Flop, reset
U37|74LS157|1||Quad 2 to 1 line Multiplexer
U38|74LS374|1||8-bit Register, 3-state outputs
U40|SRAM-32K|1||256K (32K x 8) Static RAM, 70ns, DIP-28
U43,U44|74LS257|2||Quad 2 to 1 Multiplexer
U47|M6242|1||M6242
U48|G65SC51P|1||CMOS Asynchronous Communication Interface Adapter (ACIA), Serial UART, DIP-28
U49|MAX232|1||Dual RS232 driver/receiver, 5V supply, 120kb/s, 0C-70C
X1|RTC_OSC|1|32.768 KHz|Two pin crystal
