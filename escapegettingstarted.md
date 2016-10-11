# Getting started

![escape](/images/escape-450.png)

Welcome to the ESCAPE board - this guide will describe all the features of the ESCAPE board and show you how to control up to 6 motors and 6 servos very simply.

## Board layout

Before we start to assemble your board, we'll take a look at what each section is and what it is for. Place your ESCAPE board on a table in front of you and identify each area.

##### CPPM / PPM-SUM

![ESCAPE CPPM](/images/640-cppm.png)

This is the connection that allows you connect a Radio Control (RC) receiver so that you can extend the range of control for your robot.

##### Motors

![ESCAPE Motors](/images/640-motors.png)

The ESCAPE board can control 6 independent motors. Each motor has a connection with three pins onto which you will plug the control wire from the motors ESC unit. The centre pin on the Motor connections aren't connected together. This is because the centre wire from an ESC sends 5v and having multiple 5v power supplies connected to each other can be very bad.

##### Servos

![ESCAPE Servos](/images/640-servo.png)

The ESCAPE board has connections for 6 Servos. They default to being powered by the ESCAPE boards power supply, but we can switch them to be powered by the Raspberry Pi by placing a jumper on the **POWER** pins (assuming the Raspberry Pi is powered via its USB port).

We can also power the Raspberry Pi by placing an ESC control wire on one of the Servo connects and using the 5v sent on its power wire with the **POWER** jumper in place.

We'll go into more detail on this later, so don't worry about it for now.

##### Power

![ESCAPE Power](/images/640-power.png)

The power connection should accept 5v DC - the power you connect here is isolated from your Raspberry Pi and only goes to the servos unless you have the **POWER** jumper in place.

##### Expansion area

![640 Motors](/images/640-expansionarea.png)

This area to the right of the board is for adding extra expansion boards to increase the functionality available to you. For more information on adding expansion boards [look here](/expansionadding.html)

##### Address selection

![640 Motors](/images/640-addressselection.png)

The ESCAPE board uses I2C to control the motors. You can have a lot of I2C controlled boards on your Raspberry Pi at the same time, but each must have a unique address.

We have set up the 640 board to use the address **0x61**. If you find that this conflicts with another board you want to use, and you can't change the address of that board, then you can use these 5 solder jumpers to change the 640 board address.

###### How to change the address

Each of the address pins (A0 - A4) can be set to 0 (un-soldered) or 1 (soldered). You set an address pin to 1 by adding solder to each pad of the address pin until the two parts join.

![Solder Jumpers by Adafruit](/images/solder_jumpers.jpg)

Each address jumper has a binary value - A0 = 1, A1 = 2, A3 = 4, A4 = 8

The starting address for the ESCAPE board is 0x61 - if you look closely at the jumper pads labelled A0 you will see a small connection between them setting this jumper to 1.

If we solder jumper A1 then the address will be 0x61 + 2 = 0x63. Soldering A1 and A2 will give us 0x61 + 2 + 4 = 0x67

## Setting up your Pi

Before we can start using the ESCAPE board we need to enable the interfaces that the board uses on your Raspberry Pi.

The ESCAPE board is controlled using the I2C interface. Any expansion boards attached to your ESCAPE board are controlled using the SPI interface.

### Enable I2C and SPI in Pixel

If you are using the graphical interface on your Raspberry Pi then click on your main menu icon, move down to *Preferences* and click on the *Raspberry Pi Configuration* menu item. Once open click on the *Interfaces* tab and you should see something like in the image below.

![rasbpi config i2c](/images/raspberryi2c.png)

Make sure that the line labelled I2C is set to enabled.

If you have an expansion board then you'll need to enable the SPI interface as well on the line above, so click the *Enabled* setting next to the *SPI* label

![rasbpi config spi](/images/raspberryspi.png)

Once you click Ok you may be promtped to reboot your Raspberry Pi - go ahead and reboot.

### Enable I2C and SPI on the command line

If you are only using the command line on your Raspberry Pi then you will need to use the text version of the Raspberry Pi configuration tool to enable the interfaces.

Type the following to bring up the configuration interface:

``` bash
$ sudo raspi-config
```

Once the menu is showing, scroll down to the *Advanced Options* menu and press Enter.

![rasbpi config adv](/images/advoptions-450.PNG)

Now we'll need to enable the I2C interface, so move down *I2C* menu and press Enter. You'll be asked if you want to enabled I2C - select *Yes* and you will see a confirmation and be returned to the main menu.

![rasbpi config adv i2c](/images/i2c-450.PNG)

Go to the *Advanced Options* again and do the same for *SPI*

![rasbpi config adv spi](/images/spi-450.PNG)

This time when you are returned to the main menu, move down to the *Finish* option (pressing the right arrow key twice will get you there) and press enter.

You have now enabled the interfaces you need to use your board.

### Next steps