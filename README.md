# Sega Mega CD Main BD Reproductions

This repository contains recreations of main board PCBs for Sega's Mega CD/Sega
CD add-on for the Mega Drive/Genesis console. These boards are often subject to
damage caused by leaking capacitors and/or batteries. The recreations are based
on the available schematics and reverse engineering using scanned images of the
original boards' copper layers, so should be reasonably accurate reproductions.


## Revisions

Current research suggests that there were 3 PCB part numbers for the main board.
One of these was used with two different MCE chips (the large 208-pin custom 
chip) resulting in four known revisions. Aside from the markings on the board,
the revisions are easily identified using the table below. Obviously, be sure to
select the correct replacement board for your purposes.

|Board       | CPU RAM | MCE Chip        | MCE Logic    | Region | PCM Chip  | PCM Logic  | Project Status |
|:-----------|:-------:|:---------------:|:------------:|:------:|:---------:|:----------:|:--------------:|
|837-8015    |   Zip   | 315-5477 (MCE1) | JK-FF (IC19) | Japan  | 315-5476  | None       | Testing        |
|837-8015-01 |   Zip   | 315-5548 (MCE2) | D-FF (IC19)  | Japan  | 315-5476A | XOR (IC16) | Verified       |
|837-8952    |   SOJ   | 315-5548 (MCE2) | D-FF (IC17)  | Export | 315-5476A | XOR (IC12) | Testing        |
|837-8952    |   SOJ   | 315-5632 (MCE3) | None (IC17)  | Export | 315-5476A | XOR (IC12) | Testing        |

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
usually manifest itself as graphical glitches on the BIOS "intro" screen.

For the `837-8952` be doubly sure to check which MCE revision is
used and therefore whether `IC17` should be populated or not.

Rumour has it that the MCE3 chip (`315-5632`) can be used on the `837-8015`
board *__if__* you also use the passive style connect board. We have not yet
confirmed this to be the case but it is plausible judging by the schematics.

If you have a revision or combination not listed above, we'd be interested to
hear about it.


## PCB Production

Minimum track widths, clearances and via sizes are within the standard
offering of modern PCB fabricators. Development was done using JLCPCB and
the boards therefore have their order number placeholder on the silkscreen,
which you may wish to remove if using another service.

We recommend using at least 4 layers for all boards. For optimal EMI
performance you may opt to use 6 layers by replicating the internal ground
and power planes (e.g. top, ground, power, power, ground, bottom) but this
is likely to be significantly more expensive.

* `837-8015`: the original boards were produced using a process that added
  a partial layer of copper on top of the signal layers, separated by some
  sort of dielectric coating. During testing, 2-layer boards without this
  copper layer suffered from noise issues so these have now been updated
  with internal power and ground planes.

* `837-8015-01`: this particular revision has improved routing and 2-layer
  boards have been shown to work. The design does however have 4 layers
  and we recommend using these.

* `837-8952`: the original "Export" board was 4 layers so this is also the
  only option due to reliance on internal ground and power planes.


## Bill of Materials

Most parts are marked on the board and it is expected that these will be reused
from a donor board. It is completely possible that your particular board uses
different (but compatible) parts so it's advisable to take photos before starting.
The zip RAM is not marked on the PCB but their position is obvious from the
number of pins. Take care to mount the SMD RAM in the correct positions as some
parts have very similar part numbers.

Below is therefore a partial bill of materials for parts whose values are not
marked on the boards and/or look otherwise alike. For the `837-8952` "Export"
boards, almost all references were renumbered so be sure to use the correct
column on the left to identify the parts. I would seriously recommend printing
the list and covering/removing/otherwise obscuring the irrelevant column to
avoid confusion.

Values for the capacitors unique to the `837-8952` "Export" board are based on
measurements of components on an original example and therefore potentially
inaccurate. The values are however also likely not very critical, e.g. 100pF
will probably be fine (maybe even closer to the original specification) where
133pF is stated. If in doubt, you may like to reuse the components from your
donor board.

Capacitor voltages may exceed those given, within reason. E.g. you may
substitute 10V for a 6.3V part. Do not, however, use a lower voltage than
specified. No voltage is specified for the ceramic capacitors; any 0805 part is
expected to exceed the required voltage anyway. For SMD electrolytics a diameter
of 3-4mm is specified. The originals are about 3mm but you can just about get
away with 4.3mm.

The right-most columns indicate whether (and where) the part is populated on that
revision. T = Top of board, B = bottom of board and a "-" = unpopulated. As a rule
THT and electrolytic capacitors are on top, ceramic capacitors and resistors on
the bottom. The exception is the two LEDs (`L1` and `L2`) which mount, bent at
right angles, to the bottom of the board. For best results, mount these facing
outwards, towards the front of the machine.

|Reference (Japan)|Reference (Export)|Value|Voltage|Footprint|837-8015|837-8015-01|837-8952|
|:---------------:|:----------------:|:---:|:-----:|:-------:|:------:|:---------:|:------:|
|C1|C1|1uF||0805|B|B|B|
|C2|C2|22nF||0805|B|B|B|
|C3|C3|22nF||0805|B|B|B|
|C4|C6|22nF||0805|B|B|B|
|C5|C5|22nF||0805|B|B|B|
|C6|-|22nF||0805|B|B|-|
|C7|-|22nF||0805|B|B|-|
|C8|-|22nF||0805|B|B|-|
|C9|C41|10uF|16V|SMD 3-4mm|T|T|T|
|C10|-|10uF|16V|SMD 3-4mm|T|T|-|
|C11|C42|10uF|16V|SMD 3-4mm|T|T|T|
|C12|-|10uF|16V|SMD 3-4mm|T|T|-|
|C13|-|10uF|16V|SMD 3-4mm|T|T|-|
|C14|C4|22nF||0805|B|B|B|
|C15|C32|n/u|-|-|-|-|-|
|C16|C22|n/u|-|-|-|-|-|
|C17|-|n/u|-|-|-|-|-|
|C18|-|n/u|-|-|-|-|-|
|C19|-|n/u|-|-|-|-|-|
|C20|-|n/u|-|-|-|-|-|
|C21|-|n/u|-|-|-|-|-|
|C22|-|n/u|-|-|-|-|-|
|C23|C43|10uF|16V|SMD 3-4mm|T|T|T|
|C24|C7|22nF||0805|B|B|B|
|C25|C11|22nF||0805|B|B|B|
|C26|C51|100uF|6.3V|THT 5mm pitch|T|T|T|
|C27|C9|22nF||0805|B|B|B|
|C28|C45|10uF|16V|SMD 3-4mm|T|T|T|
|C29|C23|100pF||0805|B|B|?|
|C30|C10|22nF||0805|B|B|B|
|C31|C46|10uF|16V|SMD 3-4mm|T|T|T|
|C32|C26|100pF||0805|B|B|?|
|C33|C27|100pF||0805|-|-|B|
|C34|C28|100pF||0805|B|B|B|
|C35|C24|100pF||0805|-|-|B|
|C36|C25|100pF||0805|B|B|B|
|C37|C47|10uF|16V|SMD 3-4mm|T|T|T|
|C38|C13|22nF||0805|B|B|B|
|C39|C14|22nF||0805|B|B|B|
|C40|C15|22nF||0805|B|B|B|
|C41|C48|10uF|16V|SMD 3-4mm|T|T|T|
|C42|C49|10uF|16V|SMD 3-4mm|T|T|T|
|C43|C16|22nF||0805|B|B|B|
|C44|C18|22nF||0805|B|B|B|
|C45|C17|22nF||0805|B|B|B|
|C46|C50|10uF|16V|SMD 3-4mm|T|T|T|
|C47|C36|200pF||0805|-|B|-|
|C48|C52|100uF|6.3V|THT 5mm pitch|T|T|T|
|C49|C19|22nF||0805|B|B|B|
|C50|C20|22nF||0805|B|B|B|
|C51|C12|22nF||0805|B|B|B|
|C52|C8|22uF||0805|-|B|B|
|C53|C44|10uF|16V|SMD 3-4mm|-|T|T|
|C54|C21|100pF||0805|-|-|B|
|C55|C33|33pF||0805|-|-|B|
|C56|C34|82pF||0805|-|-|B|
|C57|C30|n/u||0805|-|-|-|
|C58|C53|n/u||0805|-|-|-|
| - |C29|50pF||0805|-|-|B|
| - |C31|133pF||0805|-|-|B|
| - |C35|60pF||0805|-|-|B|
| - |C37|200pF||0805|-|-|B|
| - |C38|133pF||0805|-|-|B|
| - |C39|100pF||0805|-|-|B|
| - |C40|200pF||0805|-|-|B|
| - |C54|n/u||0805|-|-|-|
| - |C55|n/u||0805|-|-|-|
| - |C56|n/u||0805|-|-|-|
| - |C57|n/u||0805|-|-|-|
| - |C58|n/u||0805|-|-|-|
|CX1|-|51pF||THT axial\*|B|-|-|
|R1 |R1|4.7K||0805|B|B|B|
|R2 |R2|4.7K||0805|B|B|B|
|R3 |R5|2.2K||0805|B|B|B|
|R4 |R7|360||0805|B|B|B|
|R5 |R6|160||0805|B|B|B|
|R6 |R3|4.7K||0805|B|B|B|
|R7 |R4|4.7K||0805|B|B|B|
| - |R8-12|0||0805|-|-|See note\*\*|

\* `CX1` (to give it a name) was mounted on the bottom of `837-8015` boards
from the factory, between pins 2 and 38 of `IC4`. You may like to replicate
this the same way, or you may use the extra 0805 footprint provided for this
purpose. You may even want to live dangerously and leave it off.

\*\* These 0-ohm resistors are used to configure the board depending on the
MCE revision, etc.:

* `R8` and `R9`: these have the pads shorted on the board so no resistor
  need be fitted.
* `R10`: Fitted only for MCE3, in which case IC17 is unpopulated.
* `R11` and `R12`: these affect how `/CLWE` is passed to the PCM chip. With
  `R11` installed, this is passed directly like on the `837-8015` board with
  the `315-5476` (no "A" suffix) PCM chip. With `R12` installed the signal
  is passed through an XOR gate like on the `837-8015-01` board with the
  `315-5476A` (with "A" suffix) installed. This may be useful if you are
  mixing and matching parts from different boards but the best course of
  action is to note which of these resistors/jumpers is installed on the
  original board you are replacing. In any case, DO NOT install both `R11`
  and `R12` as this will likely damage `IC12`.


## Modifications

Whilst the PCB layouts are meant to be close replicas of the original, some
minor practical modifications have been made.

### 837-8015 (Japanese "Rev 0")
This revision came from the factory with a capacitor installed directly to the
underside of `IC4` (the ROM). For your convenience a dedicated SMD footprint
has been added so this can be mounted more neatly.

Two bare copper areas have been left near the edge of the board for fitting the
additional ground wires originally connected on the underside to pin 5 of `IC6`
and `IC8`. These wires were originally required as these chips and `IC7` are
otherwise grounded only by means of one thin trace. As the reproduction board
has an internal ground plane, these wires should no longer be required.


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


## Additional Resources

If you require the SEGA font for producing a logo on the board, you may
consider [this one](http://actselect.chips.jp/fonts/11.htm). Note that the
author specifies that this is allowed for personal, non-commercial use only
and may not be redistributed.


## Thanks

  * Simon "Aergan" Lock ([@Aergan](https://github.com/Aergan)) for your
    insights, advice, support and expert testing of the first boards.

  * Chrissy ([@chris-jh](https://github.com/chris-jh)) for the connect board
    reproduction project, support and testing.

  * Zaxour, @PointerFunction and the rest of the Board Folk for their support
    and general coolness.


## Legal

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
