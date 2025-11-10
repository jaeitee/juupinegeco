# juupinegeco
Remove wait time when using Juupine Geco build plates on Bambu Lab printers.


I'll clean this up later... for now....

Find: M190 S[bed_temperature_initial_layer_single] ;wait for bed temp 

And replace with...

;===== GECO - Ignore Bed Temperature ==================== 
{if curr_bed_type!="Bambu Cool Plate"} M190 S[bed_temperature_initial_layer_single] ;wait for bed temp
{endif}

Now if you select 'Cool Plate' as your printing plate it will no longer pause and wait to drop to 1c.

As the print bed is textured, find... 

;===== for Bambu Cool Plate SuperTack Plate , lower the nozzle as the nozzle was touching topmost of the texture when homing ==
;curr_bed_type={curr_bed_type}
{if curr_bed_type=="Bambu Cool Plate SuperTack"}
G29.1 Z{-0.04} ; for Bambu Cool Plate SuperTack
{endif}

and add directly below....

;===== for Geco Cool Plate , lower the nozzle as the nozzle was touching topmost of the texture when homing ==
;curr_bed_type={curr_bed_type}
{if curr_bed_type=="Bambu Cool Plate"}
G29.1 Z{-0.04} ; for Geco Cool Plate
{endif}

IF you're still having adhesion issues you can change the -0.04 value to -0.05 instead.
