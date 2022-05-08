# Marlin 3D Printer Firmware (Duveral Mod)
## What's for this configuration:
This is a modifed Marlin version for the following configuration:
- Wanhao i3
- SKR 1.4 Turbo
- 4x TMC Drivers with Sensorless homing enabled.
- Dual Drive Extruder Volcano from Trianglelab. [+Info](https://es.aliexpress.com/item/32946674846.html?gatewayAdapt=glo2esp)
- BLTouch 2.0
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

