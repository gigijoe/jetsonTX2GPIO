# jetsonTX2GPIO
A straightforward C/C++ library to interface with the NVIDIA Jetson TX2 Development Kit GPIO pins.

Modified based on https://github.com/jetsonhacks/jetsonTX1GPIO


Based on Software by RidgeRun
https://developer.ridgerun.com/wiki/index.php/Gpio-int-test.c
 * Copyright (c) 2011, RidgeRun
 * All rights reserved.

and ideas from Derek Malloy Copyright (c) 2012
https://github.com/derekmolloy/beaglebone

exampleGPIApp.cpp describes a simple usage case using a tactile button and LED as input and output.

# Jetson Nano GPIO
Execute the following from a terminal on your Jetson
```bash
sudo groupadd -f -r gpio
sudo usermod -a -G gpio $USER
sudo cp /opt/nvidia/jetson-gpio/etc/99-gpio.rules /etc/udev/rules.d/
sudo udevadm control --reload-rules && sudo udevadm trigger
```
Export GPIO with root privilege. For example, export GPIO18
```
echo "echo 18 > /sys/class/gpio/export" >> /etc/profile.d/export-gpio.sh
```
Then, reboot the Jetson
```bash
sudo reboot now
```

# Description
To add more GPIO pins, modify jetsonGPIO.h and add pin numbers you want.

* Example: 
setup and initialize GPIO388 (Pin37) as output pin on TX2:
```
/* To initialize */
jetsonTX2GPIONumber LEDControlPin = gpio388; 
gpioExport(LEDControlPin);
gpioSetDirection(LEDControlPin,outputPin);

/* To control pin high or low  */
gpioSetValue(LEDControlPin, on);     //Pull high
gpioSetValue(LEDControlPin, off);    //Pull low
```

That's it, very easy. If you like to use C/C++ to control GPIO Pin, just include "jetsonGPIO.h" in the cpp file.

# Jetson Xavier NX GPIO

```
/* To initialize */
jetsonXavierGPIONumber LEDControlPin = gpio422; 
gpioExport(LEDControlPin);
gpioSetDirection(LEDControlPin,outputPin);

/* To control pin high or low  */
gpioSetValue(LEDControlPin, on);     //Pull high
gpioSetValue(LEDControlPin, off);    //Pull low
```
