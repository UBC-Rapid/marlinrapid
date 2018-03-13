# cl0ned i3 MK1
*The firmware used to run UBC Rapid's Prusa i3 MK1 iterations on the arduino + Ramps 1.4 setups we use*

## Uploading the firmware

### Setting up the ArduinoIDE
1. Download the Ardunio IDE from [here](https://www.arduino.cc/en/Main/Software)  
   - Just use the most updated version and you'll be fine.
2. Import the u8glib library
   - The u8glib library is needed to use the full graphics display that Rapid seems to have lying around in abundance.
   - The u8glib zip folder should be there in this branch.
   - In the arduinoIDE go to Sketch->Include Library->Add .ZIP Library.. then find the zip folder to install the u8glib library
   - (Unnessesary?) Include the library in your configurations.h file right above the (#ifndef CONFIGURATION_H) line with (#include <U8glib.h>)
 3. Make your edits
    - If you reallllllyyyy must you can then change settings or edit files, hopefully you know what you're doing.
 4. Compile and Upload
    - Make sure in "Tools" in Board you are using the (Arduino/Genuino 2560 or Mega 2560) and Processor (ATmega2560 (Mega 2560))
    - Hit the verify checkmark to make sure you haven't broken anything
    - Connect your printer to your laptop and make sure you're on the right port. (Should find it automatically)
    - If you are running other software that communicates with printers, close them otherwise you'll run into errors. (Cura, Pr0nterface, Prusa Updater???)
  5.  Celebrate

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
