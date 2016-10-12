# Getting started

![escape](/images/escape-450.png)

We decided to base this build on the excellent DJI 450 Flamewheel ARF kit. The kit provides a good solid base on which to experiment and it is fairly straight forward to add a camera to the platform.

## The build

There are many excellent build videos available on-line that detail how to build the basic Quadcopter kit. We've included a few pictures below that detail our build.

##### Unboxing frame and propellors

![ESCAPE CPPM](/images/quad-unboxing-frame.png)


##### Motors

![ESCAPE Motors](/images/quad-motors.png)

These are the motors and ESC's. Two motors are CCW and two CW. The propellors are self-tightening so need to be paired with the correct motor.

##### Motors mounted

![ESCAPE Servos](/images/quad-motors-mounted.png)

The motors are mounted to the frame arms.

![ESCAPE Power Pin](/images/quad-esc-wires-cut.png)

The wires on the ESC's will also need to be cut to length and the ends tinned with solder.

##### Power

![ESCAPE Power](/images/escape-power.png)

The power connection should accept 5v DC - the power you connect here is isolated from your Raspberry Pi and only goes to the servos unless you have the **POWER** jumper in place.

##### Expansion area

![640 Motors](/images/escape-expansionarea.png)

This area to the right of the board is for adding extra expansion boards to increase the functionality available to you. For more information on adding expansion boards [look here](/expansionadding.html)

##### Address selection

![ESCAPE Motors](/images/escape-addressselection.png)

The ESCAPE board uses I2C to control the motors. You can have a lot of I2C controlled boards on your Raspberry Pi at the same time, but each must have a unique address.

We have set up the ESCAPE board to use the address **0x61**. If you find that this conflicts with another board you want to use, and you can't change the address of that board, then you can use these 5 solder jumpers to change the ESCAPE board address.

###### How to change the address

Each of the address pins (A0 - A4) can be set to 0 (un-soldered) or 1 (soldered). You set an address pin to 1 by adding solder to each pad of the address pin until the two parts join.

![Solder Jumpers by Adafruit](/images/solder_jumpers.jpg)

Each address jumper has a binary value - A0 = 1, A1 = 2, A3 = 4, A4 = 8

The starting address for the ESCAPE board is 0x61 - if you look closely at the jumper pads labelled A0 you will see a small connection between them setting this jumper to 1.

If we solder jumper A1 then the address will be 0x61 + 2 = 0x63. Soldering A1 and A2 will give us 0x61 + 2 + 4 = 0x67

## Setup your ESCAPE

Now that we know what each part of the board is for, it's time to solder all the connections - it doesn't matter what order you attach the connections to your board, but we've found that the order below is the simplest.

### Assemble the parts

**IMPORTANT** - if you have an expansion board that you want to add to your 640 board, then you should add that first as it will be a lot easier than adding it after soldering connectors to the board.

![ESCAPE parts](/images/escape-parts.png)

As we don't know what headers and connectors you selected when you ordered your ESCAPE board - we're going to show you how to connect the most common selection - other connectors and headers should attach in the same way.

*Hint* - A lump of plasticine or clay is very useful to hold your board level.

### Attach the 2 pin Power jumper

The small 2 pin jumper is the first part to put in place. It goes in the two holes labelled **POWER**. 

![ESCAPE jumper](/images/escape-jumper.png)

Place it in the holes but don't solder it in place yet.

![ESCAPE jumper in place](/images/escape-jumperinplace.png)

### Attach the 7 pin motor header and 6 pin servo header

The next parts to slot into place are the 7 x 3 connector for the CPPM and motors and the 6 x 3 connector for the servos. The holes for these parts are aligned so that the connectors should fit tightly and be held in place.

![ESCAPE 3 pin](/images/escape-3pin.png)

Slot them in place, and then using a piece of paper or card to hold the connectors in place, turn the board over.

Slide the paper away and use a piece of plasticine or clay to keep the board level on your desk if needed.

![ESCAPE 3 solder pin](/images/escape-solder3pin.png)

Solder all the pins in place - if you solder a single pin on each connector initially, then you can check if they are level and aligned correctly.

If they aren't then apply the soldering iron tip to the soldered pin and move the connector until it is level.

### Attach the power terminal

Now we need to add the power connector - slot it in place making sure that you have it the right way around (for the screw terminals the holes should be at the front of the board).

Use a piece of paper or card to hold the connector in place and turn the board upside down. Slide the paper out from under the board and use a piece of plasticine to prop the board up level.

![ESCAPE terminal](/images/escape-screwterminals.png)

Make sure everything is lined up correctly - use extra plasticine to align connectors if needed. Once you are happy, solder each of the pins.

### Attach the header

For this example we'll show you how to connect a stackable header, as it's the most complex.

Due to the length of the stackable headers pins, it can sometimes be a hassle to get them through the holes on the board.

We've found that if you slide up the spacer on the stackable header so that it is near the top, you can get the pins into the boards header holes a lot easier and then slide the spacer back down again.

![ESCAPE spacer](/images/stacker-trick.png)

Once you have your header in place, use some plasticine to make sure the board is level and then solder away. You should solder a single pin first, then make sure the header is level - if it isn't then apply the soldering iron to the pin again and move the header until it is correct.

![ESCAPE header](/images/escape-header.png)

Now that your board is set up, it's time to configure your Raspberry Pi so that you can use it.

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

[Programming in Python >](/escapepython.html)