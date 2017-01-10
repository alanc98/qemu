
The leon3-rtems branch is the qemu git head with the 
patches to support the LEON3 with RTEMS provided by
Jiri Gaisler.

The patches are here:
http://gaisler.org/qemu/

The RTEMS mailing list entry is here:
https://lists.rtems.org/pipermail/users/2014-September/028224.html

I had to manually integrate the code from the patches for the latest qemu 
git head ( January 2017 )


Here is how I build qemu and run rtems/leon3 binaries:

Look here for general instructions on how to install the proper dependancies
and build for linux:
http://wiki.qemu.org/Hosts/Linux

1. Configure QEMU for the LEON3 CPU 

Assuming qemu is checked out in the "qemu" directory
$ mkdir build
$ ../qemu/configure --target-list=sparc-softmmu --enable-debug
$ make

When finished the binary is in build/sparc-softmmu ( qemu-system-sparc ).
I end up putting that binary in my path. 

2. Run an RTEMS binary example

$ qemu-system-sparc -no-reboot -nographic -M leon3_generic -m 64M -kernel ticker.exe

This will run the ticker example and exit. 

When running an RTEMS program that does not call exit(0), qemu will need to be 
stopped/killed. I lookup the PID and use $ kill -9 <pid>

But if the application calls exit(0), qemu will exit. 


