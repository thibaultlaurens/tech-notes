# Files, Processes, Signals and Timers

Michael Kerrisk - man7.org

## Fundamental Concepts

### System Calls and library functions

* System call == controlled entry point into kernel code \(_syscalls\(2\)_ man page\)
* System calls are expensive !
* Library function == one of multitude of functions in Standard C Library \(section 3 of man pages\)
* Some library functions employ system calls
* **GNU C library \(glibc\)** is most widely used

### Error handling

* Most system calls and library functions return a status indicating success or failure
* Most system calls
  * Return -1 to indicate error
  * Place integer in global variable _errno_ to indicate cause
* Return status should **always** be tested
* Error numbers in _errno_ are &gt; 0
  * errno\(1\) man page 
  *  defines symbolic names for error numbers 

### System data types

* Various system info needs to be represented in C \(Process IDs, user IDs, file offsets, etc.\)
* Using native C data types \(e.g. int, long\) in application code would be non portable
* POSIX defines system data types via **typedef** \(pid\_t, uid\_t, off\_t etc.\)

## File I/O

### File I/O overview

* All I/O is done using file descriptors \(FDs\)
  * nonnegative integer that identifies an open files
  * used for all types of files: terminals, regular files, pipes, FIFOs, devices, sockets..
  * 3 FDs are available to programs run from shell: 0 \(stdin\), 1 \(stdout\), 2 \(stderr\)
* Key file I/O system calls: _open\(\)_, _read\(\)_, _write\(\)_, _close\(\)_

### open\(\), read\(\), write\(\) and close\(\)

```text
#include <sys/stat.h>
#include <fcntl.h>
int open(const char *pathname, int flags, ... /* mode_t mode */);
```

* Opens existing file / creates and open new file
* _flags_: control semantics of call, created by ORing \(\|\) together: 
  * Acess mode: one of O\_RDONLY, O\_WRONLY or O\_RDWR
  * File creation flags: O\_CREAT \(create file if it doesnt exists\), O\_EXCL \(error if file already exists\), O\_TRUNC \(truncate existing file to 0 length\), ...
  * File status flags: O\_APPEND \(appen writes to end of file\), O\_SYNC \(make file writes synchronous\), O\_NONBLOCK \(nonblocking I/O\), ...
* _mode_ specifies permissions when creating new file
* returns a file descriptor \(guaranteed to be lowest available FD\)

```text
#include <unistd.h>
int read(int fd, void *buffer, size_t count);
```

* Args: _fd_ file descriptor, _buffer_ pointer to buffer to store data, _count_ number of bytes to read
* Returns: &gt; 0 \(number of bytes read\), 0 \(end of file\), -1 \(error\)

```text
#include <unistd.h>
int write(int fd, const void *buffer, size_t count);
```

* Args: _fd_ file descriptor, _buffer_ pointer to data to be written, _count_ number of bytes to write
* Returns: Number of bytes written, -1 \(error\)

```text
#include <unistd.h>
int close(fd);
```

* check for errors: accidentaly closing same fd twice, FS specific errors \(e.g NFS\)
* _close\(\)_ **always** release fd, even on failure return

### The file offset and lseek\(\)

Every open file has a **file offset**:

* Location at which next read or write will occur
* Set to byte 0 on _open\(\)_
* Automatically updated by _read\(\)_, _write\(\)_ etc.
* Synonyms: read-write offset, file pointer

_lseek\(\)_: randomly accessing a file

```text
#include <unistd.h>
off_t lseek(int fd, off_t offset, int whence);
```

* Adjusts offset for open file referred to by _fd_ \(some file types no seekable: pipes, sockets etc\)
* **Returns new file offset** counted from start of file
* _whence_: how to interpret _offset_:
  * SEEK\_SET: relative start of file
  * SEEK\_CUR: relative to current position
  * SEEK\_END: relative to next byte after EOF
* _offset_ can be negative for SEEK\_CUR and SEEK\_END

File holes:

* Writing bytes beyond end of file creates a **file hole**
* Holes **don't** consume space \(saves disk space\)
* Use cases: core dump files, sparse files \(nominal size &gt;&gt;&gt; allocated size\), VM images
* Subsequent writes into holes cause blocks to be allocated 

### Relationship between file descriptors and open files

Relationship between file descriptors and open files:

* 3 kernel data structures describe files: File descriptor table \(process wide\), Open file table \(system wide\), I-node table \(system wide\)
* Multiple file descriptors can refer to the same open file
* Multiple Open files can refer to the same I-node

File descriptor table \(_struct fdtable_ in _include/linux/fdtable.h_\):

* Per process table with one entry for each FD opened by process
* Flags controlling operation of FD
* Reference to open file description \(file ptr\)

Table of open file descriptions \(_struct file_ in _include/linux/fs.h_\)

* File offset
* File access mode \(R / W / R-W, from _open\(\)_\)
* File status flags \(from _open\(\)_\)
* Reference to inode object for file

I-node table \(_struct inode_ in _include/linux/fs.h_\)

* File type \(regular file, FIFO, socket, ...\)
* File permissions
* Other file properties \(size, timestamps, ...\)

Duplicated file descriptors:

* intraprocess: a process may have multiple FDs referring to same OFD, achieved using _dup\(\)_ or _dup2\(\)_
* between processes: two processes may have FDs referring to same OFD, achieved using _for\(\)_
* two processes may have FDs referring to distinct OFDs that refer to same inode \(_open\(\)_ on the same file\)

Why it matters:

* 2 different FDs referring to same OFD share file offset \(intraprocess and interprocess\)
* Similar scope rules for status flags, changes via one FD are visible via other FD
* Conversely, changes to FD flags are private to each process FD

### Duplicating file descriptors

```text
#include <unistd.h>
int dup(int oldfd);
```

* _oldfd_: an existing file descriptor
* Returns new file descriptor \(on success\)
* **New file descriptor is guaranteed to be lowest available**
* Problematic if a lower FD is being closed when closing and duplicating a FD \(to achieve shell 2&gt;&1 redirection for instance\)

```text
#include <unistd.h>
int dup2(int oldfd, int newfd);
```

* Like _dup\(\)_ but close and reuse _newfd_ atomically
* Does nothing if _oldfd == newfd_
* Returns a new file descriptor \(_newfd_\) on success

### File status flags \(and fcntl\(\)\)

File status flags

* Control semantics of I/O on a file \(O\_APPEND, O\_SYNC, O\_NONBLOCKING, ...\)
* Associated with open file description
* Set when file is open
* Can be retrieved and modified using _fcntl\(\)_

_fcntl\(\)_: file control operations \(check access mode, change file status flags etc.\)

```text
#include <unistd.h>
int fcntl(int fd, int cmd, /* , args */ );
```

* _cmd_: the desired operation \(F\_GETFL to retrieve flags, F\_SETFL to modify flags\)
* _arg_: optional, type depends on _cmd_

### Other file I/O interfaces

```text
#include <unistd.h>
int truncate(const char *pathname, off_t length);
int ftruncate(int fd, off_t length);
```

* Truncate a file via pathname \(_truncate\(\)_\) or descriptor \(_ftruncate\(\)_\)
* length &lt; current size =&gt; data is lost
* length &gt; current size =&gt; null bytes \(a hole\) added at EOF
* Does not change file offset !

I/O at a specific location: _pread\(\)_ and _pwrite\(\)_

* Useful in multithreaded program when different threads want to do I/O in different parts of the same file
* Does not change file offset ! \(whereas _lseek\(\)_ in one thread would affect offset seen by **all** threads\)

Scatter-gather I/O: _readv\(\)_ and _writev\(\)_

* _readv\(\)_: reads contiguous block from file, scatters \(splits\) data accross multiple buffers
* _writev\(\)_: gathers output data from multiple buffers \(written one after the other in file\)
* **Advantage**: reduces number of system calls
* Buffers are described via _struct iovec \[\]_ argument

_preadv\(\)_ and _pwritev\(\)_

* _preadv\(\)_ == _pread\(\)_ + _readv\(\)_
* _pwritev\(\)_ == _pwrite\(\)_ + _writev\(\)_
* Linux specific, since 2.6.30

/proc/PID/fd

* Each process has a corresponding /proc/PID/fd directory containing symbolic links for each of the process's FDs
* ex: /proc/PID/fd/n == symlink to file opened on descriptor n by process PID

## File I/O Buffering

### Kernel buffering

Two kinds of file I/O buffering: within kernel \(the buffer cache\) and in user space

Kernel buffering of file I/O:

* _read\(\)_ and _write\(\)_ **don't** directly cause disk accesses
* Just transfer data between kernel and user space
* Within kernel, data is buffered in the _buffer_ cache
  * System-wide resource
  * Limited only by available memory
  * Strictly speaking: buffer cache == page cache 

Advantages of the buffer cache:

* **Speed**: _read\(\)_ and _write\(\)_ don't block on disk transfer
* **Efficiency**: kernel makes fewer disk transfers

Effect of buffer size on file I/O performance:

* _write\(fd, buf, 4096\);_ vs _for \(j = 0; j &lt; 4096; j++\) write\(fd, &buf\[j\], 1\);_
* Same output file, same number of buffer cache flushes but **different number of system calls** \(expensive!\)
* 4096 bytes is near optimum performance for file I/O

### User-space \(stdin\) buffering

_stdio_ has three buffering modes:

* **Line-buffered**: default mode on stdin/stdout on terminal devices: output/input flushed/available only when newline character is written/entered
* **Block buffered**: default mode for block devices \(disks\): I/O is buffered in "blocks" \(default BUFSIZ \(8192\) bytes\), output \(_write\(\)_\) flushed only when buffer is full
* **Unbufered**: default to stderr: each I/O operations results in an immediate _read\(\)_ / _write\(\)_ call

Disable _stdio_ buffering via _setvbuf\(3\)_ and _setbuf\(3\)_: occasionally useful but impact performace Flush _stdio_ buffers via _fflush\(fp\)_. Transfer \(output\) data only to kernel buffer cache \(must **flush buffer cache to ensure data lands on disk**\)

### Controlling kernel buffering

Kernel **automatically** flushes modified pages in buffer cache to disk:

* Within 30 seconds \(/proc/sys/vm/dirty\_expire\_centisecs \(3000\)\)
* Or, in response to memory pressure

Application can also perform **explicit buffer flushing** on two types of data:

* **File data**
* **Metadata** describing file \(size, last modification time, ownership, permissions, data block pointers, ...\)

Explicity flushing modified buffers:

* _fsync\(fd\)_: **flush data and metadata** associated with open file referred by _fd_
* _fdatasync\(fd\)_: Same as _fsync\(\)_ but **only flush metadata if** changes would be needed in order to subsequently read data \(potentially cheaper than _fsync\(\)_\)
* _sync\(void\)_: Flush all modified buffers for all files
* _fsync\(fd\)_, _fdatasync\(fd\)_ and _sync\(void\)_ all block until synchronization is complete \(POSIX permits _sync\(\)_ to merely **schedule** sync operation\)
* Flushing buffer cache doesn't guarantee data has landed on media surface because of disk hardware caching
* Set O\_SYNC flag to disable buffer cache and make all writes to a file synchronous and block until data has been transferred to disk \(massive performance hit!\)

## ~~File Locking~~

## Standards and Portability

### Standards: why ?

* **1969**: UNIX first implemented, developped at Bell Labs \(AT&T\)
* 1979: Seventh Edition \(V7\) UNIX
* After V7, UNIX starts to fragment: **BSD** \(Berkeley Software Distribution from UCB\), **System V** \(AT&T\), vendor implementations based on System V or BSD
* Mid-1980s: "UNIX" is a chaos of competing, increasingly incompatible implementations, "The UNIX wars": **UNIX Internation** \(AT&T, Sun\) vs **Open Software Foundation** \(the rest\)
* Pressure to standardize results in POSIX \(Portable Operating System Interface\) and other standards 

### Standards: POSIX

* **POSIX.1** \(1990\): Sheperd by IEEE \(Institute of Electrical and Electronics Engineers\), API standard for \(UNIX like\) OS
* **POSIX.2** \(1992\): Standard for shell and utilities
* POSIX.1b \(1993\): Realtime APIs
* POSIX.1c \(1995\): Threads APIs
* POSIX.1 \(1996\): Consolidation of POSIX.1-1990, POSIX.1b, POSIX.1c

### XPG and SUS

* 1989: **X/Open** founded by a consortium of computer vendors for a comprehensive set of open system standards
* **X/Open Portability Guides \(XPG\)**: Consolidation of POSIX and various other standards
* XPG subsequently repackaged as **Single UNIX Specification \(SUS\)** \(1994: SUSv1 - XPG4v2, 1997: SUSv2 - XPG5\)
* 1996: X/Open merges with Open Software Foundation =&gt; **The Open Group** \(TOG\); virtually every UNIX vendor is a member nowadays; unofficial end of "The UNIX wars"
* 1999: IEEE, TOG and ISO/IEC Joint Technical Committee 1 collaborate in **Austin Common Standards Revision Group** to revise POSIX and SUS standards and consolidate into a single standard
* 2001: combined POSIX.1-2001 and SUSv3 published as a modular standard; SUSv3 == POSIX + XSI \(X/Open System Interface\) extension
* 2008: POSIX.1-2008 / SUSv4 published 

### Linux and standards

* Linux now dominant, but portability is still valuable goal
* Linux not standards certified, but largely standards compliant
* See also: _standards\(7\)_ man page

### ~~Portable programming: feature test macros~~

### ~~Portable programming: limits and options~~

## Files

## Directories and Links

## Inotify

## Processes

## Process Credentials

## Signals: Introduction

## Signals: Signal Handlers

## Signals: Further Details

## Process Creation and Termination

## Executing Programs

## System Call Tracing with strace

## Daemons

## Extended Attributes

## Access Control Lists

## Time

## Timers and Sleeping

