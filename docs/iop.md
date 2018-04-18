[TOC]

Input/Output Processor Libraries {#ioplibraries}
========================

Name                      | Function
------------------------- | --------
@ref iopdebug "debug"     | Debug libraries
@ref iopdev9 "dev9"       | Dev9 libraries
@ref iopfs "fs"           | Filesystem libraries
@ref iophdd "hdd"         | HDD libraries
@ref iopiLink "iLink"     | iLink libraries
kernel                    | The IOP kernel library
@ref iopmc "memorycard"   | Memorycard libraries
@ref iopnetwork "network" | Network libraries
@ref iopsound "sound"     | Sound libraries
@ref iopsystem "system"   | System libraries
@ref ioptcpip "tcpip"     | TCPIP libraries
@ref iopusb "usb"         | USB libraries

---

Debug {#iopdebug}
=====

Name        | Function
----------- | --------
iopdebug    | IOP debugging library
iop_sbusdbg | IOP debugging over SBUS tty
ioptrap     | IOP exception handling
sior        | IOP serial I/O

---

Dev9 {#iopdev9}
====

Name       | Function
---------- | --------
atad       | ATA Device Driver
dev9       | Dev9 Device Driver
extflash   | External Flash Rom Driver
hdpro_atad | HD Pro Kit ATA Device Driver
poweroff   | Poweroff handling

---

Filesystem {#iopfs}
==========

Name     | Function
-------- | --------
devfs    | devfs: filesystem driver
fakehost | Redirects a path to a fake host: device
filexio  | fileXio server side
http     | http: client file driver
netfs    | TCP server for network clients

---

HDD {#iophdd}
===

Name    | Function
------- | --------
apa     | ps2hdd driver
apa-osd | OSD version of ps2hdd driver
libapa  | ps2hdd library
libpfs  | pfs library
pfs     | pfs driver
pfs-osd | OSD version of pfs driver

---

iLink {#iopiLink}
=====

Name          | Function
------------- | --------
IEEE1394_disk | SBP-2 over IEEE1394 driver. See README for more information.
iLinkman      | iLink port driver. See README for more information.

---

Memorycard {#iopmc}
==========

Name   | Function
------ | --------
mcman  | Memory card manager
mcserv | Memory card RPC server

---

Network {#iopnetwork}
=======

Name   | Function
------ | --------
netman | Network device manager
smap   | Ethernet interface driver
smbman | SMB protocol driver
udptty | TTY output driver over ethernet

Sound {#iopsound}
=====

Name   | Function
------ | --------
ahx    | AHX replayer
audsrv | audsrv IOP server
freesd | LIBSD compatible sound driver (now libsd)
libsd  | LIBSD compatible sound driver
ps2snd | IOP sound driver for libsd

---

System {#iopsystem}
======

Name     | Function
-------- | --------
alloc    | Memory management for IOP
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

---

TCPIP {#ioptcpip}
=====

Name         | Function
------------ | --------
tcpip        | TCPIP protocol stack library
tcpip-base   | TCPIP base library
tcpip-netman | TCPIP protocol stack library
tcpips       | RPC server for TCPIP protocol

---

USB  {#iopusb}
===

Name     | Function
-------- | --------
camera   | PS2 Camera driver
keyboard | USB keyboard driver
mouse    | USB mouse driver
usbd     | USB protocol driver
usbhdfsd | USB mass storage driver

---

