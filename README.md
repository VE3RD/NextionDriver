
NextionDriver (for MMDVMHost) by ON7LDS Version 1.25 Repair by VE3RD
=======================================

The current NextionDriver ver 1.25 by ON7LDS has a few minor errors
The location detail for DMR TS1 or any other modes is broken
The following are the changes I made to mske this code work

The Why
There are two sections of code to lookup location detail. One for DMR TS2 and one for everything else
DMR TS2 uses T2=2 N CallSign
DMR TS1 uses T0=1 N CallSign
P25,YSF and NXDN use T0=N CallSign
The buffer configuration for DMR is TXbuffer[12] to grab the Callsign from position 12
The buffer for the other modes needs to be TXbuffer[10] not TXbuffer[12] to grab the Callsign from position 10
This creates a conflick between DM TS1 and the other modes

The What
I added a logic element to stop the other modes block from processing if the mode was DMR and changed all the TXbuffer[12]s TXbuffer[10] in that block.
I duplicated the DMR block for TS2 and adjusted it for TS1

The When
This is a TEMPORARY fix for the ON7LDS Driver that will dissapear when ON7LDS posts a repaired version of his NextionDriver
I have set the version number to R1.25

Phil VE3RD

NextionDriver (for MMDVMHost) by ON7LDS
=======================================

Find the last version on https://github.com/on7lds/

```
Latest version : 1.21 (aug 2021)
* split contfiguration files :  
  it is possible (but not manadtory) to move all [NextionDriver] settings  
  to a separate configuration file (use the -C option for this new file)  
* minor corrections

TAKE NOTE:  
  the default filename or the users file (DMRidFile)  
  is changed from stripped.csv to users.csv as of V1.20!
```

  
  
The purpose of this program is to provide additional control for
Nextion display layouts other than the MMDVMHost supplied layouts.
It does this by sitting between MMDVMHost and the Nextion Display.
This program takes the commands, sent by MMDVMHost and translates,
changes, adds or removes these commands. 
On top of that, it can also process commands from the display and 
execute corresponding commands on the host.


Since the program has to read the MMDVMHost configuration file
(MMDVM.ini or /etc/mmdvmhost on PiStar) to know the Layout (for
setting the baudrate) and other parameters (i.e. for knowing
the frequency and location), the parameters for the NextionDriver
itself are also located in the MMDVM configuration file,
in an extra section [NextionDriver].

As stated above, the NextionDriver program will change the commands
as needed and adds extra info (e.g. temperature, TG's info, ...) 
and sends this to the Nextion display.

This program also checks the network interface regularly, and it will
show the most recent IP address, so you can check if the IP address
changed.

When the files 'groups.txt' and 'users.csv' are present, usernames
and talkgroup names will be looked up and sent to the display. 
NOTE : both files have to be sorted in ascending ID order ! 


The program also has the ability of receiving commands from the Nextion
display. This way, one can provide buttons on a layout and do something
in the host when such a button is pressed.
One could, for example, make a 'system' page on the Nextion with system
info and buttons to restart MMDVMHost, reboot or poweroff the host, ...

Yes, it is possible (when NextionDriver is running) to start/stop/restart
MMDVMHost with buttons on the Nextion display !

When the Nextion display is connected to the serial port of the modem,
NextionDriver V1.03 and later is able to address that port. 
How does this work ?
Normally, the data to the display goes directly from MMDVMHost to the
modem, tagged as data for the serial port. The modem will then pass the
data to the serial port.
By enabling transparent data, we are able to inject data into MMDVMHost
and we will tag it as data for the display (this can only be done by
setting sendFrameType=1 in the configuration file).

Data from the Nextion (when pressing buttons) will be treated similar and
will exit MMDVMHost as transparent data.
***IMPORTANT*** : the firmware of the modem has to pass data from the display
to MMDVMHost for this to work!


- [How to use the NextionDriver](README-using.md "How to use the NextionDriver")
- [Modem connected displays](README-modemdisplays.md "Modem connected displays")
- [Autostart NextionDriver](README-starting.md "Autostart NextionDriver")
- [Configuration file options](README-options.md "Configuration file options")
- [Sending commands from display to host](README-commands.md "Sending commands from display to host")
- [Change the program by coding yourself](README-coding.md "Change the program by coding yourself")

