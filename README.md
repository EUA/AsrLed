# AsrLed
AsRock LED Device Driver Script for Linux

## Notices:
This driver just for AsRock Fatal1ty AB350 Gaming-ITX/ac board.
But probably compatible with other AsRock Motherboards that runs AsrRgbLed utility.

## Warning:
If you change RGB values too much, for example using set_static_rgb function in a programatic loop to animate your custom choice, you *PROBABLY* kill your RGB Controller MCU EEPROM, that might lead some errors on RGB LED Lightning...

Motherboards that run AsrPolychromeRGB runs nu51_2.10 firmware does NOT tested with this driver. Probably not compatible, yet.

## Explaination
Register 0x30 controls the device mode. Following RGB codes (if exist) and Speed code (if exist).
Speed is higher with lower values. I don't understand what the Reg 0x31 & 0x32 used for (used by original firmware) but look works proper without them.

## Music Mode:
Music Mode does NOT work default on my motherboard; AsRock Fatal1ty AB350 Gaming-ITX/ac
LED controlling chip (an MCU, nuvoton N76E885AT20) detect sound volume via an Analog Pin,
connected to Realtek ALC1220 sound chip, Pin 0x17. But Linux drivers don't enable that line by default.
You need to install hda-jack-retask tool ( thanks Adam Honse for tool tip ):

 1) Show unconnected pins
 2) Override Pin ID 0x17
 3) Select Line out (Front)
 4) Install boot override (to make settings permanent)
 
After reboot, music mode will work proper, when Analog-speaker out has a sound.

Update pulse 
If you don't use analog output at all, like using monitor HDMI digital sound, here is a solution:

 1) Tick "Advanced override"
 2) Override Came Green Line Out, Rear side (Pin ID: 0x14) and
 3) Set Jack Detection: "Not Present"
 4) Install boot override (to make settings permanent)

to make analog speakers visible at Pulse while not plugged anything on the jack.
Than you can use paprefs tool to enable Pulse audio simultaneous output feature.
With it, you can make your LEDs sync in music mode while listening from your digital HDMI out...
