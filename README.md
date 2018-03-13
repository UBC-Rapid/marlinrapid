<<<<<<< HEAD
# cl0ned i3 MK1

## Enabling autoleveling on your slic3r software (slic3r, Cura, etc...)

### Manual Leveling feature

AFTER you do some bed leveling from the LCD controls, store the values using M500 or the save settings option in the LCD controls.

Be sure to have the following line in your Start G-code, AFTER [ G28; Home ] has been sent.  
M420 S1 ;Enables Bed leveling feature

You can also use G29 to checkout your mesh leveling points.

Use M206 Zxxx with your offest value xxx as either + (shift virtual plane upwards towards nozzle) or - (Shift virtual plane downwards away from nozzle).

### Start G-Code (Replace whatever you have in your start G-code with the following.)
G21 ; set units to millimeters  
G90 ; use absolute positioning  
M82 ; absolute extrusion mode  
G28 W ; home all without mesh bed level  
G80 ; mesh bed leveling  
M420 S1 ;Enables bed leveling feature  
M104 S{material_print_temperature} ; set extruder temp  
M140 S{material_bed_temperature} ; set bed temp  
M190 S{material_bed_temperature} ; wait for bed temp  
M109 S{material_print_temperature} ; wait for extruder temp  
G92 E0.0 ; reset extruder distance position  
G1 Y-3.0 F1000.0 ; go outside print area  
G1 X60.0 E9.0 F1000.0 ; intro line  
G1 X100.0 E21.5 F1000.0 ; intro line  
G92 E0.0 ; reset extruder distance position  
=======
# Marlin 3D Printer Firmware

[![Build Status](https://travis-ci.org/MarlinFirmware/Marlin.svg?branch=RCBugFix)](https://travis-ci.org/MarlinFirmware/Marlin)
[![Coverity Scan Build Status](https://scan.coverity.com/projects/2224/badge.svg)](https://scan.coverity.com/projects/2224)

<img align="top" width=175 src="buildroot/share/pixmaps/logo/marlin-250.png" />

Additional documentation can be found at the [Marlin Home Page](http://marlinfw.org/).
Please test this firmware and let us know if it misbehaves in any way. Volunteers are standing by!

## Bugfix Branch

__Not for production use. Use with caution!__

This branch is used to accumulate patches to the latest 1.1.x release version. Periodically this branch will form the basis for the next minor 1.1.x release.

Download earlier versions of Marlin on the [Releases page](https://github.com/MarlinFirmware/Marlin/releases). (The latest tagged release of Marlin is version 1.1.7.)

## Recent Changes
- Internally always use native machine space
- Initial UBL LCD Menu
- New optimized G-code parser singleton
- Initial `M3`/`M4`/`M5` Spindle and Laser support
- Added `M421 Q` to offset a mesh point
- Refinements to `G26` and `G33`
- Added `M80 S` to query the power state
- "Cancel Print" now shuts off heaters
- Added `EXTRAPOLATE_BEYOND_GRID` option for mesh-based leveling

## Submitting Patches

Proposed patches should be submitted as a Pull Request against this branch ([bugfix-1.1.x](https://github.com/MarlinFirmware/Marlin/tree/bugfix-1.1.x)).

- This branch is for fixing bugs and integrating any new features for the duration of the Marlin 1.1.x life-cycle. We've opted for a simplified branch structure while we work on the maintainability and encapsulation of code modules. Version 2.0 and beyond should improve on separation of bug fixes and cutting-edge development.
- Follow the proper coding style to gain points with the maintainers. See our [Coding Standards](http://marlinfw.org/docs/development/coding_standards.html) page for more information.
- Please submit your questions and concerns to the [Issue Queue](https://github.com/MarlinFirmware/Marlin/issues). The "naive" question is often the one we forget to ask.

### [RepRap.org Wiki Page](http://reprap.org/wiki/Marlin)

## Credits

The current Marlin dev team consists of:
 - Roxanne Neufeld [[@Roxy-3D](https://github.com/Roxy-3D)]
 - Scott Lahteine [[@thinkyhead](https://github.com/thinkyhead)]
 - Bob Kuhn [[@Bob-the-Kuhn](https://github.com/Bob-the-Kuhn)]

Notable contributors include:
 - Alberto Cotronei [[@MagoKimbra](https://github.com/MagoKimbra)]
 - Andreas Hardtung [[@AnHardt](https://github.com/AnHardt)]
 - Bernhard Kubicek [[@bkubicek](https://github.com/bkubicek)]
 - Bob Cousins [[@bobc](https://github.com/bobc)]
 - Chris Palmer [[@nophead](https://github.com/nophead)]
 - David Braam [[@daid](https://github.com/daid)]
 - Edward Patel [[@epatel](https://github.com/epatel)]
 - Erik van der Zalm [[@ErikZalm](https://github.com/ErikZalm)]
 - Ernesto Martinez [[@emartinez167](https://github.com/emartinez167)]
 - F. Malpartida [[@fmalpartida](https://github.com/fmalpartida)]
 - Jochen Groppe [[@CONSULitAS](https://github.com/CONSULitAS)]
 - João Brazio [[@jbrazio](https://github.com/jbrazio)]
 - Kai [[@Kaibob2](https://github.com/Kaibob2)]
 - Luc Van Daele[[@LVD-AC](https://github.com/LVD-AC)]
 - Nico Tonnhofer [[@Wurstnase](https://github.com/Wurstnase)]
 - Petr Zahradnik [[@clexpert](https://github.com/clexpert)]
 - Thomas Moore [[@tcm0116](https://github.com/tcm0116)]
 - [[@alexxy](https://github.com/alexxy)]
 - [[@android444](https://github.com/android444)]
 - [[@benlye](https://github.com/benlye)]
 - [[@bgort](https://github.com/bgort)]
 - [[@Grogyan](https://github.com/Grogyan)]
 - [[@marcio-ao](https://github.com/marcio-ao)]
 - [[@maverikou](https://github.com/maverikou)]
 - [[@oysteinkrog](https://github.com/oysteinkrog)]
 - [[@p3p](https://github.com/p3p)]
 - [[@paclema](https://github.com/paclema)]
 - [[@paulusjacobus](https://github.com/paulusjacobus)]
 - [[@psavva](https://github.com/psavva)]
 - [[@Tannoo](https://github.com/Tannoo)]
 - [[@teemuatlut](https://github.com/teemuatlut)]
 - ...and many others

## License

Marlin is published under the [GPL license](/LICENSE) because we believe in open development. The GPL comes with both rights and obligations. Whether you use Marlin firmware as the driver for your open or closed-source product, you must keep Marlin open, and you must provide your compatible Marlin source code to end users upon request. The most straightforward way to comply with the Marlin license is to make a fork of Marlin on Github, perform your modifications, and direct users to your modified fork.

While we can't prevent the use of this code in products (3D printers, CNC, etc.) that are closed source or crippled by a patent, we would prefer that you choose another firmware or, better yet, make your own.
>>>>>>> 4dad8628ff7e7922783207532c91b3688bc7fa99
