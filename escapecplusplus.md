# Programming the ESCAPE

## C++

### Introduction

The C++ libraries for the ESCAPE board and some example scripts are available via our GitHub repository. To install them open a terminal window on your Raspberry Pi (unless you are running with only the command line) and enter the following:

``` bash
$ git clone https://github.com/darkwaterfoundation/darkwater_cplus_escape.git
```

Once they are download we can navigate into the new directory and take a look around - so enter:

``` bash
$ cd ./darkwater_cplus_escape
```

Let's list the contents of that new directory by typing

``` bash
$ ls -al
```

You should see two directories (and a README.md file which contains this content), called **darkwater** and **examples**. 

The **darkwater** directory contains all of the classes needed to control your board and the **examples** directory contains a selection of demo code we've put together to show you how they are used.

#### Examples

Take a look in the examples directory and you will see the following available demos.

##### Motor

The Motor example will start each motor in turn from 1 through to 6 in a forwards direction, then stop them and do the same in reverse. To build this demo type the following:

``` bash
$ cd ./Motor
$ make
```

Once you are returned to the command prompt you can run the program with the command:

``` bash
$ sudo ./Motor
```

##### Servo

The servo example will move each of the six servos backwards and forwards six times. To build this demo type the following:

``` bash
$ cd ./Servo
$ make
```

Once it is compiled you can run it with the command:

``` bash
$ sudo ./Servo
```

##### PPM

The PPM example will read the input from a PPM radio control receiver connected to the CPPM header on the ESCAPE board, interpret the first 6 channels and move the corresponding servos.

To build this demo type the following:

``` bash
$ cd ./PPM
$ make
```

Once compiled, attach your CPPM receiver to the CPPM connector (see here CPPM set up) and run the program - you will see the output for each channel on the screen as it runs. Attaching servos to the Servo rail will allow you to control them individually by moving the sticks on your RC transmitter.

``` bash
$ sudo ./PPM
```

##### AccelGyroMag

If you have a 9DoF expansion board on your ESCAPE board or are using a SOAR board then this example will read and output the Gyroscope, Accelerometer and Compass readings.

To compile and run it, type the following

``` bash
$ cd ./AccelGyroMag
$ make
$ sudo ./AccelGyroMag
```

### The ESCAPE board API

If you take a look at the code in each of the examples you should be able to get an idea of how the ESCAPE board API works. We'll go into more detail of each of the available commands below. 

The first thing we need to do for our program is to import the required libraries - so near the top of your new program you will put

``` C
#include "darkwater/DWESCAPE.h"
#include "darkwater/Util.h"
#include <stdlib.h>
```

If you will be using the CPPM header for input then you will also need to add:

``` C
#include <pigpio.h>
#include <stdio.h>
#include <unistd.h>
```

For this example, we'll include everthing in a *main* function for neatness - have a look at the PPM example code for an alternate set up.

``` C
int main()
{

}
```

#### Create a controller

The **DWESCAPE** object controls access to all the elements on the ESCAPE board, so the first thing we need to do is create a controller - we pass in the address of the ESCAPE board as a parameter - the default address is 0x61 so if you haven't changed the address then you can leave this out.

``` C
DWESCAPE dw(0x61);
dw.initialize();
```

Now that we have the controller created, we can access all the connectors on the board.

#### Select a Motor

There are 6 motor ports on the ESCAPE board numbered 1 to 6 from left to right (with the ports facing you ).

If we want to control a motor on port number 1 then we need to request the motor object for that port from our controller - this is very easily done with a single line

``` C
DW_Motor *dw1 = dw.getMotor(1);
```

#### Motor driving

There are two main commands that you can give a motor - to move in a direction and to stop. 

We'll start with the main command to stop the motor

##### off()

The off command will switch off the motor

``` C
dw1->off()
```

##### setMotorSpeed( *speed* )

We can also stop the motor by using the second command and passing a speed of 0

``` python
m1.setMotorSpeed(0)
```

The **setMotorSpeed** command allows you to specify the speed of each motor - there are two different speed ranges the first goes from *-255* to *255*, the second from *1000* to *2000*. 

If you are familiar with radio control vehicles and ESC motors then you will recognise the second range.

For now we'll concentrate on the first range.

To get your motor going forwards at full speed you should set its speed at 255

``` python
m1.setMotorSpeed(255)
```

To get your motor going backwards at full speed you should set its speed to -255

``` python
m1.setMotorSpeed(-255)
```

The numbers from 0 to the maximum in each direction will drive the motor at a slower speed, so for half speed forwards we'd use

``` python
m1.setMotorSpeed(125)
```

And for a slow speed backwards we can use

``` python
m1.setMotorSpeed(-50)
```

##### Alternate speed range

The spped range above is easy to use as you can quickly see what speed is forwards, backwards and stopped. ESC powered motors use a different range that goes from 1000 to 2000, with 1500 (the middle point) being stop.

Both the ESCAPE and 640 boards can use either range, but if you are primarily working with ESC powered motors and Radio Control inputs then you should use this range as it makes programming a lot easier.

To get your motor going forwards at full speed you should set its speed to 2000

``` python
m1.setMotorSpeed(2000)
```

For full speed reverse you should set the speed to 1000

``` python
m1.setMotorSpeed(1000)
```

And to stop the motor we can set the speed to the mid point which is 1500

``` python
m1.setMotorSpeed(1500)
```

As before, any number between 1500 and the maximum in each direction will drive the motor at a slower speed, so for half speed forward you'd set the speed to 1750

``` python
m1.setMotorSpeed(1750)
```

and half speed in revers would be 1250

``` python
m1.setMotorSpeed(1250)
```

