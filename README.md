# ThumbsUp! Trackball v5 Omron
A version of v3 with Omron D2FC-7 switches used instead of Kailh Chocs.
PCB is used as button caps.

![Photos](https://github.com/ak66666/ThumbsUp-Trackball-v5-Omron/blob/main/Photos/v4rev1/IMG_20251021_160105760.jpg)


A PCB-based thumb-operated trackball, inspired by Elecom EX-G left hand trackball, Ploopy Nano trackball, and my own ThumbsUp! keyboards.

To be suitable for both left- and right-hand usage (in "portrairt" orientation), and also be finger-operated (in "landscape").
A three-position switch/soldering pad tells the device which mode to use - that will define the rotating direction.

It is a continuation of Trackball v3 - with the Kailh Choc switches replaced with Omron mouse buttons.
 
For MCU nice!nano v2 (and clones) with ZMK-based firmware is used (wired or wireless through Bluetooth or a dongle.)

34 mm ball, same as in Elecom EX-G.
For bearings - uxcell 2.5mm Ceramic Bearing Balls, ZrO2 Zirconium Oxide Ball, again, the same as used to improve my Elecom trackballs.
Bearings to be implanted into PCBs, no 3D-printed ball shroud/holder.


Other pictures in Photos folder.

# Firmware - same as v3

Original version with BT and wired connection:
https://github.com/ak66666/zmk-config-trackball.v3        

Dongle version:
https://github.com/ak66666/zmk-config-trackball.v3.dongle

Dongle version for a combo with ThumbsUp! v9 keyboard:
https://github.com/ak66666/zmk-config-trackball-v3-and-keyboard-v9.dongle


# For sale on Etsy
 
https://www.etsy.com/ca/listing/4390955764

# Assembly Instructions

Similar to v3:
https://thumbsupkeyboards.blogspot.com/2025/09/thumbsup-trackball-v3-assembly-steps.html

The difference is in the switches only.
3D printed switch bases are needed.
Below the switches there are three-point soldering connectors - you need to close two of them on the side where the switch button is.


# Gerber Generation

There is a little trick that needs to be applied to produce silkscreens with overlapping labels.
Normally all the elements on the silkscreen are added up, so the text would be interrupted/covered by the drawing elements.

To work around that limitation - use the generation option "Subtract Soldermask from Silkscreen".
IMPORTANT: Save and preserve the project files, you will be temporarily removing parts of the board design.

Labels which are covered by the silkscreen pattern, they should be moved to the front/back soldering mask layer.
Text needs to be inverted - check "Knockout" box in the label properties.
On the matching front/back silkscreen layer add a rectangle around the label. 
For the design time leave it unfilled - will fill it during Gerber file generation as described below.

![Photos](https://github.com/ak66666/ThumbsUp-Trackball-v3/blob/main/Photos/Silkscreen_Pattern_and_Label_Combination.png)


To generate fabrication files:
- In PCB Editor, for each of the PCB do the following (_do not_ save the file while doing that):
	- Select and delete all other PCBs, leave only one to be generated.
	- For each label on the solder mask layer - locate silkscreen rectangles around that label, modify its property - check "Filled Shape" box.
	  (Those boxes are not filled while designing the board, otherwise they cover all other elements.)
	- Generate the Gerbers (plotting, drilling files) with this:
		- Uncheck  "Subtract Soldermask from Silkscreen" option.
		- Exlude the silkscreens at this point.
	- Generate silkscreen layers with  "Subtract Soldermask from Silkscreen" option checked.
	- Close PCB Editor without saving the file.
	- Re-open PCB Editor and repeat these steps for other boards.
- Verify the genearted files.
