# Turtleblobifier

All hardwork has been done by Dendrowen for this mod + code.

This can be found here: https://github.com/Dendrowen/Blobifier

I have since taken the code to made it compatable with the AFC for box turtle  as vanila Blobifier is desighed to work with HappyHare.


## Instructions:
1. Clone this project into your printer config dir:
```git clone https://github.com/ImSundee/Turtleblobifier ~/printer_data/config/blobifier```

2. Inside your printer.cfg add the following include:
```[include blobifier/blobifier.cfg]```

3. Tell AFC about the new routines in the AFC/AFC.cfg file:
Replace with the following:
```
park_cmd: BLOBIFIER_PARK
poop_cmd: BLOBIFIER
```
4. Ensure the following is disabled in AFC/AFC.cfg:
```
kick: False
wipe: False
form_tip: False 
```
 * Cut should be hanled by AFC.
5. Setup Blobifier as normal setting the correct variables  in blobifier/blobifier_hw.cfg and blobifier/blobifier.cfg - they come Preset for my printer so becareful.  
