# Buffered IF tap board for Panadapter / SDR in a Yaesu FT-991/FT-991A
## Yaesu FT-991/FT-991A Custom Panoramic Adapter Buffered TAP Board for external SDR / Spectrum Analyser

This project is a remix of OE2DOR's [perfect and neatly crafted](https://raw.githubusercontent.com/Lightning1984/FT991A-PAT/master/Design/FT991-PAT_Installed.jpg) FT-991/FT-991A Panadapter board.

The final objective is to actually **embed** a RTL-SDR **inside** a FT-991/FT-991A, without drilling holes, external cables, connectors or whatsoever: The FT-991/FT-991A sports a USB hub (which feeds the sound card and the CAT interface). By replacing the existing 2-port USB hub chip with a 4-port variant (same SMD footprint and compatible pinout), the SDR will be installed in the radio, and it will be exposed to the computer via the existing USB port, conveniently routed through the radio's USB hub. So, plug the radio's USB port and the computer will see three devices: the virtual sound card, the CAT port **and** the SDR.

This fork adds on-board latch control, by using a AND gate with two inputs that controls a RF switch: The IF signal is only connected to the SDR if both signals (on my project, a SDR GPIO signal and the RX9 signal from radio's Main Unit) are present. Otherwise, the SDR is left isolated to the ground and no signal is tapped.

The schematics are in Autodesk Eagle EDA format. Check the Schematic folder.
The [BOM (containing Digikey parts)](Design/parts-digikey.md) and a [few](https://raw.githubusercontent.com/rfrht/FT991A-PAT/master/Design/FT-991A_PAT-Back.png) [pictures](https://raw.githubusercontent.com/rfrht/FT991A-PAT/master/Design/FT-991A_PAT-front.png) are available in Design folder.

The project tracking, evolution and discussion is on QRZ Forum: [A FT-991/FT-991A IF tap for Panadapter / RTL-SDR inside the radio](https://forums.qrz.com/index.php?threads/hard-hack-embedding-a-sdr-in-FT-991/FT-991A-need-rf-designers-review.650840/)

Board reprints in [OSHPark](https://oshpark.com/shared_projects/RCpC2dtm). Click [here for Gerber files](https://raw.githubusercontent.com/rfrht/FT991A-PAT/master/Design/board-gerbers.zip) and print somewhere else (like [JLCPCB](https://jlcpcb.com/quote), way cheaper).

This project is **also** compatible with the non-A model FT-991. The only difference is that the [FT-991 signal pick-up should be between RF switches Q1088 Pin 5 and Q1102 Pin 5](https://raw.githubusercontent.com/rfrht/FT991A-PAT/master/Design-tap-point.png).

### Current state:
* Board ordered, printed, shipped, delivered!
* Components as well!
* Did a few tests in FT-991/FT-991A - See content in https://rf01.co:8443/q/pat-991a/

### Next steps:

* Book lab time and have Yvo to solder the components and replace the USB hub from Main Unit
* Run the board through a VNA and check VSWR + Gain
* ~~Create a new Revision J board (see notes, below)~~
* Planning a Revision L, containing a RF Switch containing a bypass, moving the signal straight off the tap to the SDR_OUT port

### Notes:

* Board (5 samples) costed $2 in [jlcpcb.com](https://jlcpcb.com/quote).
* The parts costed $26 (though I bought the wrong SMA connector, how on earth is there a male pin in a female jack)
* Until revision I, the AND gate took the SCPON signal. However, the SCPON signal is not the best option to the AND gate, along the RTL's GPIO port. SCPON is only HIGH when the Scope is being displayed. If you go to Menu or Setup, the SCPON goes down. Ah, if in Scope mode, it stays HIGH during TX as well (though I found no artifacts during 50W TX, I think the line is grounded somewhere else). For now since I have printed the PCB and etc, I will just bridge the GPIO port to both ports in the board. A next board revision will use RX9 signal plus a voltage divider (to bring the voltage down to a safe voltage to the AND gate), so the AND gate will actuate the RF switch accordingly.
* IF signal is incredibly strong (centered in 68.450 MHz).
* IF is wide open, spanning the whole bandpass filter (with that comes a few problems: Strong signals might spew images through the spectrum in your SDR)
* ~~Seems that the footprints are correct~~ - No, they were not. BOM specifies 1206 and board had 0805. Had to issue Rev. K.
* Definitely, the USB footprint was designed correctly, yay \o/
* The SDR is a bit large for the radio, and I'm having a hard time finding a suitable place to lodge it (see picture 08 in my website, at 'Current State')
* I'm pending availability of the Tech for soldering the components and swapping the Main Unit IC


### Changelog: (PY2RAF)

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
* Added a few vias in voltage regulators' large ground pads 
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
* Added provision for two external inputs for latching control (actuating on a RF switch), isolating the SDR receiver when the two inputs are not in HIGH state. This is a bit of overkill in FT-991/FT-991A, but I want to be able to control the IF tap by software and be able to unplug it completely when not in use, without having to open the radio ;-)

### History (OE2DOR)

05/11/2018
 - Board Layout changed to fit neatly inside FT-991/FT-991A
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
 - Up and running on a Yaesu FT-991/FT-991A

12/10/2017
 - Revised component values to values that you can actually obtain. Added digikey parts list.

10/22/2017
 - Second revision testing complete and satisfactory. Up and running on a Yaesu FT-450D

08/30/2017
 - Schematic revised to fix capacitor placement error in original schematic. New boards sent out for fabrication and testing will be done when they get back.
