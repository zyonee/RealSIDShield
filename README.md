# RealSIDShield Version 1.0

Copyright (c) 2012,2013, A.T.Brask (atbrask[at]gmail[dot]com)

This is an Arduino shield that makes it easy to use a MOS Technology 6581/8580 SID chip (the famous C64 sound chip). This repository contains all necessary PCB design files as well as some photos and a bit of demonstration code. At some point I'll write a post about it on my blog at http://www.atbrask.dk/ with some further explanations and perhaps some audio/video examples.

The design works without any big problems. There are a couple of minor issues, but I think it's good enough to release into the wild. The board basically provides the necessary support electronics for the SID chip to work and be accessible from the Arduino. So far, I have only tested it with a 8580, but it should work fine with a 6581 too. The biggest difference is the VDD voltage for the SID chip. The board includes a little step-up converter for this. Once a board is built, it can only be used with one of the two kinds of SID.

The example code is a simple music player that plays .SID files. It consists of a Python script that emulates the Commodore 64 CPU (using the py65 package from PyPI) and an Arduino sketch that handles the SID chip.

I did have a few left over PCBs for sale, but as of October 2015 I'm all out. If anyone is interested, they can pretty easily order new ones themselves from a PCB house using the gerber files in this repository. If any specific components are unavailable/EOL you can just swap them for similar ones. Only a few of the capacitors and resistors are more or less critical.

## IMPORTANT NOTES

The Arduino sketch code has only been tested on an Arduino Uno. The code uses direct port access for I/O and depends on the specific mapping from the B and D ports on an ATmega168/328 to the digital pins on the Arduino board. This makes the code incompatible with Arduino boards with different port/pin mappings. One such case is the Arduino Leonardo which is currently not (yet) supported.

**!!! BUILD AT YOUR OWN RISK !!!**

If you end up frying your SID chip (or any other equipment), it's not my problem. :-)

Some of the component values depend on the model of SID you plan to use with the shield. This is very important to get right. Plugging a 8580 into a 6581 board may damage the chip. The other way around is probably less damaging, but it would simply not yield any sound. Please use an IC socket for the SID chip. It hurts to see it get soldered in place... :-)

If you build this board, please check that the correct voltage is present on the SID chip's pin 28 (VDD) before you plug in the chip. It should read 9V for a 8580 board and 12V for a 6581 board.

## KNOWN ISSUES

1) There are no C6 or C7. These were added for the analog paddle inputs, but this feature was scrapped.

2) The design specifies 560pF for C10. However, this yielded a too-low switching frequency in the step-up converter. As far as I remember, I switched this with a 220pF. The step-up converter is still noisy, but at least it doesn't have a very annoying audible tone.

3) The output stage was copied verbatim from an old C128 schematic. However, it seems to have a large gain, which makes the output very loud.

## BOM (6581)

| Qty | Value           | Device                 | Package           | Parts           | Description                       |
|-----|-----------------|------------------------|-------------------|-----------------|-----------------------------------|
|  2  | 220pF           | SMD MLCC               | 0805              | C10, C12        | (C10 originally 560pF, see notes) |
|  3  | 470pF           | SMD MLCC               | 0805              | C1, C2, C11     |                                   |
|  1  | 1nF             | SMD MLCC               | 0805              | C9              |                                   |
|  3  | 100nF           | SMD MLCC               | 0805              | C3, C4, C5      |                                   |
|  1  | 10µF            | SMD Electrolytic       | 5.3mm             | C14             |                                   |
|  3  | 100µF           | SMD Electrolytic       | 7.7mm             | C8, C13, C15    |                                   |
|  1  | SK 34           | SMD Diode              | DO-214AC=SMA      | D1              |                                   |
|  1  | JACK_PLUG       | Jack plug              | MX-387GL          | J1              |                                   |
|  1  | 1µH             | SMD Inductor           | 1812              | L1              |                                   |
|  1  | 330µH           | SMD Inductor           | Fastron_PISN      | L2              |                                   |
|  1  | BC847           | SMD Transistor NPN     | SOT-23            | Q1              |                                   |
|  1  | 1 Ohm           | SMD Resistor           | 0805              | R8              |                                   |
|  1  | 100 Ohm         | SMD Resistor           | 0805              | R7              |                                   |
|  2  | 1 kOhm          | SMD Resistor           | 0805              | R1, R3          |                                   |
|  1  | 1.5 kOhm        | SMD Resistor           | 0805              | R6              |                                   |
|  1  | 10 kOhm         | SMD Resistor           | 0805              | R2              |                                   |
|  1  | 13.5 kOhm       | SMD Resistor           | 0805              | R4              |                                   |
|  1  | 47 kOhm         | SMD Resistor           | 0805              | R5              |                                   |
|  1  | 74574           | Octal D-Type flip-flop | SO20-L            | U1              |                                   |
|  1  | MOS6581         | MOS 6581 (SID)         | DIL28             | U2              |                                   |
|  1  | MC34063A        | Switch regulator       | SO-8              | U3              |                                   |

## BOM (8580)

| Qty | Value           | Device                 | Package           | Parts           | Description                       |
|-----|-----------------|------------------------|-------------------|-----------------|-----------------------------------|
|  2  | 220pF           | SMD MLCC               | 0805              | C10, C12        | (C10 originally 560pF, see notes) |
|  1  | 470pF           | SMD MLCC               | 0805              | C11             |                                   |
|  1  | 1nF             | SMD MLCC               | 0805              | C9              |                                   |
|  2  | 22nF            | SMD MLCC               | 0805              | C1, C2          |                                   |
|  3  | 100nF           | SMD MLCC               | 0805              | C3, C4, C5      |                                   |
|  1  | 10µF            | SMD Electrolytic       | 5.3mm             | C14             |                                   |
|  3  | 100µF           | SMD Electrolytic       | 7.7mm             | C8, C13, C15    |                                   |
|  1  | SK 34           | SMD Diode              | DO-214AC=SMA      | D1              |                                   |
|  1  | JACK_PLUG       | Jack plug              | MX-387GL          | J1              |                                   |
|  1  | 1µH             | SMD Inductor           | 1812              | L1              |                                   |
|  1  | 330µH           | SMD Inductor           | Fastron_PISN      | L2              |                                   |
|  1  | BC847           | SMD Transistor NPN     | SOT-23            | Q1              |                                   |
|  1  | 1 Ohm           | SMD Resistor           | 0805              | R8              |                                   |
|  1  | 100 Ohm         | SMD Resistor           | 0805              | R7              |                                   |
|  2  | 1 kOhm          | SMD Resistor           | 0805              | R3, R6          |                                   |
|  1  | 6.2 kOhm        | SMD Resistor           | 0805              | R4              |                                   |
|  1  | 10 kOhm         | SMD Resistor           | 0805              | R2              |                                   |
|  1  | 47 kOhm         | SMD Resistor           | 0805              | R5              |                                   |
|  1  | 74574           | Octal D-Type flip-flop | SO20-L            | U1              |                                   |
|  1  | MOS8580         | MOS 8580 (SID)         | DIL28             | U2              |                                   |
|  1  | MC34063A        | Switch regulator       | SO-8              | U3              |                                   |

