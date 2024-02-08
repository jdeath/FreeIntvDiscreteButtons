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
These directions are using a Retronic Design Adapter with an AtGames INTV Flashback Controller. My device worked best (all keys worked on two controlles) with firmware Intellivision_Flashback_Controller_DollarGeneral_v3.3.hex (https://github.com/retronicdesign/USBJoystickAdapter_v3.3/releases/tag/v3.3). The retronic design converter is really nice and supports many orrignal controllers like INTV, Coleco, Atari, etc. Support them. Each coverter is about $30 USD.

The AtGames INTV flashback is pretty fun. But the sound sticks, cannot save games, cannot use cheats, etc. But a great way to obtain the license to run the games and the controllers are exactly like the orginal!

<img src="https://github.com/jdeath/FreeIntvDiscreteButtons/assets/17914369/8f85c5ca-9af2-4bd1-a918-185472afb2c0" width="300">


<img src="https://github.com/jdeath/FreeIntvDiscreteButtons/assets/17914369/c9e1a746-8cb4-4824-81fd-067068421c4c" width="500">

### Flash the Firmware
Get the Mr. Switcher Software from Retronic Design (https://www.retronicdesign.com/). Plug in controller to converter. Hold 6 button on controller while pluggin in the USB to computer. Keep holding, then hit refresh in software. You should see HIDBoot. Click the firmware and flash. Must still be holding 6. It will probably error, but it actually works. You will see the device name change in Mr. Switcher

### Setup EmulationStation
Things changed in Batocera v39. Do not configure the controller in EmulationStation in batocera. It will be recognized as a SNES controller. So out of the box, the disk will function as a joystick and the bottom buttons function as "A" and "B". Setting it up in emulation station further will prevent the mapping from working correcty.

In emulation station, force your controller as controller 3 (you want a regular controller for hotkeys since cannot hit two buttons at once). I have two other controllers, so I use player3 for my intv controller, but change if you only have 1 other controller. In emulation station: Select->Controller & Bluetooth -> P1’s , P2’s, P3’s etc. You must still have another controller, because hotkey will not work on the INTV controller!

### Replace the core
If on x86 batocera, you can use the binary in the release in this github. If I can learn how to cross compile, I can add more architectures. Place the libretro_freeintv.so file in your system directory. Then edit custom.sh to overwrite the core on every boot. Edit your /userdata/share/system/custom.sh to have the below line:
```
cp -f /userdata/share/system/libretro_freeintv.so /usr/lib/libretro/
```

If you use the retronic design converter the SDL buttons should be mapped as so. If not, use jtest-sdl2 --test <joystick#> to figure out how your controller is mapped. Mine looks like this:

<img src="https://github.com/jdeath/FreeIntvDiscreteButtons/assets/17914369/3668c054-0e7b-47d5-813f-6bcebb7909b6" height="300">


Emulation station thinks analog controllers use the same axis for up/down and left/right, but they are distinct buttons in our case. Note to devs: it would be good if could add option for analog axes be configured as 4 distinct buttons in emulation station to avoid this! So we need to force retroarch freeintv to see the buttons as the axis. We also need to set the L3/R3 buttons

### Add "missing keys" into retroarch
Put this in your batocera.conf: (these are for retronic design, if have another adapter could be different. Use player2 if only have one other controller)
```
intellivision.retroarch.input_player3_l3_btn ="10“
intellivision.retroarch.input_player3_r3_btn = "11“
intellivision.retroarch.input_player3_r_x_plus_btn = "12“
intellivision.retroarch.input_player3_r_x_minus_btn = "13“
intellivision.retroarch.input_player3_r_y_plus_btn = "14“
```

### Setup the core
Finally, load a intv game and go to:

Quick Menu (Via a hotkey on another controller) -> Controls -> Port3 Controls

Device Type: Intellivision Controller (Direct Keypad Buttons)

Mapped Port: 1

This makes our 3rd emulation station controller (the intv one) act as player 1 and configures as a direct keypad

Quick Menu (Via a hotkey on another controller) -> Controls -> Port1 Controls

Mapped Port: 3

This makes our 1st emulation station controller act as player 3

Finally, go into:
Quick Menu (Via a hotkey on another controller) -> Controls -> Port3 Controls

Now you want to map the buttons. On the right, you will see something like:
Start Button (should say 9 next to it): Keypad 1

You want to map the SDL button # (ignore the start, x, y, etc) to the correct INTV button. I will try to post a screen shot, but you can use this table to ensure you get everything. Not sure why some of the -/+ are invertered, but this is what worked for me.
![image](https://github.com/jdeath/FreeIntvDiscreteButtons/assets/17914369/4f696df0-c88c-43dd-86e4-9ebf425a8772)


Save Core Remap File

this will put a remap file in
\\batocera\share\system\configs\retroarch\config\remaps\FreeIntv\FreeIntv.rmp (batocera v34)

and it should load by default. 

### Notes
Happy playing! You can only hit 1 key at a time. For instance, if playing "Night Stalker" you have to release the disk for a split second in order to fire.
