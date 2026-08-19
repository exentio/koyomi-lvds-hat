# Project Koyomi - display testing hat

This is the first part of the development of Project Koyomi, read [this blog post](https://blog.exentio.sexy/2023/12/11/project-koyomi-planning.html)
for more.  
The purpose of this Raspberry Pi hat is to test and play around with the
display of the Vaio P before further development of the motherboard.  

The board is currently tested and working [as shown here](https://blog.exentio.sexy/2024/05/09/project-koyomi-update-3.html)!

The board uses Texas Instruments' SN75LVDS83B LVDS transmitter using the Pi's
DPI signals to send video out to the display. The final motherboard will use a
DVI receiver to free up the Raspberry's GPIO, a small converter board is in
development and [you can find it here](https://github.com/exentio/koyomi-hdmi-lvds).  

The display connector is made by I-PEX, and the model numbers are
`20374-030E-31`/`20374-R30E-31`, they're the same but the 0 variant seems to be
more common.  
The display, in my case a LT080EE04100 by Toshiba (it should be the same for
all Vaio Ps), has no backlight driver, and for that the backlight pins are
broken out, allowing testing of different drivers.  
The driver will be controlled using software I2C since all the hardware I2C
pins are already used by DPI. The assigned GPIOs are 23 for SDA and 24 for SCL.
More info about software I2C on [this page](https://learn.adafruit.com/raspberry-pi-i2c-clock-stretching-fixes/software-i2c).

The current settings used in `config.txt` (on top of the default) is:  
```
dtparam=i2c_arm=off
dtparam=spi=off
display_auto_detect=0
dtoverlay=vc4-kms-dpi-generic
dtparam=hactive=1600,hfp=32,hsync=65,hbp=97
dtparam=vactive=768,vfp=1,vsync=1,vbp=8
dtparam=width-mm=182,height-mm=87
dtparam=clock-frequency=83600000,rgb666
framebuffer_width=1600
framebuffer_height=768
dtoverlay=i2c-gpio,i2c_gpio_sda=23,i2c_gpio_scl=24
disable_overscan=1
```
---

### Forking guidelines
I hope that this design will inspire people to work on similar projects, and
that they'll be used as references to learn how to work on similar projects!  
If you want to make any contribution, you're welcome to fork and send a pull
request, as long as LLMs are not directly involved and you understand your
changes!  

You're also welcome to make changes to any part of this project to implement
different design choices, without having to send a pull request; however, if
your fork takes a completely different direction from Koyomi and breaks
compatibility, I kindly ask you to drop the name "Koyomi" from your project.
Please also remove every art on the PCB, if possible (wouldn't make sense to
have my face on a completely different project anyway).  
This can't and won't be enforced, so I'm just asking informally to please
respect this request, if you want to use my designs.  

### Commercial use
I purposely decided to allow commercial use for this project for two reasons: I
would be happy if modernized Vaio Ps and Koyomi were to be used in professional
contexts, and to let people distribute PCBs so everyone can build their own,
without having to sell parts myself, which is not something I can handle.  

If you plan to sell boards and parts, I only have these simple requests:  
- Please make them reasonably affordable and don't mark them up absurdly, I
want this project to be approachable from every point of view.  
- If you're profiting from reselling my designs, please donate something back
to the people who made the designs you're selling.  
- Don't remove any drawings/art on the PCBs, but you're allowed to add your own.  

None of these can and will be enforced, so I'm just asking you to respect the
time and hard work the other contributors and I have poured into designing
Koyomi.

---

Huge thanks to Arya ([@CRImier](https://github.com/CRImier)) for her help during most phases of the design!
