# LED Infinity Mirror Collar

This repo houses the materials in order to construct a LED infinity mirror collar. The original inspiration for this project I can not take credit for. Adafruit released a [guide](https://learn.adafruit.com/infinity-mirror-collar) that I originally followed. However since there has been slightly modifications to the physical construction and the software as well. 

## Firmware

### How to Flash

Need to use the serial interface.

1. Open serial connection using openocd

```sh
openocd -f interface/stlink.cfg -f target/nrf52.cfg
```

1. In a separate terminal, open the arm gdb

```sh
arm-none-eabi-gdb
```

2. Connect to target

```sh
target extended-remote localhost:3333
```

3. Download the [itsybitsy hex firmware](https://github.com/adafruit/Adafruit_nRF52_Bootloader/releases) or use the file in the ./Bootloader directory.

4. Load the firmware

```sh
load /Users/raysmets/dev/LED-Infinity-Collar/Bootloader/itsybitsy_nrf52840_express_bootloader-0.8.3_s140_6.1.1.hex

```

4. Reset the monitor and continue

```sh
monitor reset
continue
```

Now that you have the itsybitys bootloader installed you can flash the it with CircuitPython. You should be able to see the microcontroller over the the usb interface now.

5. [Download](https://adafruit-circuit-python.s3.amazonaws.com/index.html?prefix=bin/itsybitsy_nrf52840_express/en_US/) the target U2F [Circuit Python](https://circuitpython.org/board/itsybitsy_nrf52840_express/) file or can use the files already in ./Bootloader directory.

6. [Install Circuit Python](https://learn.adafruit.com/welcome-to-circuitpython/installing-circuitpython) by copying [ItsyBitsy](https://learn.adafruit.com/adafruit-itsybitsy-nrf52840-express/circuitpython) uf2 file to main drive. It should then show up in volumes as circuit python!

```sh
cp Bootloader/adafruit-circuitpython-itsybitsy_nrf52840_express-en_US-8.2.9.uf2 /Volumes/ITSY840BOOT 
```

### Upgrading the Bootloader

To [update the bootloader](https://learn.adafruit.com/introducing-the-adafruit-nrf52840-feather/update-bootloader-use-command-line#) you could use the method described above or you could use the usb serial interface and the Adafruit nrfutil. Full directions to do so here. 

1. Download [./adafruit-nrfutil](https://learn.adafruit.com/introducing-the-adafruit-nrf52840-feather/update-bootloader-use-command-line#download-adafruit-nrfutil-3108972) bin
   
2. Find the serial interface device name

```sh
ls /dev/cu.*
```

3. Download the [zip bootloader file](https://github.com/adafruit/Adafruit_nRF52_Bootloader/releases)

3. [Update the bootloader](https://learn.adafruit.com/introducing-the-adafruit-nrf52840-feather/update-bootloader-use-command-line#update-bootloader-3108978) with the command below with the target bootload zip file you want and the serial name.

```sh
./adafruit-nrfutil --verbose dfu serial --package itsybitsy_nrf52840_express_bootloader-0.9.2_s140_6.1.1.zip -p /dev/cu.usbmodem101 -b 115200 --singlebank --touch 1200
```

## Software

### Circuit Python

The ItsyBitsy_Infinity_Collar directory contains the Circuit Python code necessary to drive the animations. It also contains the necessary Adafruit libraries to work appropriately. I opted to go with more stable CircuitPython 6.x firmware and in that folder you will find the modified `code.py` which can be directory cp'd to the root of the ItsyBitsy microcontroller. 

### Personal Software Modifications

Currently the extend of the software modifications entail variable brightness control via the BLE interface via the BlueFruit mobile application. Upon connecting navigate to the control pad menu and use the `up` and `down` arrows to control the LED brightness.

## Physical Housing 

### 3D

The 3D directory contains files from which I took the provided SVGs for the collar's physical construction and turned them into STL files to be 3D printed.