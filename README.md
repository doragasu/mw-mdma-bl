# mw-mdma-fw
Bootloader for the MegaWiFi Programmer, to be used along with the programmer firmware ([mw-mdma-fw](https://github.com/doragasu/mw-mdma-fw/)).

# Building
You will `need avr-gcc`, `avr-binutils` and `avr-libc` to be able to build the sources. You will also need a recent [LUFA library](http://www.fourwalledcubicle.com/LUFA.php) installation. Edit `makefile` file, and change the `LUFA_PATH` definition to match the path where you have installed LUFA library:

```
LUFA_PATH   ?= $(HOME)/src/avr/lufa/lufa-latest/LUFA
```

Then cd to the path where the sources of this repository are located and simply run:

```
$ make
```

To burn the bootloader, you will need an external tool, such an ISP programmer. You cannot use a DFU programmer already burned on the microcontroller to flash this bootloader.

# Usage

## Entering DFU bootloader mode
If `mw-mdma-fw` is burned into the microcontroller, the bootloader will start it automatically. Otherwise DFU bootloader will be automatically entered. To switch to DFU bootloader mode when in normal firmware mode, you can try keeping pressed the pushbutton in the board while plugging the USB cable, or you can try using `mw-mdma-cli` tool with the command:
```
$ mdma -b
```

When in DFU bootloader mode, the two LEDs in the programmer board will start blinking alternatively, indicating that the board is ready to accept DFU commands.

## Flashing the application firmware
When in DFU bootloader mode, to burn a new firmware, you can use DFU tools such as [Atmel FLIP for Windows](https://www.atmel.com/tools/FLIP.aspx) of [dfu-programmer](https://github.com/dfu-programmer/dfu-programmer) for Unix/Linux/Mac. Programming the firmware using `dfu-programmer` usually requires 3 commands:
```
$ dfu-programmer at90usb646 erase
$ dfu-programmer at90usb646 flash mdma-fw.hex
$ dfu-programmer at90usb646 reset
```

If you are inside of the mw-mdma-fw source tree, you can burn the latest firmware just by executing:

```
$ make dfu
```

The new firmare will be uploaded and the board will be reset, starting the flashed firmware.

# Authors
This program has been adapted from the LUFA DFU bootloader by Dean Camera, by doragasu.

# License
This program is provided with NO WARRANTY, under the [GPLv3 license](https://www.gnu.org/licenses/gpl-3.0.html).

