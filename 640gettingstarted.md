# Getting started

![640](/images/640-450.png)

Welcome to the 640 board - this guide will describe all the features of the 640 board and show you how to control up to 6 motors or 3 stepper motors and 2 servos very simply.

## Board layout

Before we start to assemble your board, we'll take a look at what each section is and what it is for. Place your 640 board on a table in front of you and identify each area.

##### CPPM / PPM-SUM

![640 CPPM](/images/640-cppm.png)

This is the connection that allows you connect a Radio Control (RC) receiver so that you can extend the range of control for your robot.

##### Servos

![640 Servos](/images/640-servo.png)

The 640 board has connections for two Servos. They default to being powered by the Raspberry Pi 5v supply, but we can switch them to be powered by the external battery supply if we want to.

##### Motors

![640 Motors](/images/640-motors.png)

The 640 board can control 6 independent motors. Each motor has a connection with two pins (or terminals if you are using the screw terminal connections). It doesn't matter which way around you wire your motor, just make sure that you wire them all the same way. If you find that sending a Forward command makes your robot go backwards, then you can switch the wires around.

##### Power

![640 Power](/images/640-power.png)

The power connection can accept from 2v all the way up to 11v DC - the power you connect here is isolated from your Raspberry Pi and only goes to the motors. Make sure you match your recommended motor voltage as too much power can damage them, and too little won't make them turn.

##### Expansion area

![640 Motors](/images/640-expansionarea.png)

This area to the right of the board is for adding extra expansion boards to increase the functionality available to you. For more information on adding expansion boards [look here](/expansionadding.html)

##### Address selection

![640 Motors](/images/640-addressselection.png)

The 640 board uses I2C to control the motors. You can have a lot of I2C controlled boards on your Raspberry Pi at the same time, but each must have a unique address.

We have set up the 640 board to use the address **0x60**. If you find that this conflicts with another board you want to use, and you can't change the address of that board, then you can use these 5 solder jumpers to change the 640 board address.

###### How to change the address

Each of the address pins (A0 - A4) can be set to 0 (un-soldered) or 1 (soldered). You set an address pin to 1 by adding solder to each pad of the address pin until the two parts join.

![Solder Jumpers by Adafruit](/images/solder_jumpers.jpg)

Each address jumper has a binary value - A0 = 1, A1 = 2, A3 = 4, A4 = 8

The starting address for the 640 board is 0x60 - if we solder jumper A0 then the address will be 0x60 + 1 = 0x61. Soldering A0 and A1 will give us 0x60 + 1 + 2 = 0x63

## Setup your 640

Now that we know what each part of the board is for, it's time to solder all the connections - it doesn't matter what order you attach the connections to your board, but we've found that the order below is the simplest.

### Assemble the parts

**IMPORTANT** - if you have an expansion board that you want to add to your 640 board, then you should add that first as it will be a lot easier than adding it after soldering connectors to the board.

![640 parts](/images/640-parts.png)

As we don't know what headers and connectors you selected when you ordered your 640 board - we're going to show you how to connect the most common selection - other connectors and headers should attach in the same way.

*Hint* - A lump of plasticine or clay is very useful to hold your board level.

### Attached the 3 pin servo header

The first part to slot into place is the 3 x 3 connector for the CPPM and Servos. The holes for this part are aligned so that the connector should fit tightly and be held in place.

![640 3 pin](/images/640-3pin.png)

Slot it in place, but don't solder it yet.

### Attach the motor and power terminals

Now we need to add the motor and power connectors - slot each in place making sure that you have them the right way around (for the screw terminals the holes should be at the front of the board).

Use a piece of paper or card to hold the connectors in place and turn the board upside down. Slide the paper out from under the board and use a piece of plasticine to prop the board up level.

![640 terminals](/images/640-screwterminals.png)

Make sure everything is lined up correctly - use extra plasticine to align connectors if needed. Once you are happy, solder each of the pins.

### Attach the header

For this example we'll show you how to connect a stackable header, as it's the most complex.

Due to the length of the stackable headers pins, it can sometimes be a hassle to get them through the holes on the board.

We've found that if you slide up the spacer on the stackable header so that it is near the top, you can get the pins into the boards header holes a lot easier and then slide the spacer back down again.

![640 spacer](/images/stacker-trick.png)

Once you have your header in place, use some plasticine to make sure the board is level and then solder away. You should solder a single pin first, then make sure the header is level - if it isn't then apply the soldering iron to the pin again and move the header until it is correct.

![640 header](/images/640-header.png)

Now that your board is set up, it's time to configure your Raspberry Pi so that you can use it.

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

## Wiring everything up

### Attaching the power
### Attaching a Servo
### Attaching a motor
### Attaching an RC receiver

### Next steps

