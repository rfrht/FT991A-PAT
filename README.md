# Buffered IF tap board for Panadapter / SDR in a Yaesu FT-991/A

## Video: [Here](https://www.youtube.com/watch?v=WfEJoV_u_B8)
## New Branch, Light Edition: Simpler design, basics only, $15 total BOM - [Here](https://github.com/rfrht/FT991A-PAT/tree/PAT-Light)
## Instructions, tests, pictures and full documentation: Check the [Wiki](https://github.com/rfrht/FT991A-PAT/wiki)

## Yaesu FT-991/A Custom Panoramic Adapter Buffered TAP Board for external SDR / Spectrum Analyser

This project is a remix of OE2DOR's [perfect and neatly crafted](https://raw.githubusercontent.com/Lightning1984/FT991A-PAT/master/Design/FT991-PAT_Installed.jpg) FT-991/A Panadapter board with a high impedance IF tap, in order to disturb to a minimum the radio's IF signal.

This design is compatible with both A and non-A FT-991 rigs.

The final objective is to actually **lodge** a RTL-SDR **inside** a FT-991/A, with no extra cables coming off the radio.

This fork adds on-board RF switching control by using a AND gate with two inputs that controls a RF switch: The IF signal is only forwarded to the SDR if both signals (in my project, a SDR GPIO signal and the RX9 signal from radio's Main Unit) are present. Otherwise, the SDR is left isolated to the ground and no signal is tapped from IF (default state). There are also provisions to bypass entirely the high impedance/Amplifier stage via a SDR GPIO (default: off).

The schematics are in Autodesk Eagle EDA format. Check the Schematic folder.

The [BOM (containing Digikey parts)](Design/bom-ft991-panadapter.csv) and a [few](https://raw.githubusercontent.com/rfrht/FT991A-PAT/master/Design/FT991-PAT_Bottom.jpg) [pictures](https://raw.githubusercontent.com/rfrht/FT991A-PAT/master/Design/FT991-PAT_Top.jpg) are available in Design folder.

The project tracking, evolution and discussion is on QRZ Forum: [A FT-991/A IF tap for Panadapter / RTL-SDR inside the radio](https://forums.qrz.com/index.php?threads/hard-hack-embedding-a-sdr-in-ft-991a-need-rf-designers-review.650840/)

If you are interested in build your own, click [here for Gerber (the PCB layout file for fabrication) files](https://raw.githubusercontent.com/rfrht/FT991A-PAT/master/Design/board-gerbers.zip) and print somewhere else (like [JLCPCB](https://jlcpcb.com/quote), super cheap and $0 shipping on first order).

This project is **also** compatible with the non-A model FT-991. The only difference is that the [FT-991 signal pick-up should be between RF switches Q1088 Pin 5 and Q1102 Pin 5](https://raw.githubusercontent.com/rfrht/FT991A-PAT/master/Design-tap-point.png).

### Notes:

* Board (5 samples) costed $2 in [jlcpcb.com](https://jlcpcb.com/quote).
* The [parts](Design/bom-ft991-panadapter.csv) costs around $25 in Digi-Key.
* IF is wide open, spanning the preselector filter range. With that comes also a problem: Very strong signals might spew images through the spectrum in your SDR. Use the RTL-SDR RX gain to counteract.
* The selectable BPF did not work, resulting in signal loss. Fortunately, it is off by default so it did not impact directly the panadapter.

### Next steps:
* Procure the board and components
* Test

### Changelog: (PY2RAF)

02/Nov/2019 - Revision O
* Board redesign
* Moved everything to the bottom side of the board, except for a RF switch and SDR/Scope unit ports
* Redesigned BPF (thanks to [SM0AOM](https://forums.qrz.com/index.php?threads/filter-design-help.671664/))
* Changed panadapter default state from disabled to enabled
* Changed RF front-end switch to use the TX9 signal OR SDR to disable it
* Added a PTC fuse
* Choosed a simpler (and cheaper) 9V regulator

22/Jun/2019 - Revision N
* Removed the 5V regulator
* Removed the USB provisions
* Removed the G4HUP LPF. Reasoning: Found it of no use, since it cuts the signal 24 MHz above the IF center frequency. Replaced with a selectable 3-MHz wide 69.450 MHz BPF.
* Moved regulators to the top side of the board (to take advantage of heat dissipation)
* Moved the SDR Out port to the top of the board
* Added a large uncovered ground pad
* Tried to group the signals as much as possible and moved everything to the top of the board
* And thus, reduced significantly the BOM (35 to 25 different parts)

29/May/2019 - Revision M
EXPERIMENTAL.  In this revision:
* Got rid of the USB receptacle - Too much space in a tight radio
* Moved all GPIO pads to the upper board side
* Added a few missing Pin 1 references
* Renamed voltage regulators to somewhat shorter name
* Small re-routing - 9V regulator was entangled with capacitor

24/May/2019 - Revision L
EXPERIMENTAL.  In this revision:
* Added the ability to bypass entirely the amplifier and filters
  - Selectable by RF switch (default: off)
* Added a 3-pole Chebyshev Band-pass Filter centered at 69.450 MHz, 3 MHz
  wide
  - Selectable by RF switch (default: off)
* Revamped the Block Diagram
* Added the BPF LT-SPICE simulation
* Updated README, BOM, Gerbers and Pictures
* And yes, board is getting somewhat cluttered.

19/May/2019 - Revision K
* Changed footprints: BOM specifies 1206, project had 0805
  - Unified everything Resistors and Capacitors in 1206
  - Inductors are 0805
* A few routing enhancements
* Recalculated the component indexes
* Updated BOM to reflect the new component index
  - And also found a unaccounted resistor, whoops.
  - Reviewed the entire BOM and circuits. Now everything should be fine.

18/May/2019 - Revision J
* Changed SCPON signal to RX9
  - Added a Voltage Divider
* Changed the SMA-to-U.FL cable
* Added a few vias in large ground pads for voltage regulators
* Moved USB port a bit back in PCB

07/Apr/2019 - Revision I
* Created USB interconnection with the SDR
* Proper power management: Three voltage regulators in the board (9V, 5V, 3.3V)
* Power is only enabled with signaling coming from USB hub; otherwise, board quiesce
* Updated BOM

29/Mar/2019 - Revision H
* Revised routes in Cheb Filter - Made the tracks fatter and straighter
* Repositioned Q2 for better signal routing
* Better unit spelling in silk screen for resistors
* Flipped IF/SCP ports
* A few routing changes.

27/Mar/2019 - Revision G
* Removed a lingering DC blocker capacitor in filter in after RF switch.
* Added chokes in DC IN lines (3.3V and 5V) (yet another Gordon trick)

27/Mar/2019 - Revision F
* Added 1 nF capacitors in RF lines in PE4529 (except RF2, goes with a 470 pF to GND)
* Got rid of the VCC via which was crossing the RF line (argh)
* Finally got the courage to change a bit the board layout and escape from the thin strip that I was working previously.
* And another THANK YOU to Gordon AD5GG for his invaluable feedback

25/Mar/2019 - Revision E
* Changed the switch from a analog one (was a SN74LVC1G66) to a RF one (now: PE4259) (thanks to Gordon Hudson AD5GG)
* Now using 3.3V (because of PE4529)
* The switch default state now grounds the SDR
* Updated the list of contributors in PCB Silk Screen.

20/Mar/2019 - Revision D
* Moved to [OE2DOR](https://github.com/Lightning1984) **amazing** board design
* Added provision for two external inputs for latching control (actuating on a RF switch), isolating the SDR receiver when the two inputs are not in HIGH state. This is a bit of overkill in FT-991/A, but I want to be able to control the IF tap by software and be able to unplug it completely when not in use, without having to open the radio ;-)

### History (OE2DOR)

05/11/2018
 - Board Layout changed to fit neatly inside FT-991/A
 - Connection to IF using existing U.FL jumper cable 
 - Connection to FT991A SCP-UNIT using additional short U.FL jumper cable
 - Connection to SDR/SpectrumAnalyser using new U.FL to SMA cable
 - Mounting using M3/10mm PCB Spacer soldered to head of existing PCB mounting screw (since PCB mounting screw has no metric thread)
 - Fixation using M3 Plastic nut & screw sticking into tuning hole of shielding box
 - All but one resitor (1206) changed to 0805 to allow for smaller PCB layout

History (G4HUP/W3AXL)
Updated G4HUP / W3AXL panadapter tap
Simple revision to the G4HUP high-impedance IF tap with specific components and updated filters.

12/14/2017
 - Revised parts.md to add quantity of parts needed.

12/10/2017
 - Up and running on a Yaesu FT-991/A

12/10/2017
 - Revised component values to values that you can actually obtain. Added digikey parts list.

10/22/2017
 - Second revision testing complete and satisfactory. Up and running on a Yaesu FT-450D

08/30/2017
 - Schematic revised to fix capacitor placement error in original schematic. New boards sent out for fabrication and testing will be done when they get back.
