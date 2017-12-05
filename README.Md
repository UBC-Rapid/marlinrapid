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
