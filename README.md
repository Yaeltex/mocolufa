
# Yaeltex changes

* At [Yaeltex](https://www.yaeltex.com), we build MIDI controllers, and we use mocoLUFA, but we needed to be able to switch form Serial to USB-Midi with a physical switch. The long wire connecting the switch to the ISP header made the signal unstable, so it would never boot in USB-MIDI mode. To prevent this, we soldered a 10 MOhm resistor between pins 4 and 6, but as it is very large, it needed some time at boot to settle the signal. So we added a small delay with a for loop in SetupHardware function in dualMoco.c in order to wait for the pulldown resistor between ISP pins 4 and 6, to settle pin to ground. 
* We increased the size of the buffers that send and receive USB messages (HW_CDC_BULK_OUT_SIZE and HW_CDC_BULK_IN_SIZE) to 16 so we cand send and receive up to 64 bytes of data with SysEx.
  
# Instructions from original mocolufa

## mocoLUFA (MIDI firmware for Arduino Uno)
=
dualMocoLUFA Project
Copyright (C) 2013,2014,2015 by morecat_lab

2015/04/11
   
http://morecatlab.akiba.coocan.jp/lab/index.php/aruino/midi-firmware-for-arduino-uno-moco/?lang=en
  
based on LUFA-100807  

This is dual mode firmware for Arduino Uno.  
There are two mode on this firmware, USB-MIDI(MocoLUFA) and Arduino-Serial.  

INSTRUCTIONS  
1. Burn 16u2 on Arduino Uno.  
   check original document below.  
2. USB-MIDI formware work as default.  
3. To enable Arduino-Serial, ass jumper to PIN 4(MOSI PB2) and PIN6 (grand) on ICSP connector for 16U2.  
   Reset is required to swicth the firmware mode.  
  
-Yoshi  
  
-------------------------------------
original readme.txt from Arduino-Serial  
  
To setup the project and upload the Arduino usbserial application firmware to an ATMEGA16U2 using the Arduino USB DFU bootloader:  
	1. unpack the source into LUFA's Projects directory  
	2. set ARDUINO_MODEL_PID in the makefile as appropriate  
	3. do "make clean; make"  
	4. put the 16U2 into USB DFU mode:  
	4.a. assert and hold the 16U2's RESET line  
	4.b. assert and hold the 16U2's HWB line  
	4.c. release the 16U2's RESET line  
	4.d. release the 16U2's HWB line  
	5. confirm that the board enumerates as either "Arduino Uno DFU" or "Arduino Mega 2560 DFU"  
	6. do "make dfu" (OS X or Linux - dfu-programmer must be installed first) or "make flip" (Windows - Flip must be installed first)  

Check that the board enumerates as either "Arduino Uno" or "Arduino Mega 2560".  Test by uploading a new Arduino sketch from the Arduino IDE.
