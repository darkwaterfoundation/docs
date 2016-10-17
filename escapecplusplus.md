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

##### AccelGyroMag

### Drive a motor
### Motor speed
### Servo control
### PPM integration

## Expanding the board

### Adding an expansion board

### Next steps