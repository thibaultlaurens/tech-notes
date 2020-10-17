# Linux System Programming

Michael Kerrisk - man7.org

## Fundamental Concepts

### System Calls and library functions

- System call == controlled entry point into kernel code (_syscalls(2)_ man page)
- System calls are expensive !
- Library function == one of multitude of functions in Standard C Library (section 3 of man pages)
- Some library functions employ system calls
- __GNU C library (glibc)__ is most widely used

### Error handling

- Most system calls and library functions return a status indicating success or failure
- Most system calls
	- Return -1 to indicate error
	- Place integer in global variable _errno_ to indicate cause
- Return status should __always__ be tested
- Error numbers in _errno_ are > 0
	- errno(1) man page 
	- <errno.h> defines symbolic names for error numbers 

### System data types

- Various system info needs to be represented in C (Process IDs, user IDs, file offsets, etc.)
- Using native C data types (e.g. int, long) in application code would be non portable
- POSIX defines system data types via __typedef__ (pid_t, uid_t, off_t etc.)

## File I/O

### File I/O overview

- All I/O is done using file descriptors (FDs)
	- nonnegative integer that identifies an open files
	- used for all types of files: terminals, regular files, pipes, FIFOs, devices, sockets..
	- 3 FDs are available to programs run from shell: 0 (stdin), 1 (stdout), 2 (stderr)
- Key file I/O system calls: _open()_, _read()_, _write()_, _close()_

### open(), read(), write() and close()

```
#include <sys/stat.h>
#include <fcntl.h>
int open(const char *pathname, int flags, ... /* mode_t mode */);
```

- Opens existing file / creates and open new file
- _flags_: control semantics of call, created by ORing (|) together: 
	- Acess mode: one of O_RDONLY, O_WRONLY or O_RDWR
	- File creation flags: O_CREAT (create file if it doesnt exists), O_EXCL (error if file already exists), O_TRUNC (truncate existing file to 0 length), ...
	- File status flags: O_APPEND (appen writes to end of file), O_SYNC (make file writes synchronous), O_NONBLOCK (nonblocking I/O), ...
- _mode_ specifies permissions when creating new file
- returns a file descriptor (guaranteed to be lowest available FD)

```
#include <unistd.h>
int read(int fd, void *buffer, size_t count);
```

- Args: _fd_ file descriptor, _buffer_ pointer to buffer to store data, _count_ number of bytes to read
- Returns: > 0 (number of bytes read), 0 (end of file), -1 (error)

```
#include <unistd.h>
int write(int fd, const void *buffer, size_t count);
```

- Args: _fd_ file descriptor, _buffer_ pointer to data to be written, _count_ number of bytes to write
- Returns: Number of bytes written, -1 (error)

```  
#include <unistd.h>
int close(fd);
``` 

- check for errors: accidentaly closing same fd twice, FS specific errors (e.g NFS)
- _close()_ __always__ release fd, even on failure return

### The file offset and lseek()

Every open file has a __file offset__:

- Location at which next read or write will occur
- Set to byte 0 on _open()_
- Automatically updated by _read()_, _write()_ etc.
- Synonyms: read-write offset, file pointer

_lseek()_: randomly accessing a file

```
#include <unistd.h>
off_t lseek(int fd, off_t offset, int whence);
```
- Adjusts offset for open file referred to by _fd_ (some file types no seekable: pipes, sockets etc)
- __Returns new file offset__ counted from start of file
- _whence_: how to interpret _offset_:
	- SEEK_SET: relative start of file
	- SEEK_CUR: relative to current position
	- SEEK_END: relative to next byte after EOF
- _offset_ can be negative for SEEK_CUR and SEEK_END

File holes:
- Writing bytes beyond end of file creates a __file hole__
- Holes __don't__ consume space (saves disk space)
- Use cases: core dump files, sparse files (nominal size >>> allocated size), VM images
- Subsequent writes into holes cause blocks to be allocated 

### Relationship between file descriptors and open files

### Duplicating file descriptors

### File status flags (and fcntl())

### Other file I/O interfaces

## File I/O Buffering

## File Locking ???

## Standards and Portability

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