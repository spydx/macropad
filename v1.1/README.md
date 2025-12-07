# Macropad v1.1

My first attempt on build a 14 key macropad with two rotary encoders.

Read everything first, this is a very thin guide of what you need, the rest you are on your own.

## What you need

| Count | Component | Link |
| ---- | --- | --- |
|  1 | PCB | JLCPCB or any other |
|  1 | Arduino Micro Pro ATmega32U4 | [SparkFun](https://www.sparkfun.com/pro-micro-5v-16mhz.html) |
| 14 | 1N4148 Diodes | [Mouser](https://no.mouser.com/ProductDetail/onsemi-Fairchild/1N4148?qs=i4Fj9T%2FoRm8RMUhj5DeFQg%3D%3D) |
| 12 | Kailh Choc V2 Low Profiles Keys | [Max Gamming](https://www.maxgaming.no/no/switchar/choc-v2-low-profile-brown) |
|  2 | Rotary Encoderss PEC12R-2120F-S0012 | [Mouser](https://no.mouser.com/ProductDetail/Bourns/PEC12R-2120F-S0012?qs=Zq5ylnUbLm4y5zPMmL%252Bc3g%3D%3D) |
|  1 | OLED 128x32 SSD1306 I2C | [Amazon](https://www.amazon.com/128x32-SSD1306-Consumption-Display-Arduino/dp/B07PDFCVXL) |

Notes.. if you buy other parts than these they might not be compatible, inspect the schematics for details if the components will fit.

You will need knobs for the encoders and keycaps, see 3D print section.

## PCB

The [PCB](PCB/production/Bouvet_MacroPad_v1.zip) can be used to produce the new Rev 1.1 version of the macropad.
The board has the following fixes

- Fliped diode
- Swapped SDA / SCL signal for OLED

You can get PCBs printed from PCBWay or any other.

## Soldering

Recommended soldering order

- Diodes
- Microcontroller
- Switches
- Rotary Encoders
- OLED

## 3D printed Parts

### Keycaps and Knobs

Keycaps are not mentioned here, but you will need Low Profile Keycaps that fit the Kailh Choc V2.
There are many available to be 3D printed. E.g. the following will fit: [Keycaps](https://makerworld.com/en/models/1152559-choc-v2-ultra-thin-keycaps#profileId-1156967)

Rotary encoder knobs are also needed e.g. [these](https://makerworld.com/en/models/154058-grippy-encoder-knob?from=search#profileId-169689)

### Case 

There is a small case in the [CAD](CAD) folder.
Since this was the PoC for this project, it is a very basic case. I have not fixed any of the issues with the case, e.g. the top line, has to be removed for the PCB to fit.

There is a STEP file of the PCB that you can use to aid the design a new case in e.g. FreeCAD.

3D print it upside down, to make the edges pretty (because of the tilted bottom). 
No special setting.

## QMK Firmware

This keyboard uses QMK, until the my PR has been accepted, you need to follow these special steps.

You need to download MY fork of the repository, and checkout the custom branch `custom-keyboards`.
This contains the handwired keyboard config for the macropad.

```shell
git clone https://github.com/spydx/qmk_firmware
cd qmk_firmware
git checkout custom-keyboards

# Ensure that this folder is the QMK homedir
qmk config user.qmk_home=<pwd of your folder> 
qmk config user.keyboard=handwired/bouvet/macropad/v1
qmk config user.keymap=default
```

Once this is you can compile and flash the macropad.

```shell
qmk compile

# While connecting the macro pad, press and hold the top LEFT button until the macropad is detected
qmk flash 
```

Ready to use