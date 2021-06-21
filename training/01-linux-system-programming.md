---
description: Michael Kerrisk - man7.org
---

# Linux System Programing

# Files, Processes and Signals

## 1. Course Introduction

## 2. Fundamental Concepts

### System Calls and library functions

- System call == controlled entry point into kernel code \(_syscalls\(2\)_ man page\)
- System calls are expensive !
- Library function == one of multitude of functions in Standard C Library \(section 3 of man pages\)
- Some library functions employ system calls
- **GNU C library \(glibc\)** is most widely used

### Error handling

- Most system calls and library functions return a status indicating success or failure
- Most system calls
  - Return -1 to indicate error
  - Place integer in global variable _errno_ to indicate cause
- Return status should **always** be tested
- Error numbers in _errno_ are &gt; 0
  - errno\(1\) man page
  - defines symbolic names for error numbers

### System data types

- Various system info needs to be represented in C \(Process IDs, user IDs, file offsets, etc.\)
- Using native C data types \(e.g. int, long\) in application code would be non portable
- POSIX defines system data types via **typedef** \(pid_t, uid_t, off_t etc.\)

## 3. File I/O

### File I/O overview

- All I/O is done using file descriptors \(FDs\)
  - nonnegative integer that identifies an open files
  - used for all types of files: terminals, regular files, pipes, FIFOs, devices, sockets..
  - 3 FDs are available to programs run from shell: 0 \(stdin\), 1 \(stdout\), 2 \(stderr\)
- Key file I/O system calls: _open\(\)_, _read\(\)_, _write\(\)_, _close\(\)_

### open\(\), read\(\), write\(\) and close\(\)

```c
#include <sys/stat.h>
#include <fcntl.h>
int open(const char *pathname, int flags, ... /* mode_t mode */);
```

- Opens existing file / creates and open new file
- _flags_: control semantics of call, created by ORing \(\|\) together:
  - Acess mode: one of O_RDONLY, O_WRONLY or O_RDWR
  - File creation flags: O_CREAT \(create file if it doesnt exists\), O_EXCL \(error if file already exists\), O_TRUNC \(truncate existing file to 0 length\), ...
  - File status flags: O_APPEND \(appen writes to end of file\), O_SYNC \(make file writes synchronous\), O_NONBLOCK \(nonblocking I/O\), ...
- _mode_ specifies permissions when creating new file
- returns a file descriptor \(guaranteed to be lowest available FD\)

```c
#include <unistd.h>
int read(int fd, void *buffer, size_t count);
```

- Args: _fd_ file descriptor, _buffer_ pointer to buffer to store data, _count_ number of bytes to read
- Returns: &gt; 0 \(number of bytes read\), 0 \(end of file\), -1 \(error\)

```c
#include <unistd.h>
int write(int fd, const void *buffer, size_t count);
```

- Args: _fd_ file descriptor, _buffer_ pointer to data to be written, _count_ number of bytes to write
- Returns: Number of bytes written, -1 \(error\)

```c
#include <unistd.h>
int close(fd);
```

- check for errors: accidentaly closing same fd twice, FS specific errors \(e.g NFS\)
- _close\(\)_ **always** release fd, even on failure return

### The file offset and lseek\(\)

Every open file has a **file offset**:

- Location at which next read or write will occur
- Set to byte 0 on _open\(\)_
- Automatically updated by _read\(\)_, _write\(\)_ etc.
- Synonyms: read-write offset, file pointer

_lseek\(\)_: randomly accessing a file

```c
#include <unistd.h>
off_t lseek(int fd, off_t offset, int whence);
```

- Adjusts offset for open file referred to by _fd_ \(some file types no seekable: pipes, sockets etc\)
- **Returns new file offset** counted from start of file
- _whence_: how to interpret _offset_:
  - SEEK_SET: relative start of file
  - SEEK_CUR: relative to current position
  - SEEK_END: relative to next byte after EOF
- _offset_ can be negative for SEEK_CUR and SEEK_END

File holes:

- Writing bytes beyond end of file creates a **file hole**
- Holes **don't** consume space \(saves disk space\)
- Use cases: core dump files, sparse files \(nominal size &gt;&gt;&gt; allocated size\), VM images
- Subsequent writes into holes cause blocks to be allocated

### Relationship between file descriptors and open files

Relationship between file descriptors and open files:

- 3 kernel data structures describe files: File descriptor table \(process wide\), Open file table \(system wide\), I-node table \(system wide\)
- Multiple file descriptors can refer to the same open file
- Multiple Open files can refer to the same I-node

File descriptor table \(_struct fdtable_ in _include/linux/fdtable.h_\):

- Per process table with one entry for each FD opened by process
- Flags controlling operation of FD
- Reference to open file description \(file ptr\)

Table of open file descriptions \(_struct file_ in _include/linux/fs.h_\)

- File offset
- File access mode \(R / W / R-W, from _open\(\)_\)
- File status flags \(from _open\(\)_\)
- Reference to inode object for file

I-node table \(_struct inode_ in _include/linux/fs.h_\)

- File type \(regular file, FIFO, socket, ...\)
- File permissions
- Other file properties \(size, timestamps, ...\)

Duplicated file descriptors:

- intraprocess: a process may have multiple FDs referring to same OFD, achieved using _dup\(\)_ or _dup2\(\)_
- between processes: two processes may have FDs referring to same OFD, achieved using _for\(\)_
- two processes may have FDs referring to distinct OFDs that refer to same inode \(_open\(\)_ on the same file\)

Why it matters:

- 2 different FDs referring to same OFD share file offset \(intraprocess and interprocess\)
- Similar scope rules for status flags, changes via one FD are visible via other FD
- Conversely, changes to FD flags are private to each process FD

### Duplicating file descriptors

```c
#include <unistd.h>
int dup(int oldfd);
```

- _oldfd_: an existing file descriptor
- Returns new file descriptor \(on success\)
- **New file descriptor is guaranteed to be lowest available**
- Problematic if a lower FD is being closed when closing and duplicating a FD \(to achieve shell 2&gt;&1 redirection for instance\)

```c
#include <unistd.h>
int dup2(int oldfd, int newfd);
```

- Like _dup\(\)_ but close and reuse _newfd_ atomically
- Does nothing if _oldfd == newfd_
- Returns a new file descriptor \(_newfd_\) on success

### File status flags \(and fcntl\(\)\)

File status flags

- Control semantics of I/O on a file \(O_APPEND, O_SYNC, O_NONBLOCKING, ...\)
- Associated with open file description
- Set when file is open
- Can be retrieved and modified using _fcntl\(\)_

_fcntl\(\)_: file control operations \(check access mode, change file status flags etc.\)

```c
#include <unistd.h>
int fcntl(int fd, int cmd, /* , args */ );
```

- _cmd_: the desired operation \(F_GETFL to retrieve flags, F_SETFL to modify flags\)
- _arg_: optional, type depends on _cmd_

### Other file I/O interfaces

```c
#include <unistd.h>
int truncate(const char *pathname, off_t length);
int ftruncate(int fd, off_t length);
```

- Truncate a file via pathname \(_truncate\(\)_\) or descriptor \(_ftruncate\(\)_\)
- length &lt; current size =&gt; data is lost
- length &gt; current size =&gt; null bytes \(a hole\) added at EOF
- Does not change file offset !

I/O at a specific location: _pread\(\)_ and _pwrite\(\)_

- Useful in multithreaded program when different threads want to do I/O in different parts of the same file
- Does not change file offset ! \(whereas _lseek\(\)_ in one thread would affect offset seen by **all** threads\)

Scatter-gather I/O: _readv\(\)_ and _writev\(\)_

- _readv\(\)_: reads contiguous block from file, scatters \(splits\) data accross multiple buffers
- _writev\(\)_: gathers output data from multiple buffers \(written one after the other in file\)
- **Advantage**: reduces number of system calls
- Buffers are described via _struct iovec \[\]_ argument

_preadv\(\)_ and _pwritev\(\)_

- _preadv\(\)_ == _pread\(\)_ + _readv\(\)_
- _pwritev\(\)_ == _pwrite\(\)_ + _writev\(\)_
- Linux specific, since 2.6.30

/proc/PID/fd

- Each process has a corresponding /proc/PID/fd directory containing symbolic links for each of the process's FDs
- ex: /proc/PID/fd/n == symlink to file opened on descriptor n by process PID

## 4. File I/O Buffering

### Kernel buffering

Two kinds of file I/O buffering: within kernel \(the buffer cache\) and in user space

Kernel buffering of file I/O:

- _read\(\)_ and _write\(\)_ **don't** directly cause disk accesses
- Just transfer data between kernel and user space
- Within kernel, data is buffered in the _buffer_ cache
  - System-wide resource
  - Limited only by available memory
  - Strictly speaking: buffer cache == page cache

Advantages of the buffer cache:

- **Speed**: _read\(\)_ and _write\(\)_ don't block on disk transfer
- **Efficiency**: kernel makes fewer disk transfers

Effect of buffer size on file I/O performance:

- _write\(fd, buf, 4096\);_ vs _for \(j = 0; j &lt; 4096; j++\) write\(fd, &buf\[j\], 1\);_
- Same output file, same number of buffer cache flushes but **different number of system calls** \(expensive!\)
- 4096 bytes is near optimum performance for file I/O

### User-space \(stdin\) buffering

_stdio_ has three buffering modes:

- **Line-buffered**: default mode on stdin/stdout on terminal devices: output/input flushed/available only when newline character is written/entered
- **Block buffered**: default mode for block devices \(disks\): I/O is buffered in "blocks" \(default BUFSIZ \(8192\) bytes\), output \(_write\(\)_\) flushed only when buffer is full
- **Unbufered**: default to stderr: each I/O operations results in an immediate _read\(\)_ / _write\(\)_ call

Disable _stdio_ buffering via _setvbuf\(3\)_ and _setbuf\(3\)_: occasionally useful but impact performace Flush _stdio_ buffers via _fflush\(fp\)_. Transfer \(output\) data only to kernel buffer cache \(must **flush buffer cache to ensure data lands on disk**\)

### Controlling kernel buffering

Kernel **automatically** flushes modified pages in buffer cache to disk:

- Within 30 seconds \(/proc/sys/vm/dirty_expire_centisecs \(3000\)\)
- Or, in response to memory pressure

Application can also perform **explicit buffer flushing** on two types of data:

- **File data**
- **Metadata** describing file \(size, last modification time, ownership, permissions, data block pointers, ...\)

Explicity flushing modified buffers:

- _fsync\(fd\)_: **flush data and metadata** associated with open file referred by _fd_
- _fdatasync\(fd\)_: Same as _fsync\(\)_ but **only flush metadata if** changes would be needed in order to subsequently read data \(potentially cheaper than _fsync\(\)_\)
- _sync\(void\)_: Flush all modified buffers for all files
- _fsync\(fd\)_, _fdatasync\(fd\)_ and _sync\(void\)_ all block until synchronization is complete \(POSIX permits _sync\(\)_ to merely **schedule** sync operation\)
- Flushing buffer cache doesn't guarantee data has landed on media surface because of disk hardware caching
- Set O_SYNC flag to disable buffer cache and make all writes to a file synchronous and block until data has been transferred to disk \(massive performance hit!\)

## ~~5. File Locking~~

## 6. Standards and Portability

### Standards: why ?

- **1969**: UNIX first implemented, developped at Bell Labs \(AT&T\)
- 1979: Seventh Edition \(V7\) UNIX
- After V7, UNIX starts to fragment: **BSD** \(Berkeley Software Distribution from UCB\), **System V** \(AT&T\), vendor implementations based on System V or BSD
- Mid-1980s: "UNIX" is a chaos of competing, increasingly incompatible implementations, "The UNIX wars": **UNIX Internation** \(AT&T, Sun\) vs **Open Software Foundation** \(the rest\)
- Pressure to standardize results in POSIX \(Portable Operating System Interface\) and other standards

### Standards: POSIX

- **POSIX.1** \(1990\): Sheperd by IEEE \(Institute of Electrical and Electronics Engineers\), API standard for \(UNIX like\) OS
- **POSIX.2** \(1992\): Standard for shell and utilities
- POSIX.1b \(1993\): Realtime APIs
- POSIX.1c \(1995\): Threads APIs
- POSIX.1 \(1996\): Consolidation of POSIX.1-1990, POSIX.1b, POSIX.1c

### XPG and SUS

- 1989: **X/Open** founded by a consortium of computer vendors for a comprehensive set of open system standards
- **X/Open Portability Guides \(XPG\)**: Consolidation of POSIX and various other standards
- XPG subsequently repackaged as **Single UNIX Specification \(SUS\)** \(1994: SUSv1 - XPG4v2, 1997: SUSv2 - XPG5\)
- 1996: X/Open merges with Open Software Foundation =&gt; **The Open Group** \(TOG\); virtually every UNIX vendor is a member nowadays; unofficial end of "The UNIX wars"
- 1999: IEEE, TOG and ISO/IEC Joint Technical Committee 1 collaborate in **Austin Common Standards Revision Group** to revise POSIX and SUS standards and consolidate into a single standard
- 2001: combined POSIX.1-2001 and SUSv3 published as a modular standard; SUSv3 == POSIX + XSI \(X/Open System Interface\) extension
- 2008: POSIX.1-2008 / SUSv4 published

### Linux and standards

- Linux now dominant, but portability is still valuable goal
- Linux not standards certified, but largely standards compliant
- See also: _standards\(7\)_ man page

### ~~Portable programming: feature test macros~~

### ~~Portable programming: limits and options~~

## 7. Files

## 8. Directories and Links

## ~~9. Inotify~~

## 10. Processes

## 11. Process Credentials

## 12. Signals: Introduction

## 13. Signals: Signal Handlers

## ~~14. Signals: Further Details~~

## 15. Process Creation and Termination

## 16. Executing Programs

## ~~17. System Call Tracing with strace~~

## 18. Daemons

## ~~19. Extended Attributes~~

## ~~20. Access Control Lists~~

## ~~21. Time~~

## ~~22. Timers and Sleeping~~

# Threads and IPC

## 23. Threads: Introduction

### Overview of Threads

Dominant model, standardized in POSIX is POSIX threads \(Pthreads\)

Threads within a process:

- **Threads share address space** of a single process
- **Heap and data segments are shared** by all threads
- Each thread has its **own stack**
- Each thread **execute at a different point in text** \(program code\) segment

Advantages of threads:

- **Information sharing is easier \(and faster\)**: Processes requires use of **IPC** mechanisms, Threads sharing is automatic via **global variables**
- **Creation is faster**: Processes creation via _fork\(\)_ is expensive, threads creation \(_pthread_create\(\)_\) is 10x faster because no need to duplicate page table and file descriptors

Attributes shared by threads:

- Process ID and parent process I
- Process group ID, session ID and controlling terminal
- Process credentials \(UIDs and GIDs\)
- File Descriptors
- Signal dispositions
- Current working directory
- File mode creation \(umask\)
- Timers, Record locks \(_fcntl\(\)_\), resource limits \(_getrlinit\(\)_\), and more...

Attributes unique to a thread:

- Thread ID
- Signal mask
- Thread-specific data
- errno
- Capabilitiees
- Stack \(more or less...\)
- Scheduling policy + priority, and more...

### Pthreads API basics

- Traditional UNIX: errno is a process global variable. With Pthreads: errno is a per-thread variable
- Traditional UNIX APIs: return success/failure value and set errno. Most Pthreads APIS: return 0 on success or nonzero error number on failure \(same number as errno values\)
- When using POSIX threads, compile program with _cc -pthread_ to link program with libpthread library

### Thread creation and termination

Thread creation:

```c
#include <pthread.h>
int pthread_create(pthread_t *thread, const pthread_attr_t *attr, void *(*start)(void *), void *arg);
```

- _thread_ is used to return new thread's **thread ID** \(in POSIX, IDs are guaranteed **unique only within process**\)
- _attr_ defines **attributes** for new thread
  - Specify NULL **to get default** attributes
- New thread starts execution by calling the function _start_ \(_arg_ is passed as an argument to start\)

Thread termination:

- Threads normally terminate in one of two ways:
  - by performing a return **from the start function**
  - by **calling pthread_exit\(\)**
- Also: **all** threads in a process immediately terminate if:
  - **any thread** in the process **calls exit\(\)**
  - the main thread does a **return from main\(\)**

```c
#include <pthread.h>
int pthread_exit(void *retval);
```

- Equivalent to return from _start_ function but can be done **anywhere** in thread
- _retval_ is thread "return value" \(analogous to process exit status\)

### Threading implementation models

- Terminology: **kernel scheduling entity \(KSE\)** are entities \(e.g threads and processes\) that kernel scheduler schedules to run on CPU \(in Linux kernel speak, KSE == "task"\)
- **M:1 threading implementation**: many threads run in context of single KSE \(process\), implementation purely via user-space library, no real concurrency sine the kernel doesn't know about threads.
- **1:1 threading implementation**: each thread corresponds to one KSE, true concurrency, bad performance
- **M:N threading implementation**: multiple threads mapped onto smaller number of KSEs, true concurrency without overwhelming the scheduler but user-space implemantation is trickier
- in 2003, Ingo Molnar **rewrote scheduler** \(**O\(1\) scheduler**": scheduling in constant time regardless of number of KSEs\) and Ulrich Drepper wrote new **1:1 pthreads implementation** for glibc
- Result was **NPTL** \(Native POSIX Threads for Linux\), supported by Linux since version 2.6.0 \(Dec 2003\), can run thousands of threads without impacting scheduler, almost fully POSIX compliant

### Thread IDs

### Joining and detaching threads

### Thread attributes

### Signals and threads

### Threads and process control

## 24. Threads: Synchronization

## 25. IPC: Introduction and Overview

## 26. Pipes and FIFOs

## 27. Sockets: Concepts and UNIX Domain

## 28. UNIX Domain Sockets: ANcillary Data

## 29. Sockets: Internet Domain

## ~~30. TCP/IP Overview~~

## ~~31. Raw Sockets~~

## ~~32. Alternative I/O Models~~

## ~~33. POSIX IPC~~

## 34. POSIX Semaphores

## 35. POSIX Shared Memory

## ~~36. Memory Mappings~~

## ~~37. File Sealing and memfd~~

## ~~38. POSIX Message Queues~~

# Security and Isolation API

## 39. Security and Isolation APIs Overview

## 40. Priviledged Programs

## 41. Capabilities

## 42. Capabilities: Further Topics

## 43. Namespaces

## 44. Namespaces APIs

## 45. User Namespaces

## 46. User Namespaces and Capabilities

## ~~47. Mount Namespaces and Shared Subtree~~

## 48. Cgroups

## 49. Cgroups Version 2

## ~~50. Cgroups Version 2 Thread Mode~~

## 51. Seccomp

## ~~52. Network Namespaces~~

## ~~53. Docker unpluged~~

## ~~54. SELinux~~

# Shared Libraries

## 55. Fundamentals of Shared Libraries

### Background: the static linker and the dynamic linker

- **Linking**: Process of combining or matching up one or more objects. This task include **symbol relocation**: resolving symbol references in one object to definitions in another object.
- **Static linking**: at build time, when creating executable or shared library. Not to be confused with **statically linked** program: an executable that was built not to need shared libraries.
- **Dynamic linking**: at run time, when program is loaded into memory \(not required if program doesn't make use of shared libraries / is statically linked\).

### Background: static vs shared libraries

- Static libraries: "Archive" of compiled object files. Employed by \(static\) linker \(_ld_\) at link time. Cons: wast disk space, app must be relinked after libraries update.
- Shared libraries: Also called **shared object**, a single copy of object files is shared by all executables. Object module not copied into executable; linking done at run time.
- Pros of shared libraries: **smaller program size** \(may result in faster loading\) + **apps automatically employ latest version** \(linking done at runtime\)
- Cons of shared libraries: **increased complexity**, **must compile to use Position Independant Code** \(PIC\), **symbol relocation is required** at runtime.

### Basics of shared library creation and use

**ELF**: Executable and Linking Format, standardized format used to structure executables and shared objects

```text
$ cc -g -c -fPIC -Wall mod1.c mod2.c mod3.c
$ cc -g -shared -o libfoo.so mod1.o mod2.o mod3.o
```

- **First command produced object modules** that go into the library.
- **Second command creates shared library**, by convention, names have prefix _lib_ and suffix _.so_ \("shared object"\).
- -fPIC: compiler produces **position-independant code** to allow object code to be placed **anywhere in memory**. Needed because **at static linking time we don't know run time location**.

```text
$ cc -g -Wall -o prog prog.c libfoo.so
$ LD_LIBRARY_PATH=. ./prog
```

- We have to **embed name of library inside executable**, the dynamic linker \(DL, which is a share library itself provided by glibc\) will resolve executable's dynamic dependencies at run time
- DL searches libraries in standard locations OR we can use LD_LIBRARY_PATH environment variable
- Useful commands: _ldd\(1\)_: list dynamic dependencies of an executable \(invoke DL\); _pldd\(1\)_: list shared libraries currently loaded into process with the specified PID.

### The shared library soname

- **The library soname is the foundation of shared library versionning**
- **soname**: alias \(ELF DT\*SONAME tag\) of the shared library to **embed in executable** \(with _-Wl,-soname,libbar.so_\)
- symlink soname to real name before running the program \(_ln -s soname realname_\)

### ~~Summary: library creation, linking and loading~~

## 56. Versioning and Installation

### Shared library versionning

A new library version, an **Application Binary Interface** \(ABI\), change may be **compatible** \(-&gt; must create a new **minor version**\) or **incompatible** \(-&gt; must create a new **major version**\).

No API breakage:

- No public function or variable is removed
- Function call signatures aren't changed in ways that break existing consumers
- Structures allocated within and returned by functions remain unchanged
- new public functions and variables are added

Requirements for a shared library versioning scheme:

- **Allow creation of new major versions** \(new executables can use latest version\)
- **Existing executables can continue using older major versions**
- **Existing executables automatically use latest minor release**

### Shared libraries real names, sonames and linker names

- Library _real_ names correspond to real filenames: lib*name*.so.major.minor\(.patch\)
- Library _soname_ uses major version of corresponding real name: lib*name*.so.major \(one soname for each major library version, all symlinked to their latest major real name\)
- **Linker** name lib*name*.so \(one per library\) is then linked to latest soname \(lib*name*.so -&gt; lib*name*.so.major -&gt; lib*name*.so.major.minor\)

Creating a shared library following standard conventions:

```text
# create object files needed to build the library
$ cc -g -c -fPIC -Wall mod1.c mod2.c mod3.c

# build library with real name libdemo.so.1.0.1 and soname lidemo.so.1
$ cc -g -shared -Wl,-soname,libdemo.so.1 -o libdemo.so.1.0.1 mod1.o mod2.o mod3.o

# create soname and linker symlinks
ln -s libdemo.so.1.0.1 libdemo.so.1
ln -s libdemo.so.1 libdemo.so

# build executable using linker name
cc -g -Wall -o prog.c -L. -ldemo

# run program as usual
$ LD_LIBRARY_PATH=. ./prog
```

- _-ldemo_ causes the linker to search for library named according to standard conventions
- _-L_ specifies additional directory where linker should search for libraries

### Installing shared libraries

To avoid the use of LD_LIBRARY_PATH and -L when building executable, install shared libraries in:

- /usr/lib: where most standard libraries are installed
- /lib: traditionally for libraries that are required during system startup \(linked to /usr/lib nowadays\)
- /lib64 and /usr/lib64: for 64-bit libraries on 64-bit architectures \(e.g., x86-64\)
- /usr/local/lib: for nonstandard libraries \(or when we don't want to install on a network-shared /usr/lib\)
- one of the directories listed in /etc/ld.so.conf

### ldconfig

_ldconfig\(8\)_ does two things to **address potential difficulties** with shared libraries:

- Searches a standard set of directory files to **update a cache file /etc/ld.so.cache** \(reduce loading shared libraries time when used by DL at run time\)
- Prevent **soname symlinks to accidentally fall out of sync** \(examines latest minor and major versions and update or create symlinks\)

### Further details

- Constructor and destructor functions \(also available for main program\): automatically executed when library is loaded / unloaded, declared with \_\_attribute\_\_ \(\(constructor\)\) / \_\_attribute\_\_ \(\(destructor\)\)
- _abidiff\(1\)_: compares two shared objects, showing different functions, variables, and function arguments \(need debugging to show additional arguments: _cc -g_\)

## 57. The Dynamic Linker

### Rpath: specifying library search paths in an object

- Third option to inform the dynamic linker of location of shared libraries is to **insert a list of directories into the executable** during static linking.
- To embed a run-time library path \(**rpath**\) list: _gcc -Wl,-rpath,path-to-lib-dir_
- Shared libraries can themselves have dependencies
- Order of precedence: \(DT_RPATH: original and default ELF entry is a design error\) &gt; LD_LIBRARY_PATH &gt; **DT_RUNPATH** \(LD_LIBRARY_PATH can override it at run path, what we want\)
- DL understands special names in rpath list:
  - $ORIGIN: expands to directory containing program or library\)
  - $LIB: expands to lib or lib64 depending on architecture
  - $PLATFORM: expands to string corresponding to processor type\)

### Finding shared libraries at run time

1. If object has DT_RPATH list and does **not** have DT_RUNPATH: search DT_RPATH list
2. If LD_LIBRARY_PATH defined: search directories it specifies \(disable in "secure" mode, ie set-UID and set-GID programs etc\)
3. If calling object has DT_RUNPATH list: search directories in that list
4. Check /etc/ld.so.cache for a corresponding entry
5. Search /lib and /usr/lib \(in that order\) or \(/lib64 or /usr/lib64\)

### Symbol resolution, library load order, and link maps

Shared library are designed to mirror traditional static library semantics:

- Definition of global symbol in main program overrides version in library
- Global symbol appears in multiple libraries ? =&gt; reference is resolved to first definition when **scanning libraries in left-to-right order as specified in static link command line**

To make a shared libraries a **self contained subsystem**, use _-Bsymbolink_ linker option to force global symbol references to resolve inside library

Symbol resolution:

- Dependant libraries are added in **breadth-first order** \(immediate dependencies of main program are loaded first\)
- Symbols are resolved be searching libraries in load order \(set of shared objects that have been loaded by application is recorded in a **link-map list**\)

### Debugging the operation of the dynamic linker

Use the "LD_DEBUG" environment variable:

```text
$ LD_DEBUG=help ./prog
```

## 58. Shared Libraries and the Static Linker

### Recording dynamic dependencies

- When creating an object, ld records a dependency for each shared library listed on the link command \(ELF DT_NEEDED tag recorded\)
- ld records a dependency **even if library doesn't provide any symbols needed by the link**
- the _--as-needed_ linker flags changes this behevior \(enabled by default on some distros, eg ubuntu!\)

### Handling secondary dependencies at link time

When creating a **shared library**, ld does **not** require there to be a resolution available for all symbol references \(declaring symbol _extern_ keeps compiler happy\)

To handle secondary dependency:

- Don't use the _-rpath_ linker option when building the executable: main shouldnt have to care about this
- Don't specify secondary dependency when linking main: "overlinking" can change the load order
- =&gt; use _-rpath-link_ linker option to tell linker where to look for needed libraries

```text
$ cc -o liby.so -shared -fPIC liby.c
$ cc -o libx.so -shared -fPIC libx.c liby.so
$ cc -o main main.c -Wl,-rpath-link,<dirpath> libx.so
```

### How the static linker finds library dependencies

The linker _ld\(1\)_ looks for dependencies of shared libraries in:

1. Directories specified by _-rpath-link_ options
2. Directories specified by _-rpath_ options
3. The directories specified by LD_RUN_PATH env var
4. The directories specified by LD_LIBRARY_PATH env var
5. The directories in a shared library's DT_RUNPATH / DT_RPATH
6. /lib and /usr/lib \(or /lib64 and /usr/lib64\)
7. The directories specified in /etc/ld.so.conf

## 59. ELF and Program Execution

## 60. Dynamically Loaded Libraries \(dlopen\)

## 61. Symbol Visibility

## 62. Symbol Versionning

## 63. GOT, PLT, and Lazy Binding

## ~~64. Wrapup~~
