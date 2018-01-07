# OpenKickstartSwitcher
OpenKickstartSwitcher is an Open Hardware Triple Kickstart Switcher for Amiga Computers.

![Board](https://raw.githubusercontent.com/SukkoPera/OpenKickstartSwitcher/master/doc/render-top.png)

### Summary
OpenKickstartSwitcher is a Kickstart switcher for Amiga computers, based on [work by Henryk Richter](http://bax.comlab.uni-rostock.de/en/hardware/amiga500/kickstart-eprom/). It allows switching among three different Kickstart images, stored in a 27c800 or similar EPROM. In particular, the adapter supports 2x256 kilobyte Kickstart images (i.e.: up to version 1.3) and 1x512 kilobyte image (versions 2.0x and later).

Switching among Kickstart versions can be done through two physical switches or through an external add-on board that is controlled by the status of the mouse buttons at power-up (TBA).

The adapter is mostly targeted at Amiga 500+ users, which can use it to switch among Kickstart 2.04 (0r 3.x at their will), 1.3 and maybe [a diagnostic ROM](http://www.diagrom.com), achieving a high level of compatibility with troublesome software that does not work correctly on Kickstart 2.x. It will work correctly on other Amiga versions as well though, as long as it physically fits in place of the original Kickstart ROM.

OpenKickstartSwitcher is also compatible with the infamous A500 Rev.5 board, which has a routing error on one of the Kickstart ROM address lines.

### Assembly
Solder all components to the board. No particular order is recommended, but starting with the smaller components might be a good idea.

The value of the two single resistors is not critical, 10k is recommended, but probably any value between 5k and 50k will do.

The two resistor arrays should be of the *bussed* type and the recommended value is 4.7k. Note that these arrays will end up in parallel to RP106 and RP107 on A500 boards, so you can (or should?) skip them if those are already populated, as should be the case with Rev.6A boards.

The access time of the EPROM is not too critical either. It is recommended to use 100ns or faster EPROMs, but anything up to 150ns should work reliably.

When flashing the EPROM, make sure that the ROM images you are using are exactly 2x262144 and 1x524288 bytes long, and just concatenate them, with the smaller ROMs first.

### Installation
Installation is pretty straightforward:
* Program your EPROM.
* Plug it into your OpenKickStartswitcher.
* Set the jumper on OpenKickstartSwitcher so that it reflects the type of mainboard your Amiga has: one position is for A500 Rev.5, the other one is for all other cases.
* Open your Amiga.
* Remove the shielding.
* Identify the Kickstart chip.
* Carefully remove it.
* Plug OpenKickstartSwitcher in its place, making sure to match the correct orientation.
* Drill two holes into the back of your Amiga (or wherever you prefer) and screw two switches in there.
* Solder wires to switches.
* Replace your shielding.
* Close your Amiga.

### Kickstart selection
To switch between ROMs, you will need two switches, connected to the SW1/SW2 pads. A ground pad is available on the board, but any ground spot on the Amiga board can be used as well, if easier to reach. Then:

* If SW2 is HIGH, the 512 KB Kickstart image is selected.
* If SW2 is LOW, SW1 controls which one of the two 256 KB images is enabled: LOW selects the first one, and HIGH selects the second one.

Note that SW1/SW2 will both read as HIGH if left unconnected.

**IMPORTANT: ALWAYS TURN YOUR AMIGA OFF BEFORE MOVING THE SELECTION SWITCHES.**

### EEPROM Programming
Note that the 27C800 is a 42-pin EPROM, and most programmers only support chips up to 40 pins. This is the case with the popular TL866 programmer, for instance. You can get around this limitation with an adapter PCB. There are at least two open designs of such an adapter, which I haven't tested yet, so use at your own risk:
* [One by keirff](https://github.com/keirf/PCB-Projects) (who, interestingly, has its own Kickstart Switcher)
* [And another one by gaggi](https://github.com/gaggi/27c160-tl866-adapter)

### License
OpenKickstartSwitcher is Open Hardware.

### Thanks
Thanks to Henryk Richter and the guys at the Italian Amiga Page forum.
