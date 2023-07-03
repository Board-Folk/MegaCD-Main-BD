# Sega Mega CD Main BD Reproductions

This repository contains recreations of main board PCBs for Sega's Mega CD/Sega
CD add-on for the Mega Drive/Genesis console. These boards are often subject to
damage caused by leaking capacitors and/or batteries. The recreations are based
on the available schematics and scanned images of the original boards' copper
layers, so should be reasonably accurate reproductions.


## Revisions

Current research suggests that there were 3 PCB part numbers for the main board.
One of these was used with two different MCE chips (the large 208-pin custom 
chip) resulting in four known revisions. Aside from the markings on the board,
the revisions are easily identified using the table below. Obviously, be sure to
select the correct replacement board for your purposes.

|Board        | CPU RAM |  MCE Chip        | MCE Logic    | Export | PCM Chip  | PCM Logic  | Project Status   |
|:------------|:-------:|:----------------:|:------------:|:------:|:---------:|:----------:|:----------------:|
|837-8015     |   Zip   |  315-5477 (MCE1) | JK-FF (IC19) | No     | 315-5476  | None       | Testing          |
|837-8015-01  |   Zip   |  315-5548 (MCE2) | D-FF (IC19)  | No     | 315-5476A | XOR (IC16) | Verified         |
|837-8952     |   SOJ   |  315-5548 (MCE2) | D-FF (IC17)  | Yes    | 315-5476A | XOR (IC12) | Work in progress |
|837-8952     |   SOJ   |  315-5632 (MCE3) | None (IC17)  | Yes    | 315-5476A | XOR (IC12) | Work in progress |

Of these revisions, only the schematics for `837-8015-01` are easy to find
online. Luckily there are only a few minor differences between the revisions,
all of which are now documented in the schematics of this project.

Different revisions of the MCE require different support logic chips. On the
`837-8015` this is partially implemented in the "tree house" daughter board (on
which the oscillator is mounted) and the "connect board" which connects to the
console (see [this project](https://github.com/chris-jh/MegaCD-Connect-BD-Remake)
if you require a replacement). Later versions have no daughter board and have
connect boards with only passive components. Note that if you are mixing and
matching parts, there are also variations of the passive connect board with and
without particular capacitors, etc. installed. An incorrect combination will
usually manifest itself as graphical gliches on the BIOS "intro" screen.

For the `837-8952` be doubly sure to check which MCE revision is
used and therefore whether `IC17` should be populated or not.

Rumour has it that the MCE3 chip (315-5632) can be used on the 837-8015 board
*__if__* you also use the passive style connect board. I have not yet confirmed
this to be the case but it is plausible judging by the schematics.

If you have a revision or combination not listed above, we'd be interested to
hear about it.


# Bill of Materials

Most parts are marked on the board and it is expected that these will be reused
from a donor board. It is completely possible that your particular board uses
different (but compatible) parts so it's adviable to take photos before starting.
The zip RAM is not marked but their position is obvious from the number of pins.
Take care to mount the SMD RAM in the correct positions as some parts have very
similar part numbers.

Below is therefore a partial bill of materials for parts whose values are not
marked on the boards and/or look otherwise alike.

Capacitor voltages may exceed those given, within reason. E.g. you may
substitute 10V for a 6.3V part. Do not, however, use a lower voltage than
specified. No voltage is specified for the ceramic capacitors; any 0805 part is
expected to exceed the required voltage anyway. For SMD electrolytics a diameter
of 3-4mm is specified but you can just about get away with 4.3mm.

The right-most columns indicate whether (and where) the part is populated on that
revision. T = Top of board, B = bottom of board and a "-" = unpopulated. As a rule
THT and electrolytic capacitors are on top, ceramic capacitors and resistors on
the bottom. The exception is the two LEDs (`L1` and `L2`) which mount, bent at
right angles, to the bottom of the board. For best results, mount these facing
outwards, towards the front of the machine.

|Reference|Value|Voltage|Footprint|Decoupling|Schematic|837-8015|837-8015-01|
|:--------|:---:|:-----:|:-------:|:--------:|:-------:|:------:|:---------:|
|C1|1uF||0805|N|IC9 CT-GND|B|B|
|C2|22nF||0805|Y|IC1|B|B|
|C3|22nF||0805|Y|IC10|B|B|
|C4|22nF||0805|Y|IC4|B|B|
|C5|22nF||0805|Y|IC5|B|B|
|C6|22nF||0805|Y|IC6|B|B|
|C7|22nF||0805|Y|IC7|B|B|
|C8|22nF||0805|Y|IC8|B|B|
|C9|10uF|16V|SMD 3-4mm|Y|IC1|T|T|
|C10|10uF|16V|SMD 3-4mm|Y|IC7|T|T|
|C11|10uF|16V|SMD 3-4mm|Y|IC5|T|T|
|C12|10uF|16V|SMD 3-4mm|Y|IC6|T|T|
|C13|10uF|16V|SMD 3-4mm|Y|IC8|T|T|
|C14|22nF||0805|Y|IC9|B|B|
|C15|n/u|-|-|N|IC5 PRAS GND|-|-|
|C16|n/u|-|-|N|IC5 PCAS GND|-|-|
|C17|n/u|-|-|N|IC6 PRAS GND|-|-|
|C18|n/u|-|-|N|IC6 PCAS GND|-|-|
|C19|n/u|-|-|N|IC7 PRAS GND|-|-|
|C20|n/u|-|-|N|IC7 PCAS GND|-|-|
|C21|n/u|-|-|N|IC8 PRAS GND|-|-|
|C22|n/u|-|-|N|IC8 PCAS GND|-|-|
|C23|10uF|16V|SMD 3-4mm|Y|IC2|T|T|
|C24|22nF||0805|Y|IC2|B|B|
|C25|22nF||0805|Y|OSC1|B|B|
|C26|100uF|6.3V|THT 5mm pitch|Y|CN1|T|T|
|C27|22nF||0805|Y|IC11|B|B|
|C28|10uF|16V|SMD 3-4mm|Y|IC11|T|T|
|C29|100pF||0805|N|IC11 ERAS-GND|B|B|
|C30|22nF||0805|Y|IC12|B|B|
|C31|10uF|16V|SMD 3-4mm|Y|IC12|T|T|
|C32|100pF||0805|N|IC12 ORAS-GND|B|B|
|C33|n/u||0805|N|IC12 OCAS-GND|-|-|
|C34|100pF||0805|N|IC12 OWE-GND|B|B|
|C35|n/u||0805|N|IC11 ECAS-GND|-|-|
|C36|100pF||0805|N|IC11 EWE -GND|B|B|
|C37|10uF|16V|SMD 3-4mm|Y|IC3|T|T|
|C38|22nF||0805|Y|IC3|B|B|
|C39|22nF||0805|Y|IC13|B|B|
|C40|22nF||0805|Y|IC14|B|B|
|C41|10uF|16V|SMD 3-4mm|Y|IC14|T|T|
|C42|10uF|16V|SMD 3-4mm|Y|IC13|T|T|
|C43|22nF||0805|Y|IC15|B|B|
|C44|22nF||0805|Y|IC17|B|B|
|C45|22nF||0805|Y|IC18|B|B|
|C46|10uF|16V|SMD 3-4mm|Y|IC15|T|T|
|C47|200pF||0805|N|IC15 LRCKB-GND|-|B|
|C48|100uF|6.3V|THT 5mm pitch|Y|CN3|T|T|
|C49|22nF||0805|Y|IC16|B|B|
|C50|22nF||0805|Y|IC19|B|B|
|C51|22nF||0805|Y|IC20|B|B|
|C52|22uF||0805|Y|IC2|-|B|
|C53|10uF|16V|SMD 3-4mm|Y|IC2|-|T|
|C54|n/u 100pF||0805|N|IC1 D10-GND|-|-|
|C55|n/u||0805|N|FB5-GND|-|-|
|C56|n/u 33pF||0805|N|IC3 XIN-GND|-|-|
|C57|n/u||0805|N|IC16 ASEL-GND|-|-|
|C58|n/u||0805|N|IC16 CLWE-GND|-|-|
|CX1|51pF||THT axial\*|N|IC4 BROM-GND|B|-|
|R1|4.7K||0805||IC1 RES-VCC2|B|B|
|R2|4.7K||0805||IC1 HALT-VCC2|B|B|
|R3|2.2K||0805||IC10 A12-VCC2|B|B|
|R4|360||0805||LD1|B|B|
|R5|160||0805||LD2|B|B|
|R6|4.7K||0805||TR2|B|B|
|R7|4.7K||0805||TR1|B|B|

\* `CX1` (to give it a name) was mounted on the bottom of `837-8015` boards
from the factory, between pins 2 and 38 of `IC4`. You may like to replicate
this the same way, or you may use the extra footprint provided for this
purpose. You may even want to live dangerously and leave it off.


## Modifications

Whilst the PCB layouts are meant to be close replicas of the original, some
minor practical modifications have been made.

### 837-8015 (Japanese "Rev 0")
This revision came from the factory with a capacitor installed directly to the
underside of `IC4` (the ROM). For your convenience a dedicated footprint `CX1`
has been added so this can be mounted more neatly. When using a socket, it
should even be possible to install this capacitor on the top side of the board.

Two bare copper areas have been left near the edge of the board for fitting the
additional ground wires originally connected on the underside to pin 5 of `IC6`
and `IC8`. It is a good idea to fit these, otherwise these chips and `IC7` are
grounded only by means of one thin trace. Unfortunately, due to crowding of
traces in the area, this is not easily fixed on the board itself.

### Zip-to-SOJ DRAM Adapter Boards
Due to concerns regarding the availability of the smaller zip DRAM chips, two
adapter boards have been created to allow the use of the SOJ part found on
the `837-8952` with earlier revisions. The footprints are tailored to the
reproduction boards but should also be usable on originals.

Installation is reasonably self-explanatory; fit the SOJ RAM to the adapter
board and use header pins or similar to install this in place of the original
zip chips. Capacitor C2 may benefit from bending the legs 90 degrees so it
sits to the side of the board, depending on its physical size. On both boards,
it may also be useful/necessary to desolder `FR5` and orient this parallel to
the PCB to improve clearance. It should be fine to remove/leave off the
decoupling capacitors for the zip RAM (`C10`, `C11`, `C12`, `C13`) from the
main board too if this helps.

Many pins are common to all the zip chips so not all pins need to be
connected to the adapter. The required pins are circled on the board. It
should not harm anything to connect the others (e.g. to improve structural
stability) but this may introduce some additional noise.


# Additional Resources

If you require the SEGA font for producing a logo on the board, you may
consider [this one](http://actselect.chips.jp/fonts/11.htm). Note that the
author specifies that this is allowed for personal, non-commercial use only
and may not be redistributed.


# Thanks

  * Simon "Aergan" Lock ([@Aergan](https://github.com/Aergan)) for your
    insights, advice, support and expert testing of the first boards.

  * Chrissy ([@chris-jh](https://github.com/chris-jh)) for the connect board
    reproduction project, support and testing.

  * Zaxour, @PointerFunction and the rest of the Board Folk for their support
    and general coolness.


# Legal

As the product of this project is a replica of a proprietary product, the
the author makes no claim of copyright to the schematics nor PCB layouts and
releases these into the public domain, solely for the purposes of study and
historical preservation.

You are free to produce PCBs based on this project's designs at your own risk
and without limitation, for your own use or for sale and/or repair at a
reasonable price. Attribution is appreciated. The authors are not obliged to
provide support of any kind.

Under no circumstances will the authors be held responsible or liable in any
way for losses, damages or costs resulting from the use of the information
and/or resources of this project.

The resources are provided "as-is" without warranty of any kind, either
expressed or implied, including, but not limited to, the implied warranties
of merchantability and fitness for a particular purpose.
