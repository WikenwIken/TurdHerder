# Turd Herder
## _The Porcelain Standard for 3D Printer Waste Management_

![INST](https://github.com/WikenwIken/TurdHerder/blob/main/Images/INST.png)

The Turd Herder is a dookie dispoasl system for 3D printers with toolheads that have limited to no travel past the edges of the print bed.  The bowl extends over the edge of the print bed, receives the "payload," retracts and whisks it off to a tank in the depths below.  

Turd Herder was designed for use with the Voron Trident / Box Turtle AMS combo running Klipper firmware. The macros are designed to integrate with the AFC Macros (included with the Box Turtle system).
The motion system was inspired by [Dendrowen's Blobifier], the mounting system incorporates whole, and modified, parts from [Armored Turtle's AT Brush]  and the macros are modified versions of [ImSundee's Turtleblobifier].


## Features

- Can be used with any toolhead / probe combo as there aren't any negative Z moves
- A modified G28 allows for safe Z homing 
- Easy to print parts, no supports required!
- Plugs into a BL Touch Port for easy wiring
- Optional brush attachment creates an all-in-one solution

## Required Tools
- Sodering Iron
- Crimping Tool
- Wire Stripper
- Allen Wrenches / Hex Drivers (1.5, 2, 2.5 and 3 mm)
- Small Phillips Screw Driver

## BOM

| Part | QTY | 
| ------ | ------ |
| MG90S Servo (180°) + Hardware Kit | 1 |
| Micro Limit Switch (with lever) | 1 |
| Bambu A1 style brush (37x8) | 1 |
| 6 x 3 mm magnet | 2 |
| 15 x 14 x 1 mm aluminum cube | 1 |
| M5 x 10 mm SHCS | 2 |
| M5 Rollnut | 2 |
| M3 Hex Nut | 2 |
| M3 Washer | 1 |
| M3 x 5 x 4 mm Heat Set Insert | 8 |
| M3 x 6 mm SHCS | 2 | 
| M3 x 8 mm SHCS | 4 |
| M3 x 8 mm BHCS | 1 |
| M3 x 6 mm BHCS | 1 |
| M2 x 8 mm SHCS | 2 |
| 3 mm ID Bowden Tube (optional) | ~4.5 mm |
| JST-XH Male / Female Plugs / Crimps | ~ |
| Zip Ties (optional) | ~ |



*Note:  the M3 Hex Nuts MUST be magnetic.  The sled mechanism will not work properly without a strong-ish magnetic connection.*

*Note: The aluminum cube is just a landing pad for the ___hot___ load and can be made of anything that will take the heat better than bare plastic.  We don't things to stick and get clogged.  I cut up an aluminum plate from an old project box but as long as its <=1mm thick you could fold up some aluminum foil or glue a few layers of soda cans together.  Get creative.*

## Printing

In addition to the STLs in this repositiory, Turd Herder requires the following parts from the [AFC-Accessories] repo.
- [mount_lower.stl]
- [mount_upper.stl]

Parts should be printed in ABS and in accordance to typical Voron specs which may be found [here]. Tolerances for the slots are a little tight and may require some filing to achieve a smooth translation from front to rear.
All parts are oriented correctly and don't require any modifiers from the slicer.  
Supports should not be needed.

# Software Installation
__It is important that the software be installed prior to building the Turd Herder as some of the macros are vital to the installation process.
It is recommended that you make a backup of your __printer.cfg__ and __/AFC/AFC.cfg__ files before proceeding.__
Variables do not need to be tuned at this point, we're just installing the software so the servo macros may be utilized for the install.  We will cover the critical variables later in this document.
1) Clone this project into your printer's config folder ``` git clone https://github.com/WikenwIken/Turdherder ~/printer_data/config/Turdherder```
2) Open /TurdHerder/turd_hw.cfg and set the correct values for `pin:` and `switch_pin:`  
3) Make the following changes to your printer.cfg file:
    - Add ```[include /turdherder/turdherder.cfg]```
    - Comment out ```[safe_z_home]``` and all lines included within
    - Paste the sections `[force_move]` and `[homing_override]` from /turdherder/printurd.cfg into your printer.cfg, adding in any custom features that were previously executed in `[safe_z_home]`
4) Make the adjustments to your /AFC/AFC.cfg file as noted in the second half of the /turdherder/printurd.cfg file

# Assembly

1a) Install 6 M3 heatset inserts according to Figures 1 and 2: 
    - front_arm_base x2
    - servo_base x2
    - chimney x2
    
Fig. 1    
![HSI_01](https://github.com/WikenwIken/TurdHerder/blob/main/Images/HSI_01.png)

Fig. 2
![HSI_02](https://github.com/WikenwIken/TurdHerder/blob/main/Images/HSI_02.png)

1b) Install 2 M3 heatset inserts into __mount_upper__ according to [Step 4] of the AT Brush Manual.
2) Solder one wire to each of the outer pins of the micro limit switch.  Terminate each wire with an appropriate sized crimp / plug.  Orientation in the plug does not matter for the limit switch.
3) MG90S Servos typically ship with dupont connectors.  These will need to be removed and replaced by an appropriate connector.  Consult your main board's pinout diagram before building your new connector.
3) Attach the servo to the __servo_mount__ using the self-tapping screws that came with the servo.  It will only fit one way.
4) Secure the __slide_base__ to the __servo_mount__ using 2 M3x8 SHCS (Figure 3)
5) Plug the servo into the socket on the main board that you defined in /turdherder/turdherder.cfg.  
    - Execute the macro ```SERVO_IN```.  This should rotate the shaft *clockwise*  
    - Execute the macro ```SERVO_OUT```.  This should rotate the shaft *counter-clockwise*
    - If the shaft does not rotate, check your wiring / pin definitions.
    - If the shaft rotates in the wrong direction some modification of the code is likely in order to make it work with your motor.
6) Execute the macro ```SERVO_OUT``` and press the __cog__ onto the shaft as seen in Figure 3.  Add the M3 Washer and M2.5 mounting screw if the __cog__ isn't as rigid as you would prefer.  It should be a pretty tight fit.  Once installed, execute the macros ```SERVO_IN``` and ```SERVO_OUT``` to confirm the cog has full range of travel.  
*Note: The motor should complete its move without physically butting up against the frame.  If the motor doesn't stop freely then some physical / code adjustments should be made.*

Fig. 3

![COG_O](https://github.com/WikenwIken/TurdHerder/blob/main/Images/COG_O.png)

7) Ensure that the cog is in the position indicated in Figure 3 by running the ```SERVO_OUT``` macro and unplug the servo from the main board before moving on.
8) Feed the limit switch up through the rectangular hole in the __servo_mount__ and secure it in place with M2x8 screws.  __Mind the orientation in Figure 4.__

Fig. 4

![SW](https://github.com/WikenwIken/TurdHerder/blob/main/Images/SW_O.png)

9) Insert 1 M3 Hex Nut into the cutout in the __slide_mount__.  If the fit is too tight to press in with your fingers it may be useful to "pull" it into place with an M3 screw from the bottom of the part.  If the fit is too loose use a dab of super glue or insert an M3 screw from below that won't protrude above the nut to hold it in place.  
10) Insert 2 6 x 3 mm magnets into the holes in __sled__.  A dab of super glue may be required to old them in place.  Polarity is not important.  Be careful not to split the layers.    
11) Glue the Aluminum Plate onto the tray of the __sled__.  It should not protrude above the edges of the tray.
12) Click the __sled__ in place on the __slide_mount__ (Figure 5)

Fig. 5

![SL](https://github.com/WikenwIken/TurdHerder/blob/main/Images/SL.png)

13) Attach the __chimney_slot__ to the __chimney__ by inserting an M3x6 SHCS into the hole on the left-rear of the parts. (Figure 6)
14) Insert 1 M3 Hex Nut into the cutout in the __chimney__ and secure it with an M3x6 BHCS through the holes in the middle. (Figure 7)

Fig. 6

![CHHW_1](https://github.com/WikenwIken/TurdHerder/blob/main/Images/CHHW_1.png)

Fig. 7

![CHWW_2](https://github.com/WikenwIken/TurdHerder/blob/main/Images/CHHW_2.png)

15) Drop the chimney assembly into the slots on the __slide_mount__.  The top of the __sled__ inserts into the space in the __chimney__ with the M3 Hex Nut.  Align the slot in the __chimney_slot__ with the hole in the slender end of the __cog__ and screw an M3x8 BHCS into the __cog__ until it is flush with the underside (Figure 8).  It should not protrude from the bottom at all.  This connection should remain fairly loose to allow for free translation of the screw in the slot.  It is easily adjusted later if movement is labored.
_OPTIONAL: A 4mm OD x 3mm ID bowden tube sleeve may be installed around the M3x8 screw to cut down on the threads wearing out the slot_

Fig. 8

![PS](https://github.com/WikenwIken/TurdHerder/blob/main/Images/PS.png)

16) Attach the __brush_arm__ to the __chimney__ using an M3x6 SHCS
17) Attach the silicone brush to the top surface of the __brush_arm__ 
18) Assembly of the Turd Herder is complete.  (Figure 9)

19) Follow these instructions in the [AT Brush Manual] utilizing the modified __front_arm_base__ from this repository:
    - Steps 1 - 8
    - Steps 13 - 15
20) Attach the Turd Herder assembly to the frame mount assembly using 2 M3x8 SHCS

Fig. 9

![INST](https://github.com/WikenwIken/TurdHerder/blob/main/Images/INST.png)

21) Adjust the height of the assembly so that, when the Turd Herder is extended, the nozzle comes in contact with the brush on the Z axis.  (See Step 16 in the [AT Brush Manual])

22) Plug the servo and the limit switch into the main board.  
    - Ensure smooth movement by cycling through the ```SERVO_IN```, ```SERVO_MID``` and ```SERVO_OUT``` macros
    - Ensure the `TH` limit switch reads *detected* in the ```SERVO_IN``` and ```SERVO_MID``` positions.
    - Ensure the ``TH`` limit switch reads *not detected* in the ```SERVO_OUT``` position.
23) Congratulations!  The Turd Herder is fully assembled and the mechanism is working as intended!  Don't release those bowels just yet, there are a few more things to set up.

# Critical Variables
The following are the _must have_ variables that need to be defined for the specific printer that Turd Herder is being installed in.  Each variable is accompanied with a description within the .cfg file.
## turd_hw.cfg 
`[servo TURDHERDER]`
* `pin:`

`[filament_switch_sensor turdherd]`
* `switch_pin:`

## turdherder.cfg
`[gcode_macro TURDHERDER]`
* `variable_purge_spd`
* `variable_thbottom`
* `variable_brush_start_x`
* `variable_brush_start_y`
* `variable_purge_x`
* `variable_purge_y`

## printer.cfg / printurd.cfg
`[homing_override]`
* `home_pos_x`
* `home_pos_y`


   [Dendrowen's Blobifier]: <https://github.com/Dendrowen/Blobifier>
   [ImSundee's Turtleblobifier]: https://github.com/ImSundee/Turtleblobifier
   [Armored Turtle's AT Brush]: https://github.com/ArmoredTurtle/AFC-Accessories/tree/main/AT_Brush
   [AFC-Accessories]: https://github.com/ArmoredTurtle/AFC-Accessories
   [mount_lower.stl]: https://github.com/ArmoredTurtle/AFC-Accessories/blob/main/AT_Brush/STLs/mount_lower.stl
   [mount_upper.stl]: https://github.com/ArmoredTurtle/AFC-Accessories/blob/main/AT_Brush/STLs/mount_upper.stl
   [here]:<https://docs.vorondesign.com/sourcing.html#print-settings>
   [AT Brush Manual]: https://www.armoredturtle.xyz/manual.html?manual=at_brush&step=1
   [Step 4]: https://www.armoredturtle.xyz/manual.html?manual=at_brush&step=4
