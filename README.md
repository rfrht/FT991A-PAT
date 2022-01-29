# This is the REV. R *FULL VERSION* Branch.

# Buffered IF tap board for Panadapter / SDR in a Yaesu FT-991/A

## Instructions, tests, pictures and full documentation: Check the [Wiki](https://github.com/rfrht/FT991A-PAT/wiki)

## Yaesu FT-991/A Custom Panoramic Adapter Buffered TAP Board for external SDR / Spectrum Analyser

This project is a remix of OE2DOR's [perfect and neatly crafted](https://raw.githubusercontent.com/Lightning1984/FT991A-PAT/PAT-Light/Design/FT991-PAT_Installed.jpg) FT-991/A Panadapter board with a high impedance IF tap, in order to disturb to a [minimum](https://youtu.be/yeTeMTJRBIg) the radio sensitivity.

This design is compatible with both A and non-A FT-991 transceivers.

The objective is to actually **lodge** a RTL-SDR **inside** a FT-991/A, with no extra cables coming off the radio.

The schematics are in Autodesk Eagle EDA format. Check the [Schematic](Schematic) folder. The [Design](Design) folder contains some ancillary material.

The project genesis and some discussion are logged on QRZ Forum: [A FT-991/A IF tap for Panadapter / RTL-SDR inside the radio](https://forums.qrz.com/index.php?threads/hard-hack-embedding-a-sdr-in-ft-991a-need-rf-designers-review.650840/). If you need to ask questions, either file a Github Issue (preferred) or use the QRZ Forum.

If you are interested in build your own, [click here to download the Gerber](Design/board-gerbers.zip) and order in your favourite PCB Fab (like [JLCPCB](https://jlcpcb.com/quote), super cheap, good quality and $0 shipping on first order). **Ensure to read the [Wiki](https://github.com/rfrht/FT991A-PAT/wiki)**.

### Notes:

* The board (5 samples) costed $2 in [jlcpcb.com](https://jlcpcb.com/quote).
* The [parts](Design/bom-ft991-panadapter.csv) costs around $15 in Digi-Key.
* The IF signal is wide open, spanning the radio's [preselector filter range](/rfrht/FT991A-PAT/wiki/appendix-preselector-rx-stage-characteristics). With that comes also a problem: Very strong signals in passband might spew images through the spectrum in your SDR. Use the RTL-SDR RX gain to counteract.

### Changelog:
Check [Here](CHANGELOG.md)
