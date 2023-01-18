GBxCart RW

A device for reading game ROMs, backing up & restoring saves and flashing re-writable flash carts for GB, GBC and GBA carts from your PC via USB.

No support provided, this is our old v1.3 device.

Purchase the official version https://gbxcart.com

Licensed under CC BY-NC-SA 4.0

Original version by insidegadgets:
https://github.com/insidegadgets/GBxCart-RW


Modded by S-I-M-O-N to work with Arduino MEGA 2560 and it's clones:
https://github.com/S-I-M-O-N/GBxCart-RW-MEGA2560

The design is based on simple wiring between the Gameboy Edge Connector and the Arduino pins, as you can see on the Picture.

  Game Edge Connector (GEC) | pins in order from left to right

  VCC /WR /CS A1  A3  A5  A7  A9  A11 A13 A15 D1  D3  D5  D7  AIN
    CLK /RD A0  A2  A4  A6  A8  A10 A12 A14 D0  D2  D4  D6  /RS GND
   U U U U U U U U U U U U U U U U U U U U U U U U U U U U U U U U  
   | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | |
   | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | |
   | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | |
  5V |38 |40 |23 |25 |27 |29 |36 |34 |32 | 30|48 |46 |44 | 42| 51| 
    NC  39  22  24  26  28  37  35  33  31  49  47  45  43  50  GND
 
  ARDUINO MEGA 2560 PINS
  
  
Installation:
git clone https://github.com/S-I-M-O-N/GBxCart-RW-MEGA2560.git

or download just download the file main.hex

Program Arduino with
make program

or manually with
avrdude -p m2560 -c wiring -P /dev/ttyUSB0 -b 115200 -v -D -U flash:w:main.hex:i  

If you want to compile the main.hex yourself do so with
make all


You can now connect to the Arduino with FlashGBX v2.8.
Installation:
git clone https://github.com/S-I-M-O-N/FlashGBX.git

Run with
python run.py


Trouble-shooting:
This FW and SW only works in this exact configuration. i.e. GBxCart RW v1.3 R22 and FLashGBX v2.8.
Accordingly do not update the firmware nor the software.

It happens that the serial port does not properly initialize.
In this case you should open it with a serial terminal program at 1000000 baud first; e.g.:
minicom -b 1000000 -D /dev/ttyUSB0 -H
You can then the the connection by typing V which should be answered by 16

The FlashGBX software assumes that you have an Arduino with an CH340 serial chip with vendor id 1a86 and product id 7523
Should you have a different chip you need to change the following line in hw_GBxCartRW_ofw.py to reflect your ids:
	if comports[i].vid == 0x1A86 and comports[i].pid == 0x7523:
You can check which ids you have by issuing the command lsusb in the shell.
