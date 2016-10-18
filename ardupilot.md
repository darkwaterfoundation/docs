# Getting started with ArduPilot

ArduPilot can be used with the ESCAPE board to take it to the next level for operating everything from multicopters to full size tractors. More details [here at ardudpilot.org] (http://ardupilot.org)

The ESCAPE board will need to be combined with either a SOAR board  or 9DOF expansion board as well as a MS5611 High resolution atmospheric pressure module (barometer). You can optionally add a serial GPS.

Ideally you will need a version of Raspbian that has been compiled with a Real-Time kernel. Available for download from here.

(Note please don't run 'sudo apt-get update' as this will overwrite the kernel)

## Using our downloaded image

Download our pre-prepared image that already contains compiled programs for either a Quadcopter, Rover or Plane


## Rolling your own

Use an SSH program to log onto the Raspberry Pi.

Clone the Ardupilot source.

```
git clone https://github.com/diydrones/ardupilot.git
cd ardupilot
git submodule update --init
```

Waf is the preferred method of building code

!!! Note
	Waf should always be called from the ardupilot root directory.

To keep access to Waf convenient, use the following alias from the root ardupilot directory:

```
alias waf="$PWD/modules/waf/waf-light"
```

Choose the board to be used:

```
waf configure --board=dark
```

### Build

Now you can build your preferred vehicle. For quadcopter use the following command:

```
waf --targets bin/arducopter-quad
```

To build for other frame types replace quad with one of the following options

```
coax heli hexa octa octa-quad single tri y6
```

At the end of compilation a binary file with the name arducopter-quad will be placed in the following directory

```
ardupilot/build/dark/bin/ 
```

Other vehicle types can be built:

```
waf --targets bin/ardurover  
```

or

```
waf --targets bin/arduplane
```



 



 