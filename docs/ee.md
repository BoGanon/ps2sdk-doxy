[TOC]

Emotion Engine Libraries {#eelibraries}
========================

Name           | Function
-------------- | --------
debug          | A library for stacktraces and printing to screen for debugging.
dma            | A library for using the DMAC to send and receive dma chains.
draw           | A library for using the GS via the GIF channel to draw.
eedebug        | A library for EE debugging.
erl            | A library for creating relocatable ELFs.
erl-loader     | A loader program for running ERLs.
@ref fontnotes "font"           | A library initially written to document the fontx2 bitmapped font type, popular in Japan.
graph          | A library for setting up the GS framebuffer, video output, VRAM allocation, etc.
@ref inputnotes "input"          | A library for input in a high level object oriented way.
iopreboot      | A library for rebooting the IOP with special encrypted
kernel         | The kernel library that is the core of ps2sdk. Contains patches to fix incompatibilities between various versions of the PS2.
kernel-nopatch | The kernel library with no patches. Useful for creating loaders or resident programs.
libc           | Standard C library.
libgs          | A library for utilizing the DMAC and GS.
libvux         | A library for 3D math utilizing the VU0 SIMD instructions.
math           | A library for single-precision floating point math functions.
math3d         | A library for 3D math utilizing the VU0 SIMD instructions.
mpeg           | A library for MPEG video decoding utilizing the IPU, DMAC, Scratchpad RAM, and MMI SIMD instructions.
@ref networknotes "network"        | Libraries for network support.
@ref packetnotes "packet"         | A library for creating DMA chains.
@ref rpcnotes "rpc"            | The Remote Procedure Call (RPC) client libraries for server side libraries running on the IOP.
sbv            | A library for controlling the IOP and a collection of patches to overcome limitations in the PS2 BIOS.
startup        | This directory contains the crt0.s and linkfile for compiling and linking binaries for the EE.

---

Font Notes {#fontnotes}
==========
## FontX2
 * Fontx2 fonts can be single byte JISCII but can also have double byte Shift-JIS.
 * The rom0:KROM file in the bios is a fontx2 font that supports both.
 * The print functions support Shift-JIS encoded strings.

## FontStudio
FontStudio was a useful font utility for compressing UTF-8 variable width Truetype fonts into a small image. Then, using pngquant, the texture could be further compressed down to 4-bit.

Unfortunately, it seems to have disappeared.

---

Input Notes {#inputnotes}
===========
An example of getting a controller, using it, and freeing it.

```C
// Unlocked means the analog can be turned on or off
pad_t *pad1 = pad_open(0,0,MODE_UNLOCK);

// Wait for pad to be ready
pad_wait(pad1);

// Read buttons
pad_get_buttons(pad1);

// The btns bits. 0 means pressed. 1 means unpressed.
if ((pad1->buttons.btns ^ 0xffff) & PAD_LEFT)
  printf("Left is pressed");

// Enable force feedback
pad_init_actuators(pad1);

// Turn on small motor
pad_set_actuators(pad1,1,0);

// Set large motor to 50% (0-255)
pad_set_actuators(pad1,1,128);

// Stop force feedback
pad_set_actuators(pad1,0,0);

// Free the pad
pad_close(pad1);
```

---

Network Notes {#networknotes}
=============
Name   | Function
------ | --------
netman | A network manager for network support. See NETMAN.txt.
tcpip  | A port of lwip for TCP/IP stack support.

---

Packet Notes {#packetnotes}
============
A packet consists of:

Member | Function
------ | --------
qwords | the number of qwords allocated
qwc    | the number of qwords in the dma chain
type   | the type of address space allocated
data   | the address of the allocated qwords

## Errata
packet_increment_qwc() is an unimplemented stub.

## Usage
The samples in the graph and draw libraries have some examples for building DMA chains.

---

RPC Notes {#rpcnotes}
=========
The Remote Procedure Call (RPC) client libraries for server side libraries running on the IOP.

Versions with 'x' in the name are updated versions with extended functionality.

Name       | Function
---------- | --------
ahx        | Replaying AHX files
audsrv     | Audio playback support. WAV, ADPCM, CDDA
camera     | PS2 camera via USB support
cdvd       | Disc drive support
fileio     | Filesystem I/O handling
filexio    | Filesystem I/O handling with extended functionality (IOMANX)
hdd        | Hard disk support such as formatting and partition information
keyboard   | USB keyboard support
memorycard | Memory card support
mouse      | USB mice support
multitap   | Multitap support
pad        | Controller input support
padx       | Controller input support, supports multitap
poweroff   | Handles powering off the PS2
ps2snd     | Using libsd and playing back ADPCM
remote     | PS2 remote support
sior       | Serial I/O support
tcpips     | TCP/IP stack support
xcdvd      | Disc drive support

---

Terminology {#terms}
===========

Term  | Definition
----- | ----------
DMAC  | DMA controller
EE    | Emotion Engine is the main processor
GS    | Graphics Synthesizer
IOP   | The Input/Output processor
IPU   | Image Processing Unit for MPEG-2 decoding
VU    | Vector Units for vector math and geometry
GIF   | The DMA interface for the GS
SIF   | The DMA interface between EE and IOP
VIF0  | The DMA interface for VU0
VIF1  | The DMA interface for VU1
IRX   | IOP executable
MMI   | Multimedia SIMD Instructions
QWORD | A 16-byte (128-bit) data type
RPC   | Remote procedure call

---

