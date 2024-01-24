# Project Koyomi - display testing hat

This is the first part of the development of Project Koyomi, read [this blog post](https://blog.exentio.sexy/2023/12/11/project-koyomi-planning.html)
for more.  
The purpose of this Raspberry Pi hat is to test and play around with the
display of the Vaio P before further development of the motherboard.  

### ⚠️ WARNING: at the moment of writing, this board is untested.  

The board uses Texas Instruments' SN75LVDS83B LVDS transmitter using the Pi's
DPI signals to send video out to the display. I might consider dropping DPI and
replacing it with a DVI receiver to free up the Raspberry's GPIO, but those ICs
tend to be bulky so it'll be considered in the later stages of development.  

The display connector is made by I-PEX, and the model numbers are
`20374-030E-31`/`20374-R30E-31`, they're the same but the 0 variant seems to be
more common.  
The display, in my case a LT080EE04100 by Toshiba (it should be the same for
all Vaio Ps), has no backlight driver, and for that the backlight pins are
broken out, allowing testing of different drivers.  
The driver will be controlled using software I2C since all the hardware I2C
pims are already used by DPI. The assigned GPIOs are 23 for SDA and 24 for SCL.
More info about software I2C on [this page](https://learn.adafruit.com/raspberry-pi-i2c-clock-stretching-fixes/software-i2c).

Huge thanks to Arya ([@CRImier](https://github.com/CRImier)) for her help during most phases of the design!
