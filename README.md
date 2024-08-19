# LED Infinity Mirror Collar

This repo houses the materials in order to construct a LED infinity mirror collar. The original inspiration for this project I can not take credit for. Adafruit released a [guide](https://learn.adafruit.com/infinity-mirror-collar) that I originally followed. However since there has been slightly modifications to the physical construction and the software as well. 

## Firmware

### How to Flash

1. connect using openocd

```sh
openocd -f interface/stlink.cfg -f target/nrf52.cfg
```

1. In a separate terminal, open the arm gdb

```sh
arm-none-eabi-gdb
```

2. connect to target

```sh
target remote localhost:3333
```

3. load the firmware

```sh
load /Users/raysmets/dev/LED-Infinity-Collar/Bootloader/itsybitsy_nrf52840_express_bootloader-0.8.0_s140_6.1.1.hex
```

4. Reset the monitor and continue

```sh
monitor reset
continue
```

Now that you have the itsybitys bootloader installed you can flash the it with CircuitPython. You should be able to see the microcontroller over the the usb interface now.

Copy the Circuit Python uf2 file to main drive. It should then show up in volumes as circuit python!

## Software

### Circuit Python

The ItsyBitsy_Infinity_Collar directory contains the Circuit Python code necessary to drive the animations. It also contains the necessary Adafruit libraries to work appropriately. I opted to go with more stable CircuitPython 6.x firmware and in that folder you will find the modified `code.py` which can be directory cp'd to the root of the ItsyBitsy microcontroller. 

### Personal Software Modifications

Currently the extend of the software modifications entail variable brightness control via the BLE interface via the BlueFruit mobile application. Upon connecting navigate to the control pad menu and use the `up` and `down` arrows to control the LED brightness.

## Physical Housing 

### 3D

The 3D directory contains files from which I took the provided SVGs for the collar's physical construction and turned them into STL files to be 3D printed.