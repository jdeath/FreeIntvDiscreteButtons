# FreeIntv
FreeIntv is a libretro emulation core for the Mattel Intellivision designed to be compatible with joypads from the SNES era forward even if they originally required a number pad.

This version includes an option to assign every Intellivision button to a seperate Retropad button. This change was made my msheehan79 (not me!) and available in his dev2 fork (https://github.com/msheehan79/FreeIntv/tree/dev2) . I am including it here in a master branch to be easier to use, incude come compiled cores in releases, and provide insturctions for use in batocera. 

Hopefully one day this will be the default version, but until then will have a copy here. Most ColecoVision cores have this option, so should eventually make it to the default. Must not be many INTV fans around anymore!

## Authors

FreeIntv was created by David Richardson.
The PSG and STIC emulation was made closer to hardware and optimized by Oscar Toledo G. (nanochess), who also added save states.

The Intellivoice code has been contributed by Joe Zbiciak (author of jzintv), and adapted by Oscar Toledo G. (nanochess)

## License
The FreeIntv core is licensed under GPLv2+. More information at https://github.com/libretro/FreeIntv/blob/master/LICENSE

## BIOS
FreeIntv requires two Intellivision BIOS files to be placed in the libretro 'system' folder:

| Function | Filename* | MD5 Hash |
| --- | --- | --- | 
| Executive ROM | `exec.bin`  | `62e761035cb657903761800f4437b8af` |
| Graphics ROM | `grom.bin` | `0cd5946c6473e42e8e4c2137785e427f` |

* BIOS filenames are case-sensitive

## Entertainment Computer System
FreeIntv does not currently support Entertainment Computer System (ECS) functionality. Contributions to the code are welcome!

## Controller overlays
Mattel Intellivision games were often meant to be played with game-specific cards overlaid on the numeric keypad. These overlays convey information which can be very useful in gameplay. Images of a limited selection of Intellivision titles are available at: http://www.intellivisionlives.com/bluesky/games/instructions.shtml

## Controls (Default OSD Setup - If Do not have an INTV Controller)

* **Mini-Keypad** - allows the user to view and select keys from a small Intellivision pad in the lower corner of the display.
* **Controller Swap** - Some Intellivision games expect the left controller to be player one, others expect the right controller. This isn't a problem if you have two controllers (and don't mind juggling them) but users with only one controller or using a portable setup would be effectively locked out of some games. Controller Swap swaps the two controller interfaces so that the player does not have to physically swap controllers.

| RetroPad | FreeIntv Function |
| --- | --- |
| D-Pad| 8-way movement |
| Left Analog Stick | 16-way disc |
| A | Left Action Button |
| Y | Top Action Button |
| X | Use the Last Selected Intellivision Keypad Button. In Astrosmash, for example, you can leave "3" selected to enable instant access to hyperspace. |
| L/R | Activate the Mini-Keypad |
| Start | Pause Game |
| Select | Controller Swap |

## Controls (Discrete Button Setup - If you have a INTV Controller)
These directions are using a Retronic Design Adapter with an AtGames INTV Flashback Controller. My device worked best (all keys worked on two controlles) with firmware Intellivision_Flashback_Controller_DollarGeneral_v3.3.hex (https://github.com/retronicdesign/USBJoystickAdapter_v3.3/releases/tag/v3.3). 

The AtGames INTV flashback is pretty fun. But the sound sticks, cannot save games, cannot use cheats, etc. But a great way to obtain the license to run the games and the controllers are exactly like the orginal!

<img src="https://github.com/jdeath/FreeIntvDiscreteButtons/assets/17914369/8f85c5ca-9af2-4bd1-a918-185472afb2c0" width="300">


<img src="https://github.com/jdeath/FreeIntvDiscreteButtons/assets/17914369/c9e1a746-8cb4-4824-81fd-067068421c4c" width="500">

### Flash the Firmware
Get the Mr. Switcher Software from Retronic Design (https://www.retronicdesign.com/). Plug in controller to converter. Hold 6 button on controller while pluggin in the USB to computer. Keep holding, then hit refresh in software. You should see HIDBoot. Click the firmware and flash. Must still be holding 6. It will probably error, but it actually works. You will see the device name change in Mr. Switcher

TBD


