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

### Drive a motor
### Motor speed
### Servo control
### PPM integration

## Expanding the board

### Adding an expansion board

### Next steps