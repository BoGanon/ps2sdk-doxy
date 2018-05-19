@mainpage IOP Input/Output Processor

[TOC]

@section iop_lib IOP Libraries
The libraries that come with ps2sdk for the IOP.

Name        | Function
----------- | --------
debug       | Debug libraries
dev9        | Dev9 libraries
fs          | Filesystem libraries
hdd         | HDD libraries
iLink       | iLink libraries
kernel      | The IOP kernel
memorycard  | Memorycard libraries
network     | Network libraries
sound       | Sound libraries
system      | System libraries
tcpip       | TCPIP libraries
usb         | USB libraries


@subsection iop_debug Debug
Libraries that can be used for debugging.

Name        | Function
----------- | --------
iopdebug    | IOP debugging library
iop_sbusdbg | IOP debugging over SBUS tty
ioptrap     | IOP exception handling
sior        | IOP serial I/O

@subsection iop_dev9 DEV9
Libraries that utilize the DEV9 expansion port.

Name        | Function
----------- | --------
atad        | ATA device driver
dev9        | Dev9 device driver
extflash    | External Flash Rom driver
hdpro_atad  | HD Pro Kit ATA device driver
poweroff    | Poweroff handling


@subsection iop_fs Filesystems
Libraries for filesystem handling.

Name        | Function
----------- | --------
devfs       | devfs: filesystem driver
filexio     | fileXio server side
http        | http: client file driver
netfs       | TCP filesystem server for network clients

@subsection iop_hdd HDD
Libraries that provide Hard Disk Drive functionality.

Name    | Function
------- | --------
apa     | ps2hdd driver
apa-osd | OSD version of ps2hdd driver
libapa  | ps2hdd library
libpfs  | pfs library
pfs     | pfs driver
pfs-osd | OSD version of pfs driver

@subsection iop_ilink iLink
Libraries that utilize the iLink interface.

Name          | Function
------------- | --------
IEEE1394_disk | SBP-2 over IEEE1394 driver. See README for more information.
iLinkman      | iLink port driver. See README for more information.

@subsection iop_mc Memory Card
Libraries that provide memory card functionality.

Name   | Function
------ | --------
mcman  | Memory card filesystem manager
mcserv | Memory card RPC server

@subsection iop_network Network
Libraries that provide network functionality.

Name   | Function
------ | --------
netman | Network device manager
smap   | Ethernet interface driver
smbman | SMB protocol driver
udptty | TTY output driver over ethernet

@subsection iop_sound Sound
Libraries that provide sound playback functionality.

Name   | Function
------ | --------
ahx    | AHX replayer
audsrv | audsrv IOP server
freesd | LIBSD compatible sound driver (now libsd)
libsd  | LIBSD compatible sound driver
ps2snd | IOP sound driver for libsd

@subsection iop_system System
Libraries that provide system or device functionality.

Name     | Function
-------- | --------
alloc    | Memory management for the IOP
freemtap | Multitap driver (now mtapman)
freepad  | Controller driver (now padman)
freesio2 | XSIO2MAN replacement driver (now sio2man)
iomanx   | Input/Output filesystem management
iopmgr   | IOP manager
mtapman  | Multitap driver
padman   | Controller driver
rmman    | Remote manager
rmtapman | mtapman with remote support
rpadman  | padman with remote support
rsio2man | ROM1:SIO2MAN replacement driver with remote support
sbusintr | sbus interrupts
siftoo   | SIF2 library
sio2log  | XSIO2MAN replacement driver with logging
sio2man  | XSIO2MAN replacement driver


@subsection iop_tcpip TCPIP
Libraries that provide a TCP/IP stack on the IOP.

Name         | Function
------------ | --------
tcpip        | TCPIP protocol stack library
tcpip-base   | TCPIP base library
tcpip-netman | TCPIP protocol stack library
tcpips       | RPC server for TCPIP protocol

@subsection iop_usb USB
Libraries that provide USB functionality.

Name     | Function
-------- | --------
camera   | PS2 Camera driver
keyboard | USB keyboard driver
mouse    | USB mouse driver
usbd     | USB protocol driver
usbhdfsd | USB mass storage driver

