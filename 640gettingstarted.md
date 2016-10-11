## Getting started

![640](/images/640-450.png)

Welcome to the 640 board - this guide will describe all the features of the 640 board and show you how to control up to 6 motors or 3 stepper motors and 2 servos very simply.

## Board layout

##### CPPM / PPM-SUM

![640 CPPM](/images/640-cppm.png)

##### Servos

![640 Servos](/images/640-servo.png)

##### Motors

![640 Motors](/images/640-motors.png)

##### Power

![640 Power](/images/640-power.png)


## Setup your 640
### Attaching the power
### Attaching a Servo
### Attaching a motor
### Attaching an RC receiver

## Setting up your Pi

Before we can start using the 640 board we need to enable the interfaces that the board uses on your Raspberry Pi.

The 640 board is controlled using the I2C interface. Any expansion boards attached to your 640 board are controlled using the SPI interface.

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

