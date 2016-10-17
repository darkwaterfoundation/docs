# Programming the ESCAPE

## Python

### Introduction

The Python libraries for the ESCAPE board and some example scripts are available via our GitHub repository. To install them open a terminal window on your Raspberry Pi (unless you are running with only the command line) and enter the following:

``` bash
$ git clone https://github.com/darkwaterfoundation/darkwater_python_escape.git
```

Next you need to navigate into the new directory so enter:

``` bash
$ cd ./darkwater_python_escape
```

And once in there we can install the libraries with:

``` bash
$ sudo python setup.py install
```

### Example scripts

Once everything is installed we can have a play with the example scripts included in the download. As well as being useful to test each part of your board, they are also handy as a starting point when writing your own scrips.

Let's move into the examples directory and take a look at what is there.

``` bash
$ cd ./examples
```

If you list the files in this directory, you should see a few test scripts

``` bash
$ ls -al
```

#### escapemotortest.py

This script will start each motor port, in the forwards direction, in turn from left to right and then do the same backwards. To run the script enter the following:

``` bash
$ python escapemotortest.py
```

#### escapeservotest.py

This script will move any servos connected to the servo headers left, then center, then right. To run the script enter the following:

``` bash
$ python escapeservotest.py
```

### The ESCAPE board API

Now you know everything works, it's time to write your own scripts. So create a new python script in your editor with a memorable name and add the following lines to import our libraries:

``` python
import time
from darkwater_escape import dw_Controller, dw_Motor, dw_Servo
```

#### Create a controller

The **dw_controller** object controls access to all the elements on the ESCAPE board, so the first thing we need to do is create a controller - we pass in the address of the ESCAPE board as a parameter - the default address is 0x61

``` C
dw = dw_Controller( addr=0x61 )
```

Now that we have the controller created, we can access all the connectors on the board.

#### Select a Motor

There are 6 motor ports on the ESCAPE board numbered 1 to 6 from left to right (with the ports facing you ).

If we want to control a motor on port number 1 then we need to request the motor object for that port from our controller - this is very easily done with a single line

``` python
m1 = dw.getMotor(1)
```

#### Motor driving

There are two main commands that you can give a motor - to move in a direction and to stop. 

We'll start with the main command to stop the motor

##### off()

The off command will switch off the motor

``` python
m1.off()
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

and half speed in reverse would be 1250

``` python
m1.setMotorSpeed(1250)
```

#### Select a Servo

There are six servo ports on the ESCAPE board. They are numbered from 1 to 6 with number 1 to the left hand side and number 6 the closest to the power connector.

You select a servo in the same manner as you select motors, by requesting a servo object from the controller - to select the first servo we use:

``` python
s1 = dw.getServo(1)
```

#### Servo control

Once you have a servo object there are currently three commands you can run.

##### off()

The off command will switch off your servo and stop any signals being sent to it.

``` python
s1.off()
```

##### setPWMuS( *microseconds* )

This command will allow you to set the PWM pulse to the Servo in microseconds. 

Most standard servos use a parameter value of 1000 for fully counter-clockwise, 2000 for fully clockwise, and 1500 for the middle - though you may have a wider range on your servo, so you should check the technical documentation for it to get the finer details.

``` python
s1.setPWMuS(1500) # middle
s1.setPWMuS(2000) # fully clockwise
s1.setPWMuS(1000) # fully counter clockwise
```

##### setPWMmS( *milliseconds* )

This command allows you to specify the PWM pulse in milliseconds rather than seconds.

``` python
s1.setPWMmS(1.5) # middle
s1.setPWMmS(2.0) # fully clockwise
s1.setPWMmS(1.0) # fully counter clockwise
```

### Next steps