Notice!: I am aware of the installation of the ATXPiHat plugin with 1.3.8 Octoprint. I am working on a solution. I apologize for the issue, there is some sort of issue with PIP and the installer is failing on the smbus2 library which is a prerequisite of the plugin. 

# OctoPrint-Atxpihat

No more cutting up and soldering ATX power supplies for your 12v 3d printer applications. This is a Raspberry Pi Hat that makes the process of changing over to a ATX power supply from the underpowered cheap chinese models a breeze. Fully integrated with Octoprint via the provided plugin. 

These are available for [sale at baprojectworkshop.com](https://baprojectworkshop.com/shop).

6/17/2018 - Version 1.1.5

General Repairs
* Full support for the [ATXPiHat v1](https://baprojectworkshop.com/product/atxpihat-atx-psu-interface-for-3d-printers/) and the [ATXPiHat Zero](https://baprojectworkshop.com/product/atxpihat-zero-atx-psu-interface-for-3d-printers/)
* Worked out the installation and detection of the Adafruit DHT libraries for the DHT11/22/AM2302 temperature sensors
* Consolidated the logging and enhanced integration
* Slowed down the timers that update the browser
* General clean up and misc bug fixes
* Moved the startup code out of init to on_after_startup to make sure that I had a logging injected
* Refined the installation documentation [help](https://baprojectworkshop.com/support/)

ATXPiHat Zero updates - Please review all of the [feature differences](https://wp.me/p98gmw-bf)
* Added IO support – DHT11/22/AM2302/DS18B20/2 and 3 wire filament out sensors - These are all available for [sale](https://baprojectworkshop.com/shop).
* EPO support prior to power up

Initial software release to support the [ATXPiHat](https://wp.me/p98gmw-7g) 1.0. A lot of the features below come disabled and are easily enabled on the settings tab. Here is the hardware/software features;

* Fully compatible with Octoprint 1.3.6 or greater.
* Directly power the Raspberry Pi 3B, no more external power source.
* ATX 24 Molex connector, no more cutting up the supply cables
* Amperage support to handle 19 amps at 12v for heat bed and hot end
* Screw connectors make easy connection to the main board, External Mosfet, etc
* Direct 12v RGB LED support, can also be controlled by GCODE
* Emergency power off (EPO)
* Power On/Off monitoring
* Visual indicator of the 12v supply being active and powering the external devices
* 12v monitored (RPM) cooling fan port
* Upon fan failure it can be configured to automatically shuts the printer down
* Auxiliary 5v support for external powered items
* Monitoring of the 12v rail, for amperage and voltage
* Automatic shutdown when an amperage threshold is reached. Meltdown protection
* Switchable 12 or 5 v connector for controlling external items via GCODE

This plugin is only supported on the Raspberry Pi 3, and has been tested on the Model B. Any requests for help, please use the [contact](https://baprojectworkshop.com/contact/) form for the quickest way to get help.

## Here is the standard disclaimer – you must understand and agree to this!
Understand this, this board has **not** been tested by an independent lab such as UL, or anyone else. **You use it at your own risk**. Each board is shipped tested and should work properly out of the box. They are designed to work with a Raspberry Pi 3b and Zero. However, all the work has been done on Pi 3b’s. I will work hard with the user to make sure that everything is good. **Never, and I mean never, use this board and or your printer unsupervised. I will not be held accountable for anything that happens while using this board. Again, use it at your own risk.**

## Installation

For the most up to date instruction, please refer to [https://baprojectworkshop.com/support/installation-instructions/](https://baprojectworkshop.com/support/installation-instructions/)!

Do not install the plugin until you have completed the installation steps below;
* After you backup the memory chip for the PI, **(Just do it)**
* It is always good to update the Raspbian image prior to any upgrade. From a terminal prompt;

        cd ~
        sudo apt-get update
        sudo apt-get dist-upgrade
        sudo apt-get install build-essential python-dev
        curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
        sudo python get-pip.py
        sudo pip install --upgrade setuptools
        sudo ~/oprint/bin/pip install --upgrade pip
        sudo ~/oprint/bin/pip install --upgrade setuptools

* After completion, go ahead power down the PI and install the board. **Do not just power it off**,

         sudo shutdown now

* Plug the ATXPiHat in and connect the ATX power supply. Make sure that you **do not have any other power source plugged into the PI**, the board and power supply will take care of this. During the installation of the board to the PI, make sure that the board is plugged in to the pins properly and the board is supported on all of the screw holes. **Do not power the board if it is not plugged in properly to the PI. You will destroy the PI.** Check it twice.

* After turning on the ATX power supply, and the PI boots, you will need to [enable](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c) the I2C interface on the PI. Adafruit has some great [instructions](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c) on how to do this.

* This plugin requires the pigpio library from joan@abyz.me.uk - http://abyz.co.uk/rpi/pigpio/python.html . Currently there is no pip installer for this library on the PI, so Octoprint will not install it automatically or install it as a service. There are several available install scripts to do this, here is one [implementation](https://github.com/banichow/pigpioinstall) that I recommend. https://github.com/banichow/pigpioinstall 

* Make sure that there are no other plugins that would conflict with this plugin. PSUControl, LEDStripControl are two. With everything out there, I would review what I already have installed.

* Install via the bundled [Plugin Manager](https://github.com/foosel/OctoPrint/wiki/Plugin:-Plugin-Manager) or manually using this URL:

        https://github.com/banichow/OctoPrint-Atxpihat/archive/master.zip

* We found during our testing, it is a good idea to restart the Pi after installation or upgrade of the plugin. This will be the first thing that we will ask during any support requests.

* There are additional application notes available on my [website](https://baprojectworkshop.com/support/) that go into installation of the pigpio, Adafruit DHT, and 1 wire communications and how to install them on the standard jessie image provided by [Octoprint](https://octoprint.org).

* After this, sign into Octoprint and start working with the board.

## Credits and Contributions

* ATXPiHat Hardware - Steve Smith - Xygax - https://www.facebook.com/Xygax
* PSUControl - Shawn Bruce - https://github.com/kantlivelong/
* LEDStripControl - https://github.com/google/OctoPrint-LEDStripControl
* pigpio - joan@abyz.me.uk - http://abyz.co.uk/rpi/pigpio/python.html
* Octoprint-ETA - Pablo Ventura - https://github.com/pablogventura/Octoprint-ETA
* Gina Häußge <gina@octoprint.org>
* Octoprint-Filament-Reloaded - Connor Huffine - https://github.com/kontakt/Octoprint-Filament-Reloaded
* DS18B20 Temperature sensor - https://pimylifeup.com/raspberry-pi-temperature-sensor/
* https://learn.adafruit.com/adafruits-raspberry-pi-lesson-11-ds18b20-temperature-sensing/ds18b20
* https://www.modmypi.com/blog/am2302-temphumidity-sensor

## Licensing
Creative Commons Attribution-ShareAlike 4.0 International License - http://creativecommons.org/licenses/by-sa/4.0/
