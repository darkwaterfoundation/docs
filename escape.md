# Getting started

![escape](/images/escape-450.png)

Welcome to the ESCAPE board - this guide will describe all the features of the ESCAPE board and show you how to control up to 6 motors and 6 servos very simply.

## Board layout

Before we start to assemble your board, we'll take a look at what each section is and what it is for. Place your ESCAPE board on a table in front of you and identify each area.

### CPPM / PPM-SUM

![ESCAPE CPPM](/images/escape-cppm.png)

This is the connection that allows you connect a Radio Control (RC) receiver so that you can extend the range of control for your robot.

### Motors

![ESCAPE Motors](/images/escape-motors.png)

The ESCAPE board can control 6 independent motors. Each motor has a connection with three pins onto which you will plug the control wire from the motors ESC unit. The centre pin on the Motor connections aren't connected together. This is because the centre wire from an ESC sends 5v and having multiple 5v power supplies connected to each other can be very bad.

### Servos

![ESCAPE Servos](/images/escape-servos.png)

The ESCAPE board has connections for 6 Servos. They default to being powered by the ESCAPE boards power supply, but we can switch them to be powered by the Raspberry Pi by placing a jumper on the **POWER** pins (assuming the Raspberry Pi is powered via its USB port).

![ESCAPE Power Pin](/images/escape-powerjumper.png)

We can also power the Raspberry Pi by placing an ESC control wire on one of the Servo connects and using the 5v sent on its power wire with the **POWER** jumper in place.

We'll go into more detail on this later, so don't worry about it for now.

### Power

![ESCAPE Power](/images/escape-power.png)

The power connection should accept 5v DC - the power you connect here is isolated from your Raspberry Pi and only goes to the servos unless you have the **POWER** jumper in place.

### Expansion area

![ESCAPE Expansion](/images/escape-expansionarea.png)

This area to the right of the board is for adding extra expansion boards to increase the functionality available to you. For more information on adding expansion boards [look here](/expansionadding.html)

### Address selection

![ESCAPE Motors](/images/escape-addressselection.png)

The ESCAPE board uses I2C to control the motors. You can have a lot of I2C controlled boards on your Raspberry Pi at the same time, but each must have a unique address.

We have set up the ESCAPE board to use the address **0x61**. If you find that this conflicts with another board you want to use, and you can't change the address of that board, then you can use these 5 solder jumpers to change the ESCAPE board address.

#### How to change the address

Each of the address pins (A0 - A4) can be set to 0 (un-soldered) or 1 (soldered). You set an address pin to 1 by adding solder to each pad of the address pin until the two parts join.

![Solder Jumpers by Adafruit](/images/solder_jumpers.jpg)

Each address jumper has a binary value - A0 = 1, A1 = 2, A3 = 4, A4 = 8

The starting address for the ESCAPE board is 0x61 - if you look closely at the jumper pads labelled A0 you will see a small connection between them setting this jumper to 1.

If we solder jumper A1 then the address will be 0x61 + 2 = 0x63. Soldering A1 and A2 will give us 0x61 + 2 + 4 = 0x67

# Setup your ESCAPE

Now that we know what each part of the board is for, it's time to solder all the connections - it doesn't matter what order you attach the connections to your board, but we've found that the order below is the simplest.

## Assemble the parts

**IMPORTANT** - if you have an expansion board that you want to add to your 640 board, then you should add that first as it will be a lot easier than adding it after soldering connectors to the board.

![ESCAPE parts](/images/escape-parts.png)

As we don't know what headers and connectors you selected when you ordered your ESCAPE board - we're going to show you how to connect the most common selection - other connectors and headers should attach in the same way.

*Hint* - A lump of plasticine or clay is very useful to hold your board level.

## Attach the 2 pin Power jumper

The small 2 pin jumper is the first part to put in place. It goes in the two holes labelled **POWER**. 

![ESCAPE jumper](/images/escape-jumper.png)

Place it in the holes but don't solder it in place yet.

![ESCAPE jumper in place](/images/escape-jumperinplace.png)

## Attach the 7 pin motor header and 6 pin servo header

The next parts to slot into place are the 7 x 3 connector for the CPPM and motors and the 6 x 3 connector for the servos. The holes for these parts are aligned so that the connectors should fit tightly and be held in place.

![ESCAPE 3 pin](/images/escape-3pin.png)

Slot them in place, and then using a piece of paper or card to hold the connectors in place, turn the board over.

Slide the paper away and use a piece of plasticine or clay to keep the board level on your desk if needed.

![ESCAPE 3 solder pin](/images/escape-solder3pin.png)

Solder all the pins in place - if you solder a single pin on each connector initially, then you can check if they are level and aligned correctly.

If they aren't then apply the soldering iron tip to the soldered pin and move the connector until it is level.

## Attach the power terminal

Now we need to add the power connector - slot it in place making sure that you have it the right way around (for the screw terminals the holes should be at the front of the board).

Use a piece of paper or card to hold the connector in place and turn the board upside down. Slide the paper out from under the board and use a piece of plasticine to prop the board up level.

![ESCAPE terminal](/images/escape-screwterminals.png)

Make sure everything is lined up correctly - use extra plasticine to align connectors if needed. Once you are happy, solder each of the pins.

## Attach the header

For this example we'll show you how to connect a stackable header, as it's the most complex.

Due to the length of the stackable headers pins, it can sometimes be a hassle to get them through the holes on the board.

We've found that if you slide up the spacer on the stackable header so that it is near the top, you can get the pins into the boards header holes a lot easier and then slide the spacer back down again.

![ESCAPE spacer](/images/stacker-trick.png)

Once you have your header in place, use some plasticine to make sure the board is level and then solder away. You should solder a single pin first, then make sure the header is level - if it isn't then apply the soldering iron to the pin again and move the header until it is correct.

![ESCAPE header](/images/escape-header.png)

Now that your board is set up, it's time to configure your Raspberry Pi so that you can use it.

# Setting up your Pi

Before we can start using the ESCAPE board we need to enable the interfaces that the board uses on your Raspberry Pi.

The ESCAPE board is controlled using the I2C interface. Any expansion boards attached to your ESCAPE board are controlled using the SPI interface.

## Enable I2C and SPI in Pixel

If you are using the graphical interface on your Raspberry Pi then click on your main menu icon, move down to *Preferences* and click on the *Raspberry Pi Configuration* menu item. Once open click on the *Interfaces* tab and you should see something like in the image below.

![rasbpi config i2c](/images/raspberryi2c.png)

Make sure that the line labelled I2C is set to enabled.

If you have an expansion board then you'll need to enable the SPI interface as well on the line above, so click the *Enabled* setting next to the *SPI* label

![rasbpi config spi](/images/raspberryspi.png)

Once you click Ok you may be promtped to reboot your Raspberry Pi - go ahead and reboot.

## Enable I2C and SPI on the command line

If you are only using the command line on your Raspberry Pi then you will need to use the text version of the Raspberry Pi configuration tool to enable the interfaces.

Type the following to bring up the configuration interface:

```bash
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

## Reboot your Pi

Once you have enabled the interfaces you will need to reboot your Raspberry Pi so that the required libraries can be loaded. This is an important step and your code won't run correctly without it.

# Wiring up the ESCAPE board

Now that we have your ESCAPE board and Raspberry Pi setup, it's time to connect some motors and servos to it.

![the ESCAPE board](/images/onlyescape.png)

## Connecting Servos
## Connecting Motors
## Connecting the power
## Connecting your RC receiver 

# Programming the ESCAPE

## Installing the Python libraries

The Python libraries for the ESCAPE board and some example scripts are available via our GitHub repository. To install them open a terminal window on your Raspberry Pi (unless you are running with only the command line) and enter the following:

```bash
$ git clone https://github.com/darkwaterio/darkwater_python_escape.git
```

Next you need to navigate into the new directory so enter:

```bash
$ cd ./darkwater_python_escape
```

And once in there we can install the libraries with:

```bash
$ sudo python setup.py install
```

### Example scripts

Once everything is installed we can have a play with the example scripts included in the download. As well as being useful to test each part of your board, they are also handy as a starting point when writing your own scrips.

Let's move into the examples directory and take a look at what is there.

```bash
$ cd ./examples
```

If you list the files in this directory, you should see a few test scripts

```bash
$ ls -al
```

#### escapemotortest.py

This script will start each motor port, in the forwards direction, in turn from left to right and then do the same backwards. To run the script enter the following:

```bash
$ python escapemotortest.py
```

#### escapeservotest.py

This script will move any servos connected to the servo headers left, then center, then right. To run the script enter the following:

```bash
$ python escapeservotest.py
```

## The Python API

Now you know everything works, it's time to write your own scripts. So create a new python script in your editor with a memorable name and add the following lines to import our libraries:

```python
import time
from darkwater_escape import dw_Controller, dw_Motor, dw_Servo
```

### Create a controller

The **dw_controller** object controls access to all the elements on the ESCAPE board, so the first thing we need to do is create a controller - we pass in the address of the ESCAPE board as a parameter - the default address is 0x61

```python
dw = dw_Controller( addr=0x61 )
```

Now that we have the controller created, we can access all the connectors on the board.

### Select a Motor

There are 6 motor ports on the ESCAPE board numbered 1 to 6 from left to right (with the ports facing you ).

If we want to control a motor on port number 1 then we need to request the motor object for that port from our controller - this is very easily done with a single line

```python
m1 = dw.getMotor(1)
```

### Motor driving

There are two main commands that you can give a motor - to move in a direction and to stop. 

We'll start with the main command to stop the motor

#### off()

The off command will switch off the motor

```python
m1.off()
```

#### setMotorSpeed( *speed* )

We can also stop the motor by using the second command and passing a speed of 0

```python
m1.setMotorSpeed(0)
```

The **setMotorSpeed** command allows you to specify the speed of each motor - there are two different speed ranges the first goes from *-255* to *255*, the second from *1000* to *2000*. 

If you are familiar with radio control vehicles and ESC motors then you will recognise the second range.

For now we'll concentrate on the first range.

To get your motor going forwards at full speed you should set its speed at 255

```python
m1.setMotorSpeed(255)
```

To get your motor going backwards at full speed you should set its speed to -255

```python
m1.setMotorSpeed(-255)
```

The numbers from 0 to the maximum in each direction will drive the motor at a slower speed, so for half speed forwards we'd use

```python
m1.setMotorSpeed(125)
```

And for a slow speed backwards we can use

```python
m1.setMotorSpeed(-50)
```

#### Alternate speed range

The spped range above is easy to use as you can quickly see what speed is forwards, backwards and stopped. ESC powered motors use a different range that goes from 1000 to 2000, with 1500 (the middle point) being stop.

Both the ESCAPE and 640 boards can use either range, but if you are primarily working with ESC powered motors and Radio Control inputs then you should use this range as it makes programming a lot easier.

To get your motor going forwards at full speed you should set its speed to 2000

```python
m1.setMotorSpeed(2000)
```

For full speed reverse you should set the speed to 1000

```python
m1.setMotorSpeed(1000)
```

And to stop the motor we can set the speed to the mid point which is 1500

```python
m1.setMotorSpeed(1500)
```

As before, any number between 1500 and the maximum in each direction will drive the motor at a slower speed, so for half speed forward you'd set the speed to 1750

```python
m1.setMotorSpeed(1750)
```

and half speed in reverse would be 1250

```python
m1.setMotorSpeed(1250)
```

### Select a Servo

There are six servo ports on the ESCAPE board. They are numbered from 1 to 6 with number 1 to the left hand side and number 6 the closest to the power connector.

You select a servo in the same manner as you select motors, by requesting a servo object from the controller - to select the first servo we use:

```python
s1 = dw.getServo(1)
```

### Servo control

Once you have a servo object there are currently three commands you can run.

#### off()

The off command will switch off your servo and stop any signals being sent to it.

```python
s1.off()
```

#### setPWMuS( *microseconds* )

This command will allow you to set the PWM pulse to the Servo in microseconds. 

Most standard servos use a parameter value of 1000 for fully counter-clockwise, 2000 for fully clockwise, and 1500 for the middle - though you may have a wider range on your servo, so you should check the technical documentation for it to get the finer details.

```python
s1.setPWMuS(1500) # middle
s1.setPWMuS(2000) # fully clockwise
s1.setPWMuS(1000) # fully counter clockwise
```

#### setPWMmS( *milliseconds* )

This command allows you to specify the PWM pulse in milliseconds rather than seconds.

```python
s1.setPWMmS(1.5) # middle
s1.setPWMmS(2.0) # fully clockwise
s1.setPWMmS(1.0) # fully counter clockwise
```

## Installing the C++ libraries

The C++ libraries for the ESCAPE board and some example scripts are available via our GitHub repository. To install them open a terminal window on your Raspberry Pi (unless you are running with only the command line) and enter the following:

```bash
$ git clone https://github.com/darkwaterfoundation/darkwater_cplus_escape.git
```

Once they are download we can navigate into the new directory and take a look around - so enter:

```bash
$ cd ./darkwater_cplus_escape
```

Let's list the contents of that new directory by typing

```bash
$ ls -al
```

You should see two directories (and a README.md file which contains this content), called **darkwater** and **examples**. 

The **darkwater** directory contains all of the classes needed to control your board and the **examples** directory contains a selection of demo code we've put together to show you how they are used.

### Examples

Take a look in the examples directory and you will see the following available demos.

#### Motor

The Motor example will start each motor in turn from 1 through to 6 in a forwards direction, then stop them and do the same in reverse. To build this demo type the following:

```bash
$ cd ./Motor
$ make
```

Once you are returned to the command prompt you can run the program with the command:

```bash
$ sudo ./Motor
```

#### Servo

The servo example will move each of the six servos backwards and forwards six times. To build this demo type the following:

```bash
$ cd ./Servo
$ make
```

Once it is compiled you can run it with the command:

```bash
$ sudo ./Servo
```

#### PPM

The PPM example will read the input from a PPM radio control receiver connected to the CPPM header on the ESCAPE board, interpret the first 6 channels and move the corresponding servos.

To build this demo type the following:

```bash
$ cd ./PPM
$ make
```

Once compiled, attach your CPPM receiver to the CPPM connector (see here CPPM set up) and run the program - you will see the output for each channel on the screen as it runs. Attaching servos to the Servo rail will allow you to control them individually by moving the sticks on your RC transmitter.

```bash
$ sudo ./PPM
```

#### AccelGyroMag

If you have a 9DoF expansion board on your ESCAPE board or are using a SOAR board then this example will read and output the Gyroscope, Accelerometer and Compass readings.

To compile and run it, type the following

```bash
$ cd ./AccelGyroMag
$ make
$ sudo ./AccelGyroMag
```

## The C++ API

If you take a look at the code in each of the examples you should be able to get an idea of how the ESCAPE board API works. We'll go into more detail of each of the available commands below. 

The first thing we need to do for our program is to import the required libraries - so near the top of your new program you will put

```c
#include "darkwater/DWESCAPE.h"
#include "darkwater/Util.h"
#include <stdlib.h>
```

If you will be using the CPPM header for input then you will also need to add:

```c
#include <pigpio.h>
#include <stdio.h>
#include <unistd.h>
```

For this example, we'll include everthing in a *main* function for neatness - have a look at the PPM example code for an alternate set up.

```c
int main()
{

}
```

### Create a controller

The **DWESCAPE** object controls access to all the elements on the ESCAPE board, so the first thing we need to do is create a controller - we pass in the address of the ESCAPE board as a parameter - the default address is 0x61 so if you haven't changed the address then you can leave this out.

```c
DWESCAPE dw(0x61);
dw.initialize();
```

Now that we have the controller created, we can access all the connectors on the board.

### Select a Motor

There are 6 motor ports on the ESCAPE board numbered 1 to 6 from left to right (with the ports facing you ).

If we want to control a motor on port number 1 then we need to request the motor object for that port from our controller - this is very easily done with a single line

```c
DW_Motor *dw1 = dw.getMotor(1);
```

### Motor driving

There are two main commands that you can give a motor - to move in a direction and to stop. 

We'll start with the main command to stop the motor

#### off()

The off command will switch off the motor

```c
dw1->off()
```

#### setMotorSpeed( *speed* )

We can also stop the motor by using the second command and passing a speed of 0

```c
dw1->setMotorSpeed(0);
```

The **setMotorSpeed** command allows you to specify the speed of each motor - there are two different speed ranges the first goes from *-255* to *255*, the second from *1000* to *2000*. 

If you are familiar with radio control vehicles and ESC motors then you will recognise the second range.

For now we'll concentrate on the first range.

To get your motor going forwards at full speed you should set its speed at 255

```c
dw1->setMotorSpeed(255);
```

To get your motor going backwards at full speed you should set its speed to -255

```c
dw1->setMotorSpeed(-255)
```

The numbers from 0 to the maximum in each direction will drive the motor at a slower speed, so for half speed forwards we'd use

```c
dw1->setMotorSpeed(125)
```

And for a slow speed backwards we can use

```c
dw1->setMotorSpeed(-50)
```

#### Alternate speed range

The spped range above is easy to use as you can quickly see what speed is forwards, backwards and stopped. ESC powered motors use a different range that goes from 1000 to 2000, with 1500 (the middle point) being stop.

Both the ESCAPE and 640 boards can use either range, but if you are primarily working with ESC powered motors and Radio Control inputs then you should use this range as it makes programming a lot easier.

To get your motor going forwards at full speed you should set its speed to 2000

```c
dw1->setMotorSpeed(2000)
```

For full speed reverse you should set the speed to 1000

```c
dw1->setMotorSpeed(1000)
```

And to stop the motor we can set the speed to the mid point which is 1500

```c
dw1->setMotorSpeed(1500)
```

As before, any number between 1500 and the maximum in each direction will drive the motor at a slower speed, so for half speed forward you'd set the speed to 1750

```c
dw1->setMotorSpeed(1750)
```

and half speed in reverse would be 1250

```c
dw1->setMotorSpeed(1250)
```

### Select a Servo

There are six servo ports on the ESCAPE board. They are numbered from 1 to 6 with number 1 to the left hand side and number 6 the closest to the power connector.

You select a servo in the same manner as you select motors, by requesting a servo object from the controller - to select the first servo we use:

```c
DW_Servo *s1 = dw.getServo(1);
```

### Servo control

Once you have a servo object there are currently three commands you can run.

#### off()

The off command will switch off your servo and stop any signals being sent to it.

```c
s1->off();
```

#### setPWMuS( *microseconds* )

This command will allow you to set the PWM pulse to the Servo in microseconds. 

Most standard servos use a parameter value of 1000 for fully counter-clockwise, 2000 for fully clockwise, and 1500 for the middle - though you may have a wider range on your servo, so you should check the technical documentation for it to get the finer details.

```c
s1->setPWMuS(1500); // middle
s1->setPWMuS(2000); // fully clockwise
s1->setPWMuS(1000); // fully counter clockwise
```

#### setPWMmS( *milliseconds* )

This command allows you to specify the PWM pulse in milliseconds rather than seconds.

```c
s1->setPWMmS(1.5); // middle
s1->setPWMmS(2.0); // fully clockwise
s1->setPWMmS(1.0); // fully counter clockwise
```

## Compiling your code

Unlike with Python, we need to take an extra step with C++ and compile our code so that it can be run on the Raspberry Pi.

To do that, and to make it easier to re-compile as you update, we will create a *makefile*. The *makefile* is a little script that knows the location of all the libraries we want to include in our program and knows how to compile them together to make a single exectuable. 