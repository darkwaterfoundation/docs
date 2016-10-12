# Getting started

![soar](/images/soar-450.png)

Welcome to the SOAR board - this is a very simple board designed to hold our small expansion sensors. 

Whilst you may decide to connect an expansion sensor directly to your control board - if you think that you may change motor drivers at some point, then this board gives you the option of keeping your sensors separate.

## Setup your SOAR

The first thing you should do is add the expansion sensor to your SOAR board - it is a lot easier to solder it on when the SOAR board is flat on your desk.

![SOAR expansion](/images/soarexpansion.png)

Our guide to adding the [expansion board is here](/expansionadding.html). When you have the expansion board added, return here.

### Attach the header

For this example we'll show you how to connect a stackable header, as it's the most complex.

Due to the length of the stackable headers pins, it can sometimes be a hassle to get them through the holes on the board.

We've found that if you slide up the spacer on the stackable header so that it is near the top, you can get the pins into the boards header holes a lot easier and then slide the spacer back down again.

![SOAR spacer](/images/stacker-trick.png)

Once you have your header in place, use some plasticine to make sure the board is level and then solder away. You should solder a single pin first, then make sure the header is level - if it isn't then apply the soldering iron to the pin again and move the header until it is correct.

![SOAR header](/images/soar-header.png)

*Note* - the image above shows the SOAR board ready for the header to be soldered **without** the expansion sensor attached - you can assemble the board in this order if you want (some people prefer it), but it's easier to add the expansion sensor first in out opinion.

Now that your board is set up, it's time to configure your Raspberry Pi so that you can use it.

## Setting up your Pi

Before we can start using the SOAR board we need to enable the interface that the board uses on your Raspberry Pi.

The SOAR board is controlled using the SPI interface.

### Enable SPI in Pixel

If you are using the graphical interface on your Raspberry Pi then click on your main menu icon, move down to *Preferences* and click on the *Raspberry Pi Configuration* menu item. Once open click on the *Interfaces* tab and you should see something like in the image below.

![rasbpi config spi](/images/raspberryspi.png)

Make sure that the line labelled SPI is set to enabled.

Once you click Ok you may be promtped to reboot your Raspberry Pi - go ahead and reboot.

### Enable SPI on the command line

If you are only using the command line on your Raspberry Pi then you will need to use the text version of the Raspberry Pi configuration tool to enable the interfaces.

Type the following to bring up the configuration interface:

``` bash
$ sudo raspi-config
```

Once the menu is showing, scroll down to the *Advanced Options* menu and press Enter.

![rasbpi config adv](/images/advoptions-450.PNG)

Now we'll need to enable the SPI interface, so move down to the *SPI* menu and press Enter. You'll be asked if you want to enabled SPI - select *Yes* and you will see a confirmation and be returned to the main menu.

When you are returned to the main menu, move down to the *Finish* option (pressing the right arrow key twice will get you there) and press enter.

You have now enabled the interface you need to use your board.