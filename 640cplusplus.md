# Programming the 640

## C++

### Introduction

The C++ libraries for the 640 board and some example scripts are available via our GitHub repository. To install them open a terminal window on your Raspberry Pi (unless you are running with only the command line) and enter the following:

``` bash
$ git clone https://github.com/darkwaterfoundation/darkwater_cplus_640.git
```

Once they are download we can navigate into the new directory and take a look around - so enter:

``` bash
$ cd ./darkwater_cplus_640
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

The servo example will move each of the two servos on the 640 board backwards and forwards six times. To build this demo type the following:

``` bash
$ cd ./Servo
$ make
```

Once it is compiled you can run it with the command:

``` bash
$ sudo ./Servo
```

##### PPM

The PPM example will read the input from a PPM radio control receiver connected to the CPPM header on the 640 board, interpret the first 6 channels and move the corresponding motors.

To build this demo type the following:

``` bash
$ cd ./PPM
$ make
```

Once compiled, attach your CPPM receiver to the CPPM connector (see here CPPM set up) and run the program - you will see the output for each channel on the screen as it runs. Attaching motors to each of the motor connectors will allow you to control them individually by moving the sticks on your RC transmitter.

``` bash
$ sudo ./PPM
```

##### AccelGyroMag

If you have a 9DoF expansion board on your 640 board or are using a SOAR board then this example will read and output the Gyroscope, Accelerometer and Compass readings.

To compile and run it, type the following

``` bash
$ cd ./AccelGyroMag
$ make
$ sudo ./AccelGyroMag
```

### The 640 board API

If you take a look at the code in each of the examples you should be able to get an idea of how the 640 board API works. We'll go into more detail of each of the available commands below. 

The first thing we need to do for our program is to import the required libraries - so near the top of your new program you will put

``` c
#include "darkwater/DW640.h"
#include "darkwater/Util.h"
#include <stdlib.h>
```

If you will be using the CPPM header for input then you will also need to add:

``` c
#include <pigpio.h>
#include <stdio.h>
#include <unistd.h>
```

For this example, we'll include everthing in a *main* function for neatness - have a look at the PPM example code for an alternate set up.

``` c
int main()
{

}
```

#### Create a controller

The **DW640** object controls access to all the elements on the 640 board, so the first thing we need to do is create a controller - we pass in the address of the 640 board as a parameter - the default address is 0x60 so if you haven't changed the address then you can leave this out.

``` c
DW640 dw(0x60);
dw.initialize();
```

Now that we have the controller created, we can access all the connectors on the board.

#### Select a Motor

There are 6 motor ports on the 640 board numbered 1 to 6 from left to right (with the ports facing you ).

If we want to control a motor on port number 1 then we need to request the motor object for that port from our controller - this is very easily done with a single line

``` c
DW_Motor *dw1 = dw.getMotor(1);
```

#### Motor driving

There are two main commands that you can give a motor - to move in a direction and to stop. 

We'll start with the main command to stop the motor

##### off()

The off command will switch off the motor

``` c
dw1->off()
```

##### setMotorSpeed( *speed* )

We can also stop the motor by using the second command and passing a speed of 0

``` c
dw1->setMotorSpeed(0);
```

The **setMotorSpeed** command allows you to specify the speed of each motor - there are two different speed ranges the first goes from *-255* to *255*, the second from *1000* to *2000*. 

If you are familiar with radio control vehicles and ESC motors then you will recognise the second range.

For now we'll concentrate on the first range.

To get your motor going forwards at full speed you should set its speed at 255

``` c
dw1->setMotorSpeed(255);
```

To get your motor going backwards at full speed you should set its speed to -255

``` c
dw1->setMotorSpeed(-255)
```

The numbers from 0 to the maximum in each direction will drive the motor at a slower speed, so for half speed forwards we'd use

``` c
dw1->setMotorSpeed(125)
```

And for a slow speed backwards we can use

``` c
dw1->setMotorSpeed(-50)
```

##### Alternate speed range

The spped range above is easy to use as you can quickly see what speed is forwards, backwards and stopped. ESC powered motors use a different range that goes from 1000 to 2000, with 1500 (the middle point) being stop.

Both the ESCAPE and 640 boards can use either range, but if you are primarily working with ESC powered motors and Radio Control inputs then you should use this range as it makes programming a lot easier.

To get your motor going forwards at full speed you should set its speed to 2000

``` c
dw1->setMotorSpeed(2000)
```

For full speed reverse you should set the speed to 1000

``` c
dw1->setMotorSpeed(1000)
```

And to stop the motor we can set the speed to the mid point which is 1500

``` c
dw1->setMotorSpeed(1500)
```

As before, any number between 1500 and the maximum in each direction will drive the motor at a slower speed, so for half speed forward you'd set the speed to 1750

``` c
dw1->setMotorSpeed(1750)
```

and half speed in reverse would be 1250

``` c
dw1->setMotorSpeed(1250)
```

#### Select a Servo

There are two servo ports on the 640 board. They are numbered from 1 to 6 with number 1 to the left hand side and number 6 the closest to the power connector.

You select a servo in the same manner as you select motors, by requesting a servo object from the controller - to select the first servo we use:

``` c
DW_Servo *s1 = dw.getServo(1);
```

#### Servo control

Once you have a servo object there are currently three commands you can run.

##### off()

The off command will switch off your servo and stop any signals being sent to it.

``` c
s1->off();
```

##### setPWMuS( *microseconds* )

This command will allow you to set the PWM pulse to the Servo in microseconds. 

Most standard servos use a parameter value of 1000 for fully counter-clockwise, 2000 for fully clockwise, and 1500 for the middle - though you may have a wider range on your servo, so you should check the technical documentation for it to get the finer details.

``` c
s1->setPWMuS(1500); // middle
s1->setPWMuS(2000); // fully clockwise
s1->setPWMuS(1000); // fully counter clockwise
```

##### setPWMmS( *milliseconds* )

This command allows you to specify the PWM pulse in milliseconds rather than seconds.

``` c
s1->setPWMmS(1.5); // middle
s1->setPWMmS(2.0); // fully clockwise
s1->setPWMmS(1.0); // fully counter clockwise
```

#### Select a Stepper motor

You can control up to 3 stepper motors with the 640 board - each stepper motor uses two motor ports for 4 wire stepper motors and three motor ports for 5 wire stepper motors. 

Running 5 wire stepper motors is almost the same as 4 wire stepper motos but requires a small extra step which we'll explain at the end.

Each stepper motor is assigned to a pair of motor ports:
- **Stepper motor 1** - uses motor ports 1 and 2
- **Stepper motor 2** - uses motor ports 3 and 4
- **Stepper motor 3** - uses motor ports 5 and 6

The first step is to identify the two wires for each coil on your stepper motor (you may need to read the technical documentation for your motor to find this out) and attach these two wires to each port.

*Example: You have a stepper motor with 4 wires - orange, pink, yellow and blue. If the orange and pink wires for your stepper motor are attached to coil one then attach these wires to motor port 1, attach the two remaining wires to motor port 2.*

Once you have your stepper motor wired up you need to request the relevant stepper motor object from the controller.

``` c
DW_Stepper *st1 = dw.getStepper(1);
```

The default stepper object created assumes that your stepper motor has 48 steps per revolution - if you motor has more or less steps per revolution then you can specify this using an alterative command:

``` c
DW_Stepper *st1 = dw.getStepper(1, 48);
```

Change the *48* in the line above to the number of steps your stepper motor has per revolution.

#### Stepper motor control

There are four commands for stepper motors. The first one you'll recognise

##### off()

The off command will switch off the stepper motor

``` c
st1->off();
```

##### setMotorSpeed( *rpm* )

This command allows you to set the speed of your stepper motor. Pass the number of revolutions per minute that you want your stepper motor to run at.

``` c
st1->setMotorSpeed(200);
```

##### oneStep( *direction*, *style* )

This command will move the stepper motor one step in your chosen direction -

- **DW_FORWARD** - set the stepper motor to move forward
- **DW_REVERSE** - set the stepper motor to move backwards

There are two stepping styles available - 

- **DW_SINGLE** - this is the simplest method of stepping which activates a single coil at a time to move and hold the motor. This method uses the  least amount of power.
- **DW_DOUBLE** - this is a slightly more complex method of stepping which uses to coils to move and hold the motor. This method uses twice as much power as the single step, but is more powerful.

``` c
st1->oneStep(DW_FORWARD, DW_SINGLE);
st1->oneStep(DW_REVERSE, DW_DOUBLE);
```

##### step( *steps*, *direction*, *style* )

If you want to move the stepper motor a set number of steps then you can use this command. This, however, will stop all processing until the motor has moved the specified number of steps.

``` c
st1->step( 400, DW_FORWARD, DW_SINGLE );
st1->step( 400, DW_REVERSE, DW_DOUBLE );
```

If you want more control and need to move two or more motors at the same time then you should use the **oneStep** command.

### Compiling your code

Unlike with Python, we need to take an extra step with C++ and compile our code so that it can be run on the Raspberry Pi.

To do that, and to make it easier to re-compile as you update, we will create a *makefile*. The *makefile* is a little script that knows the location of all the libraries we want to include in our program and knows how to compile them together to make a single exectuable. 