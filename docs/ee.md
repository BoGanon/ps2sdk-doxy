
@defgroup file_io File I/O
@details File input and output on the EE.
@defgroup libfileio FILEIO: EE FILEIO RPC Client
@ingroup file_io
@defgroup libfileXio FileXio: EE FileXio RPC Client
@ingroup file_io
@defgroup fio_stat File I/O file modes and types
@ingroup libfileio libfileXio

@defgroup libkernel Kernel
@details The core library of the EE.
@defgroup cache Cache
@details When sharing cached memory with other processors, it is a good idea to
    writeback the data cache so the memory contains the latest data. When
    accessing data from a DMA transfer from other processors, it is a good idea
    to invalidate the data cache to make sure a fresh copy of the data is
    fetched from memory. For the instruction cache, invalidate it after
    rewriting a place in memory that holds instructions.
@ingroup libkernel
@defgroup interrupt Interrupts
@details Functions dealing with interrupts provided by the EE kernel.
@ingroup libkernel
@defgroup semaphore Semaphores
@details Functions dealing with semaphores provided by the EE kernel.
@ingroup libkernel
@defgroup timer Timers
@details Hardware timers on the EE.
@ingroup libkernel
@defgroup thread Threads
@details Functions dealing with threads provided by the EE kernel.
@ingroup libkernel
@defgroup loadfile EE Loadfile: ELF and IRX loader client library.
@details Functions dealing with loading IOP modules or ELF files.
@ingroup libkernel

@defgroup rpc_main Remote Procedure Call
@defgroup audsrv audsrv: Audio playback library.
@ingroup rpc_main
@defgroup libcdvd libcdvd: CDVD library.
@ingroup rpc_main
@defgroup libmc libmc: memorycard library.
@ingroup rpc_main
@defgroup libpad libpad: pad input library.
@ingroup rpc_main

@defgroup sbvpatches SBV Patches

@mainpage EE Emotion Engine

[TOC]

@section ee_lib Emotion Engine Libraries
The libraries that come with ps2sdk for the EE.

Name           | Function
-------------- | --------
debug          | A library for stacktraces and printing to screen for debugging.
dma            | A library for using the DMAC to send and receive dma chains.
draw           | A library for using the GS via the GIF channel to draw.
eedebug        | A library for EE debugging.
erl            | A library for creating relocatable ELFs.
erl-loader     | A loader program for running ERLs.
font           | A library initially written to document the fontx2 bitmapped font type, popular in Japan.
graph          | A library for setting up the GS framebuffer, video output, VRAM allocation, etc.
input          | A library for input in a high level object oriented way.
iopreboot      | A library for rebooting the IOP with special encrypted
kernel         | The kernel library that is the core of ps2sdk. Contains patches to fix incompatibilities between various versions of the PS2.
kernel-nopatch | The kernel library with no patches. Useful for creating loaders or resident programs.
libgs          | A library for utilizing the DMAC and GS.
libvux         | A library for 3D math utilizing the VU0 SIMD instructions.
math           | A library for single-precision floating point math functions.
math3d         | A library for 3D math utilizing the VU0 SIMD instructions.
mpeg           | A library for MPEG video decoding utilizing the IPU, DMAC, Scratchpad RAM, and MMI SIMD instructions.
network        | Libraries for network support.
packet         | A library for creating DMA chains.
rpc            | The Remote Procedure Call (RPC) client libraries for server side libraries running on the IOP.
sbv            | A library for controlling the IOP and a collection of patches to overcome limitations in the PS2 BIOS.
startup        | This directory contains the crt0.s and linkfile for compiling and linking binaries for the EE.

@subsection ee_network Network
Libraries for network support.
Name   | Function
------ | --------
netman | A network manager for network support. See NETMAN.txt.
tcpip  | A port of lwip for TCP/IP stack support.

@subsection ee_rpc RPC
The Remote Procedure Call (RPC) client libraries for server side libraries
running on the IOP.

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

@section ee_terms Terminology


Term   | Definition
------ | ----------
DMAC   | DMA controller
EE     | Emotion Engine is the main processor
GS     | Graphics Synthesizer
IOP    | The Input/Output processor
IPU    | Image Processing Unit for MPEG-2 decoding
VU     | Vector Units for vector math and geometry
GIF    | The DMA interface for the GS
SIF    | The DMA interface between EE and IOP
VIF0   | The DMA interface for VU0
VIF1   | The DMA interface for VU1
IRX    | IOP executable
MMI    | Multimedia SIMD Instructions
%QWORD | A 16-byte (128-bit) data type
RPC    | Remote procedure call
X*     | Denotes a later version of an IOP module


@page file_over Overview

@ingroup file_io
@{

@section Libraries
There are two file I/O libraries provided with ps2sdk. Most file I/O is done
generally by using a device driver on the IOP and communicating to it through
the SIF RPC interface. 

@subsection FILEIO
The @ref libfileio "FILEIO" library provides basic functionality through
rom0:XFILEIO in the bios. Newer versions of XFILEIO are incompatible with
the EE RPC client protocol in ps2sdk. 

**IRX Modules:**
    @li rom0:IOMAN
    @li rom0:XFILEIO

@note These modules are not provided by early Japanese models.

@subsection FileXio
The @ref libfileXio "fileXio" library provides extended functionality through
iomanX.irx and fileXio.irx in ps2sdk.

**IRX Modules:**
    @li iomanX.irx
    @li fileXio.irx

@section paths Paths
This is how a pathname generally looks.

      "<device><unit>:<path>"

 @li @c device is the device specifier.
 @li @c unit is a number specifying the specific device, sometimes optional.
 @li @c : is the separator between the device and the path on the device.
 @li @c path is the path on the device.

@section Devices
Each device on the IOP define their own implementations for the following
functions. Their behavior is similar to the related POSIX functions but
return values are negatively signed errno codes on failure.

```c
    int open(const char *path, int flags, int mode);
    int close(int fd);
    int read(int fd, void* buf, int size);
    int write(int fd, void *buf, int size);
    int lseek(int fd, int offset, int whence);
    int ioctl(int fd, int request, void *buf);
    int remove(const char *path);
    int mkdir(const char *path, int mode);
    int rmdir(const char *path);
    int dopen(const char *path);
    int dclose(int fd);
    int dread(int fd, void *buf);
    int getstat(const char *path, void *buf);
    int chstat(const char *path, void *buf, unsigned int mask);
    int format(const char *dev, const char *block, void *arg, int arglen);
    int rename(const char *old_name, const char *new_name);
    int chdir(const char *name);
    int sync(const char *device, int flag);
    int mount(const char *mnt, const char *src, int flag, void *arg, int arglen);
    int umount(const char *mnt);
    long long lseek64(int fd, long long offset, int whence);
    int devctl(const char *name, int cmd, void *arg, unsigned int arglen, void *buf, unsigned int buflen);
    int symlink(const char *old, const char *new);
    int readlink(const char *path, char *buf, unsigned int buflen);
    int ioctl2(int fd, int cmd, void *arg, unsigned int arglen, void *buf, unsigned int buflen);
```

@subsection mcards Memory Cards

**IRX Modules:**
@li sio2man.irx
@li mcman.irx
@li mcserv.irx

@par Path:

      "mc<unit>:<path>"

See @ref libmc for more details.

@subsection mass USB Mass Storage Devices

**IRX Modules:**
@li usbd.irx
@li usbhdfsd.irx

@par Path:

      "mass<unit>:<path>"

  @note The unit specifier is optional if only accessing the first connected
        device. E.g "mass:/"

  @note Supports up to two devices with 4 primary partitions.

  @attention It takes a few seconds to warm up and initialize USB devices.
             Introduce a delay prior to accessing files on a USB mass
             storage device after loading the usbd and usbhdfsd IRX modules.

@subsection hdd Hard Disk Drives

**IRX Modules:**
@li ps2dev9.irx
@li ps2atad.irx (or hdproatad.irx for the HDPro Kit)
@li ps2hdd.irx
@li ps2fs.irx

The ps2hdd module has two arguments.
      @li @c -o for max open files (default 1)
      @li @c -n for number of caches (default 3)

The ps2fs module has three arguments.
      @li @c -m max mounts allowed (default 1)
      @li @c -o max open files (default 2)
      @li @c -n number of buffers (default 8) (add two per open file)

@par Path:

      "hdd<unit>:<name>,<fp>,<rp>,<sz>,<PFS>"

 @li @c name is the name of the partition.
 @li @c fp is a string indicating the full access password.
 @li @c rp is a string indicating the read only password.
 @li @c sz is a string indicating size when creating partitions.
 @li @c PFS is the type of partition to open, PFS, CFS, EXT2, EXT2SWAP.

@par Example:
Open the partition table and read an entry.
```c
    int fd = fileXioDopen("hdd0:");
    fileXioDread(fd, &io_stat);
    fileXioDclose(fd);
```

@par Example:
Create a 4GB sized +MYPART partition using the PFS format without a password.
```c
    fileXioOpen("hdd0:+MYPART,,,4G,PFS",IO_CREAT|IO_RDWR);
```

@par Example:
Mount the +MYPART partition read only.
```c
   fileXioMount("pfs0:","hdd0:+MYPART",IO_RDONLY);
```

@par Example:
Unmount the +MYPART partition.
```c
   fileXioUmount("pfs0:");
```

@note The general convention is to use a '+' sign to indicate a partition
      that isn't related to official games or system use.

@attention It takes a while for hard disk drives to initialize so introduce
           a delay prior to accessing a hard disk or hard disk partition.

See @ref libhdd.c for more detailed usage.
@}

@page kernel_main Overview

@ingroup libkernel
@{
Based on the EE kernel emulation in the Play! PS2 Emulator and my own tests.

@section sema_main Semaphores
Synchronization on the EE is provided by semaphores. Semaphores have a wait
queue for threads when the resource is used.

@subsection sema_attr Attributes
@par sema.count
Filled by ReferSemaStatus(). The current count.

@par sema.max_count
The number of times the semaphore can be used.

@par sema.init_count
The initial count value when creating the semaphore.

@par sema.wait_threads
The number of threads waiting on the semaphore.

@par sema.option
A pointer to user data. E.g. A string constant describing its use.

@subsection sema_mutex Mutexes
A mutex is a semaphore that allows only one running thread into a critical
section of code.

@par sema.max_count
Set the max count to 1.

@par sema.init_count
To create a mutex locked, set the init_count to 0.

@par sema.init_count
To create a mutex unlocked, set the init_count to 1.

@subsection sema_using Using Semaphores
The functions with a lowercase 'i' should be used when interrupts are
disabled like when in an interrupt handler.
```c
int CreateSema(ee_sema_t *sema);
```
Returns the id of the semaphore.
```c
int WaitSema(int id);
```
A thread calls WaitSema() decreasing the count using the resource. When another
thread calls WaitSema(), if the count is 0, that thread is put into the
semaphore's wait queue.
```c
int SignalSema(int id);
int iSignalSema(int id);
```
A thread calls SignalSema() increasing the count returning the resource. The
next thread waiting in the semaphore's queue is run.
```c
int PollSema(int id);
int iPollSema(int id);
```
A thread calls PollSema() decreasing the count using the resource. 
If the count is already zero, it does not put the thread calling PollSema()
into a wait state, but returns an error.

Using PollSema() prior to WaitSema() on a semaphore acting as a mutex can
create a race condition.

@par E.g.
A thread calls SignalSema() on a semaphore, then a thread using
PollSema() uses the resource. WaitSema() then puts the next thread into
wait status. No other threads are in the critical section of code to call
SignalSema() to free the resource.

```c
int DeleteSema(int id);
int iDeleteSema(int id);
```
After DeleteSema() is called, threads in the semaphore's wait queue are
returned to running status, the semaphore is deleted, and calls referring to
the semaphore return an error.
```c
int ReferSemaStatus(int id, ee_sema_t *sema);
int iReferSemaStatus(int id, ee_sema_t *sema);
``` 
ReferSemaStatus() can be used to check the current count, the max_count, and
number of threads waiting on the semaphore.

@section threads_main Threads
Multithreading on the EE kernel is cooperative. The kernel provides a pool of
256 threads to be used. A few are reserved for fixing bugs and various libraries
on the EE may run their own.

@subsection threads_coop Cooperative Multithreading
Threads with a higher priority have to cede control to other threads. Threads
with a longer amount of execution time will take time away from other threads
since there isn't a regular preemptive schedule.

@subsection threads_attr Attributes

@par thread.status
Status of the thread.

Status      | Effect
----------- | --------
THS_RUN     | Running
THS_READY   | Ready to run
THS_WAIT    | Waiting 
THS_SUSPEND | Suspended
THS_DORMANT | Newly created or terminated

Threads in THS_WAIT state can be suspended, too.

@par thread.func
Function for the thread to run.

@par thread.stack
Memory aligned to 16 byte boundary to use as stack.

@par thread.stack_size
Since the stack is 16-byte aligned, size is a multiple of 16.

@par thread.gp_reg
Pointer to global offset (the symbol _gp is defined by the linkscript).

@par thread.initial_priority
Initial priority when using CreateThread(). 0 - 127 (lower number is higher
priority, but 0 is reserved by the kernel).

@par thread.current_priority
Filled by ReferThreadStatus(). Contains the thread's current priority.

@par thread.option
Pointer to user data. Documented not to work.

@par thread.waitType
Filled by ReferThreadStatus(). Contains why the thread is waiting.

Type        | Reason
----------- | --------
THS_WT_NONE | Not waiting 
THS_WT_WAKE | Waiting for wakeup  
THS_WT_SEMA | Waiting for semaphore

If a thread state is THS_WAIT and the wait type is THS_WT_WAKE, then the thread
has been put to sleep using SleepThread().

@par thread.waitId
Filled by ReferThreadStatus(). Contains the semaphore's ID if waiting on a
semaphore.

@par thread.wakeupCount
Filled by ReferThreadStatus(). Contains the number of times other threads have
tried to wake up the thread when it wasn't sleeping.

@subsection threads_using Using Threads
The functions with a lowercase 'i' should be used when interrupts are
disabled like when in an interrupt handler.
```c
int CreateThread(ee_thread_t *thread);
```
Create the thread and put it into THS_DORMANT state. Returns thread's id on
success.
```c
int DeleteThread(int id);
```
Deletes THS_DORMANT thread from another thread.
```c
int StartThread(int id);
```
Starts a THS_DORMANT thread.
```c
void ExitThread(void);
```
Changes the calling thread to THS_DORMANT.
```c
void ExitDeleteThread(void);
```
Changes the calling thread to THS_DORMANT then returns it to internal pool.
```c
int SleepThread(void);
```
If the wakeupCount is 0, puts the current thread into THS_WAIT status.
```c
int GetThreadId(void);
```
Returns the id of the current thread.
```c
int TerminateThread(int id);
int iTerminateThread(int id);
```
Changes a thread to THS_DORMANT state from another thread.
```c
int ChangeThreadPriority(int id, int priority);
int iChangeThreadPriority(int id, int priority);
```
Changes a thread's priority and schedules it at the bottom of that priority's
queue
```c
int RotateThreadReadyQueue(int priority);
int iRotateThreadReadyQueue(int priority);
```
Finds first ready or running thread of a given priority and schedules it at the
bottom of the queue.
```c
int ReleaseWaitThread(int id);
int iReleaseWaitThread(int id);
```
Release a thread from THS_WAIT state.
```c
int WakeupThread(int id);
int iWakeupThread(int id);
```
Removes THS_WAIT status from a thread. If the thread isn't in wait status, the
wakeupCount is incremented.
```c
int CancelWakeupThread(int id);
int iCancelWakeupThread(int id);
```
Set thread's wakeupCount to 0.
```c
int SuspendThread(int id);
int iSuspendThread(int id);
```
Suspends a thread, adding THS_SUSPEND to its status.
```c
int ResumeThread(int id);
int iResumeThread(int id);
```
Removes THS_SUSPEND state from a thread.
```c
int ReferThreadStatus(int id, ee_thread_status_t *status);
int iReferThreadStatus(int id, ee_thread_status_t *status);
```
Retrieve the status of a thread.

@section kernel_example Example
This example shows how to implement a preemptive schedule for a group of
threads.

```c
#include <tamtypes.h>
#include <stdio.h>
#include <kernel.h>

// I've provided an alternative wakeup and sleep implementation using
// semaphores.
//#define USE_SEMA

// The global offset pointer
extern void *_gp;

#define SECONDS_TO_RUN 10

// A kilobyte of stack per thread
#define THREAD_STACK_SIZE  1024

volatile int counter = 0;
volatile int executing = 0;

// Scheduler attributes
#define SCHEDULER_PRIORITY 30

// Alarm intervals

// NTSC Frames per second
#define SCHEDULER_SECOND 30

// HBlanks 1/29.96 second NTSC
#define SCHEDULER_TIME 525

// HBlanks 1/30 second NTSC
//#define SCHEDULER_TIME 524

// HBlanks 1/25 second 576i
//#define SCHEDULER_TIME 625
//#define SCHEDULER_SECOND 25

#ifdef USE_SEMA
volatile int  scheduler_sema = 0;
#endif

unsigned char scheduler_stack[THREAD_STACK_SIZE] ALIGNED(16);
int           scheduler_id;

// Threads
unsigned char          thread_a_stack[THREAD_STACK_SIZE] ALIGNED(16);
int                    thread_a_id;
volatile unsigned int  thread_a_cycles = 0;

unsigned char          thread_b_stack[THREAD_STACK_SIZE] ALIGNED(16);
int                    thread_b_id;
volatile unsigned int  thread_b_cycles = 0;


void thread_a(void *arg);
void thread_b(void *arg);

// This scheduler thread could just be replaced with
// iRotateThreadReadyQueue() in the interrupt function.
// Using a thread allows for more flexibility and doesn't affect other threads
// since interrupts are enabled.
void scheduler(void* a)
{
  while(1)
  {

#ifdef USE_SEMA
    WaitSema(scheduler_sema);
#else
    SleepThread();
#endif

    RotateThreadReadyQueue(SCHEDULER_PRIORITY);

    if (counter > SCHEDULER_SECOND * SECONDS_TO_RUN)
      executing = 0;

#ifdef USE_SEMA
    PollSema(scheduler_sema);
#endif

  }
}

void interrupt(s32 id, u16 time, void *arg)
{
  counter++;

#ifdef USE_SEMA
  iSignalSema(scheduler_sema);
#else
  iWakeupThread(scheduler_id);
#endif

  iSetAlarm(SCHEDULER_TIME, interrupt, NULL);

  // Calling this re-enables interrupts properly
  ExitHandler();
}

int main( int argc, char **argv)
{
  volatile unsigned int main_cycles = 0;
  int interrupt_id = -1;

  ee_thread_t thread;

#ifdef USE_SEMA
  ee_sema_t   sema;

  // Create a mutex for the scheduler and indicate that the resource
  // is already being used by setting init_count to 0.
  sema.max_count = 1;
  sema.init_count = 0;
  sema.option = 0;

  if ((scheduler_sema = CreateSema(&sema)) < 0)
    return -1;
#endif

  // Setup scheduler thread which will rotate the running threads
  // Give it a high priority
  thread.func = scheduler;
  thread.stack = scheduler_stack;
  thread.stack_size = THREAD_STACK_SIZE;
  thread.gp_reg = &_gp;
  thread.initial_priority = 1;
  scheduler_id = CreateThread(&thread);

  if (scheduler_id < 0)
    return -1;

  // Start the scheduler thread, it will go straight to wait status
  StartThread(scheduler_id, NULL);

  // Change the priority of the main thread so we know it's higher than
  // the threads we're about to start.
  ChangeThreadPriority(GetThreadId(), SCHEDULER_PRIORITY-1);

  // Create 2 threads for the scheduler to rotate
  thread.func = thread_a;
  thread.stack = thread_a_stack;
  thread.stack_size = THREAD_STACK_SIZE;
  thread.gp_reg = &_gp;
  thread.initial_priority = SCHEDULER_PRIORITY;

  if ((thread_a_id = CreateThread(&thread)) < 0)
  {
    TerminateThread(scheduler_id);
    DeleteThread(scheduler_id);
    return -1;
  }

  thread.func = thread_b;
  thread.stack = thread_b_stack;
  thread.stack_size = THREAD_STACK_SIZE;
  thread.gp_reg = &_gp;
  thread.initial_priority = SCHEDULER_PRIORITY;

  if ((thread_b_id = CreateThread(&thread)) < 0)
  {
    TerminateThread(thread_a_id);
    DeleteThread(thread_a_id);
    TerminateThread(scheduler_id);
    DeleteThread(scheduler_id);
    return -1;
  }


  // Use an interrupt to rotate a queue of threads to give each thread equal
  // slices of cpu time.
  // Use a hardware timer interrupt instead of an alarm for more finetuned
  // control and less overhead
  interrupt_id = SetAlarm(SCHEDULER_TIME, interrupt, NULL);

  // Indicate that we're about to execute parallel threads
  executing = 1;

  // Start threads and change the main thread so it's on the same
  // schedule.
  printf("Starting threads\n");

  StartThread(thread_a_id, NULL);
  StartThread(thread_b_id, NULL);

  ChangeThreadPriority(GetThreadId(),SCHEDULER_PRIORITY);

  while(executing)
  {
    main_cycles++;
  }

  // Threads are done so change the main thread back to a higher priority
  ChangeThreadPriority(GetThreadId(),SCHEDULER_PRIORITY-1);

  TerminateThread(thread_a_id);
  TerminateThread(thread_b_id);

  DeleteThread(thread_a_id);
  DeleteThread(thread_b_id);

  printf("Threads done: Executed %d %d %d cycles in %d seconds\n",
	  thread_a_cycles, thread_b_cycles, main_cycles,
	  counter/SCHEDULER_SECOND);

  // Releasing alarms does not work correctly on an unpatched kernel.
  ReleaseAlarm(interrupt_id);

  TerminateThread(scheduler_id);
  DeleteThread(scheduler_id);

#ifdef USE_SEMA
  // Delete the semaphore after stopping the scheduler thread.
  DeleteSema(scheduler_sema);
#endif

  return 0;
}

// Thread functions
void thread_a(void *arg)
{
  while(1)
  {
    thread_a_cycles++;
  }
}

void thread_b(void *arg)
{
  volatile int i;

  while(1)
  {
    thread_b_cycles++;
    // Simulate a work load that gets heavier as time passes
    // Comment this out to see how thread_a isn't affected by
    // how long thread_b takes to run
#if 1
    for (i = 0; i > thread_b_cycles; i++)
#endif
    {
      ;
    }
  }
}
```

@}


