# Buffered IF tap board for Panadapter / SDR in a Yaesu FT-991/A

## Instructions, tests, pictures and full documentation: Check the [Wiki](https://github.com/rfrht/FT991A-PAT/wiki)

## Yaesu FT-991/A Custom Panoramic Adapter Buffered TAP Board for external SDR / Spectrum Analyser

This project is a remix of OE2DOR's [perfect and neatly crafted](https://raw.githubusercontent.com/Lightning1984/FT991A-PAT/PAT-Light/Design/FT991-PAT_Installed.jpg) FT-991/A Panadapter board with a high impedance IF tap, in order to disturb to a minimum the radio's IF signal.

This design is compatible with both A and non-A FT-991 rigs.

The schematics are in Autodesk Eagle EDA format. Check the [Schematic](Schematic) folder.

The objective is to actually **lodge** a RTL-SDR **inside** a FT-991/A, with no extra cables coming off the radio.

The [BOM (containing Digikey parts)](Design/bom-ft991-panadapter.csv) and a [few](https://raw.githubusercontent.com/rfrht/FT991A-PAT/PAT-Light/Design/FT991-PAT_Bottom.jpg) [pictures](https://raw.githubusercontent.com/rfrht/FT991A-PAT/PAT-Light/Design/FT991-PAT_Top.jpg) are available in Design folder.

The project tracking, evolution and discussion is on QRZ Forum: [A FT-991/A IF tap for Panadapter / RTL-SDR inside the radio](https://forums.qrz.com/index.php?threads/hard-hack-embedding-a-sdr-in-ft-991a-need-rf-designers-review.650840/)

If you are interested in build your own, [click here to download the Gerber](https://raw.githubusercontent.com/rfrht/FT991A-PAT/PAT-Light/Design/board-gerbers.zip) and order in your favourite PCB Fab (like [JLCPCB](https://jlcpcb.com/quote), super cheap, good quality and $0 shipping on first order).

This project is **also** compatible with the non-A model FT-991. The only difference is that the [FT-991 signal pick-up should be between RF switches Q1088 Pin 5 and Q1102 Pin 5](https://github.com/rfrht/FT991A-PAT/wiki/installation#ft-991-if).

### Notes:
* Board (5 samples) costed $2 in [jlcpcb.com](https://jlcpcb.com/quote).
* The [parts](Design/bom-ft991-panadapter.csv) costs around $15 in Digi-Key.
* IF is wide open, spanning the preselector filter range. With that comes also a problem: Very strong signals might spew images through the spectrum in your SDR. Use the RTL-SDR RX gain to counteract.

### Changelog:
Click [Here](CHANGELOG.md)
