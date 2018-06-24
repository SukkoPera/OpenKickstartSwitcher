# OpenKickstartSwitcher
OpenKickstartSwitcher is an Open Hardware Triple Kickstart Switcher for Amiga Computers.

![Board](https://raw.githubusercontent.com/SukkoPera/OpenKickstartSwitcher/master/doc/render-top.png)

### Summary
OpenKickstartSwitcher is a Kickstart switcher for Amiga computers, based on [work by Henryk Richter](http://bax.comlab.uni-rostock.de/en/hardware/amiga500/kickstart-eprom/). It allows switching among three different Kickstart images, stored in a 27C800 or similar EPROM. In particular, the adapter supports 2x256 KB Kickstart images (i.e.: up to version 1.3) and 1x512 KB image (versions 2.0x and later).

Switching among Kickstart versions can be done through two physical switches or through an external add-on board that is controlled by the status of the mouse buttons at power-up (TBA).

The adapter is mostly targeted at Amiga 500+ users, which can use it to switch among Kickstart 2.04 (0r 3.x at their will), 1.3 and maybe [a diagnostic ROM](http://www.diagrom.com), achieving a high level of compatibility with troublesome software that does not work correctly on Kickstart 2.x. It will work correctly on other Amiga versions as well though, as long as it physically fits in place of the original Kickstart ROM, so it can also be useful on the 600 and 2000.

OpenKickstartSwitcher is also compatible with the infamous A500 Rev.5 board, which has a routing error on one of the Kickstart ROM address lines.

### Assembly
Solder all components to the board. No particular order is recommended, but starting with the smaller components might be a good idea.

The value of the two single resistors is not critical, 10k is recommended, but probably any value between 5k and 50k will do.

My tests show that an SN74HC00 gate works fine. I don't recommend using parts from the *HC* series though, *HCT* or *LS* should be preferred.

The two resistor arrays are not always needed. First of all, these will end up in parallel to RP106 and RP107 on A500 boards, so you must skip them if those are already populated on your particular board. If they are not, you might still get away without them, depending on the particular EPROM you are using: I have several EPROMs of the same model (but different production batches), and some need the resistors while others don't, so the only way to find out is actual testing. For this I usually just load a Kickstart 1.2 disk, start up the four *Demos* and leave them running for a while. If the system does not hang/crash in like 15 minutes (usually it is much quicker than that, sometimes it even hangs before you can start all the demos!), you don't need them, otherwise you do. If you decide to install them, they must be of the *bussed* type and the recommended value is 4.7k.

### EPROM Programming
I recommend using M27C800-100F1 EPROMs by ST. The access time of the EPROM is not critical: use 100ns or faster EPROMs if you can, but anything up to 150ns should work reliably.

When flashing the EPROM, make sure that the ROM images you are using are exactly 2x262144 and 1x524288 bytes long, and just concatenate them, with the smaller ROMs first. You must also take care to use the correct byte ordering, as the Amiga hardware expects 16-bit words to be stored in the *big-endian* format (which is NOT the format UAE expects them in, for the record).

Note that the 27C800 is a 42-pin EPROM, and most programmers only support chips up to 40 pins. This is the case with [the popular TL866 programmer](http://autoelectric.cn/EN/TL866_main.html), for instance. You can get around this limitation with an adapter PCB. There are at least two open designs of such an adapter:
* [One by keirff](https://github.com/keirf/PCB-Projects) (who, interestingly, has its own Kickstart Switcher)
* [And another one by gaggi](https://github.com/gaggi/27c160-tl866-adapter)

I have only used the latter and found it to be working fine.

### Installation
Once your OpenKickstartSwitcher is assembled and programmed, the rest of the installation should be pretty straightforward:
* Open your Amiga.
* Remove the shielding.
* Identify the mainboard revision by looking at the bottom right corner near the floppy drive zone.
* Set the jumper on OpenKickstartSwitcher so that it reflects the type of mainboard your Amiga has: one position is for A500 Rev.5, the other one is for all other cases.
* Identify the Kickstart chip.
* Carefully remove it.
* Plug OpenKickstartSwitcher in its place, making sure to match the correct orientation.
* Drill two holes into the back of your Amiga (or wherever you prefer) and screw two switches in there.
* Solder wires to switches.
* Replace your shielding.
* Close your Amiga.

### Kickstart selection
To switch between ROMs, you will need two switches, connected to the SW1/SW2 pads. A ground pad is available on the board, but any ground spot on the Amiga board can be used as well, if easier to reach. Then:

* If SW2 is HIGH, the 512 KB Kickstart image is selected, regardless of SW1.
* If SW2 is LOW, SW1 controls which one of the two 256 KB images is enabled: LOW selects the first one, and HIGH selects the second one.

Note that SW1/SW2 will both read as HIGH if left unconnected, so the 512 Kickstart will be selected if no switches are wired.

**IMPORTANT: ALWAYS TURN YOUR AMIGA OFF BEFORE MOVING THE SELECTION SWITCHES.**

### License
OpenKickstartSwitcher is Open Hardware. If you make any modifications to the board, please contribute them back.

### Support the Project
Since the project is open you are free to get the PCBs made by your preferred manufacturer, however in case you want to support the development, you can order them from PCBWay through this link:

[![PCB from PCBWay](https://www.pcbway.com/project/img/images/frompcbway.png)](https://www.pcbway.com/project/shareproject/OpenKickstartSwitcher_V2.html)

You get cheap, professionally-made and good quality PCBs, I get some credit that will help with this and [other projects](https://www.pcbway.com/project/member/shareproject/?bmbid=41100). You won't even have to worry about the various PCB options, it's all pre-configured for you!

Also, if you still have to register to that site, [you can use this link](https://www.pcbway.com/setinvite.aspx?inviteid=41100) to get some bonus initial credit (and yield me some more).

Again, if you want to use another manufacturer, feel free to, don't feel obligated :).

### Get Support
If you need help or have questions, you can join [the official Telegram group](https://t.me/joinchat/HUHdWBC9J9JnYIrvTYfZmg).

### Thanks
Thanks to Henryk Richter and the guys at the Italian Amiga Page forum.
