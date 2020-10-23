# Buffered IF tap board for Panadapter / SDR in a Yaesu FT-991/A

## Video: [Here](https://www.youtube.com/watch?v=WfEJoV_u_B8)
## Instructions, tests, pictures and full documentation: Check the [Wiki](https://github.com/rfrht/FT991A-PAT/wiki)

## Yaesu FT-991/A Custom Panoramic Adapter Buffered TAP Board for external SDR / Spectrum Analyser

This project is a remix of OE2DOR's [perfect and neatly crafted](https://raw.githubusercontent.com/Lightning1984/FT991A-PAT/master/Design/FT991-PAT_Installed.jpg) FT-991/A Panadapter board with a high impedance IF tap, in order to disturb to a minimum the radio's IF signal.

This design is compatible with both A and non-A FT-991 rigs.

The final objective is to actually **lodge** a RTL-SDR **inside** a FT-991/A, with no extra cables coming off the radio.

The schematics are in Autodesk Eagle EDA format. Check the Schematic folder.

The [BOM (containing Digikey parts)](Design/bom-ft991-panadapter.csv) and a [few](https://raw.githubusercontent.com/rfrht/FT991A-PAT/master/Design/FT991-PAT_Bottom.jpg) [pictures](https://raw.githubusercontent.com/rfrht/FT991A-PAT/master/Design/FT991-PAT_Top.jpg) are available in Design folder.

This fork adds on-board RF switching control by using a AND gate with two inputs that controls a RF switch: The IF signal is only forwarded to the SDR if both signals (in my project, a SDR GPIO signal and the RX9 signal from radio's Main Unit) are present. Otherwise, the SDR is left isolated to the ground and no signal is tapped from IF (default state). There are also provisions to bypass entirely the high impedance/Amplifier stage via a SDR GPIO (default: off).

The project tracking, evolution and discussion is on QRZ Forum: [A FT-991/A IF tap for Panadapter / RTL-SDR inside the radio](https://forums.qrz.com/index.php?threads/hard-hack-embedding-a-sdr-in-ft-991a-need-rf-designers-review.650840/)

If you are interested in build your own, click [here for Gerber (the PCB layout file for fabrication) files](https://raw.githubusercontent.com/rfrht/FT991A-PAT/master/Design/board-gerbers.zip) and print somewhere else (like [JLCPCB](https://jlcpcb.com/quote), super cheap and $0 shipping on first order).

This project is **also** compatible with the non-A model FT-991. The only difference is that the [FT-991 signal pick-up should be between RF switches Q1088 Pin 5 and Q1102 Pin 5](https://raw.githubusercontent.com/rfrht/FT991A-PAT/master/Design-tap-point.png).

### Notes:
* Board (5 samples) costs $2 in [jlcpcb.com](https://jlcpcb.com/quote).
* The [parts](Design/bom-ft991-panadapter.csv) costs around $24 in Digi-Key.
* IF is wide open, spanning the preselector filter range. With that comes also a problem: Very strong signals might spew images through the spectrum in your SDR. Use the RTL-SDR RX gain to counteract.
* The selectable BPF **now works!!**

### Next steps:
Procure the board
Test

### Changelog:
Click [Here](CHANGELOG.md)
