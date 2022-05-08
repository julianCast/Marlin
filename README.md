# Marlin 3D Printer Firmware (Duveral Mod)
## What's for this configuration:
This is a modifed Marlin version for the following configuration:
- Wanhao i3
- SKR 1.4 Turbo
- 4x TMC Drivers with Sensorless homing enabled.
- Dual Drive Extruder Volcano from Trianglelab. [+Info](https://es.aliexpress.com/item/32946674846.html?gatewayAdapt=glo2esp)
- BLTouch 2.0

## Start G-Code
```gcode
M117 Getting the bed up to temp!
M140 S{material_bed_temperature_layer_0}   ; Set Heat Bed temperature
M190 S{material_bed_temperature_layer_0}   ; Wait for Heat Bed temperature
M117 Pre-heating the extruder!
M104 S160                                  ; start warming extruder to 160
G28                                        ; Home all axes
M117 Auto bed-level GO!
G29                                        ; Auto bed-level (BL-Touch)
G92 E0                                     ; Reset Extruder
M117 Getting the extruder up to temp!
M104 S{material_print_temperature_layer_0} ; Set Extruder temperature
M109 S{material_print_temperature_layer_0} ; Wait for Extruder temperature
G1 Z1.0 F3000                              ; move z up little to prevent scratching of surface
G1 X0.1 Y20 Z0.3 F5000.0                   ; move to start-line position
M117 LET THE PURGE BEGIN!
G1 X0.1 Y190.0 Z0.3 F1500.0 E15            ; draw 1st line
G1 X0.4 Y190.0 Z0.3 F5000.0                ; move to side a little
G1 X0.4 Y20 Z0.3 F1500.0 E30               ; draw 2nd line
G92 E0                                     ; reset extruder
G1 Z1.0 F3000                              ; move z up little to prevent scratching of surface
M117 Autobots! Roll Out!
; End of custom start GCode
```
## After flashing:
1. Reset configs with new config
```gcode
M502 ;Reset all configurable settings to their factory defaults.
M500 ;Reset settings in EEPROM
```

2. Calibrate BLTouch Probe z-offset
```gcode
G28         ;home
M851 Z0     ;reset current z offset
M500        ;store settings
M501        ;set eprom as active param
M503        ;get current settings
G28 Z0      ;home z
G1 F60 Z0   ;move nozzle to 0 z
M211 S0     ;off soft endstops

;Slide paper while turning the wheel until is right and write down Z axis number from the LCD + thickness paper

M851 Z X.XX ;set value from last comment Ex; M851 Z-0.88
M211 S1     ;on soft endstops
M500, M501, M503
G28
G1 F60 Z0   ;check is correct
```
:tv: [Watch Video with instructions](https://www.youtube.com/watch?v=y_1Kg45APko)

