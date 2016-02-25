#Virtual System Calls

The "virtual dynamic shared object" (or vDSO) is a small shared library 
exported by the kernel to accelerate the execution of certain system 
calls that do not necessarily have to run in kernel space.

User-space functions that emulate system calls are called virtual system calls.
These are "read-only" system calls that are not allowed to write into the 
kernel address space.

Example virtual system calls:

- gettime
- time
- getcpu
- gettimeofday

gettimeofday vDSO will read from a known location in memory instead of invoking
the kernel syscall.

## What is the vDSO

1. dynamic library
2. memory region belonging to the address of every user-mode process

Example:

    root# cat /proc/<pid>/maps
    f77d9000-f77da000 r-xp 00000000 00:00 0 [vdso]

f77d9000-f77da000 shows that the vDSO occupies a single 4KB page.
r-xp permission flags specify that read and execute permissions are enabled
and that the region is private.
Last three fields indicate that the region is not mapped from any file (no 
inode).

## Format

The binary code of the vDSO memory region has the format of a dynamic library.
In python:

    #!/usr/bin/env python
    from ctypes import *

    for ln in open('/proc/self/maps'):
        if "[vdso]" in ln:
            start, end = [int(x,16) for x in ln.split()[0].split('-')]
            CDLL("libc.so.6").write(1, c_void_p(start), end-start)
            break

Then dump to a file:

    root# python dump.py > vdso.o
    root# file vsdo.o
    vdso.o: ELF 32-bit LSB shared object

## Where is the data

Each vDSO has two addresses, one is a regular kernal-space address greater than
PAGE_OFFSET, the second address is in a region called "vvar" which is made 
available read-only to user-space code. They both refer to the same physical
address (page frame).

