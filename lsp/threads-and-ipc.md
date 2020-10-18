# Threads and IPC

Michael Kerrisk - man7.org

## Threads: Introduction

### Overview of Threads

Dominant model, standardized in POSIX is POSIX threads (Pthreads)

Threads within a process:
- __Threads share address space__ of a single process
- __Heap and data segments are shared__ by all threads
- Each thread has its __own stack__
- Each thread __execute at a different point in text__ (program code) segment

Advantages of threads:
- __Information sharing is easier (and faster)__: Processes requires use of __IPC__ mechanisms, Threads sharing is automatic via __global variables__
- __Creation is faster__: Processes creation via _fork()_ is expensive, threads creation (_pthread_create()_) is 10x faster because no need to duplicate page table and file descriptors

Attributes shared by threads:
- Process ID and parent process I
- Process group ID, session ID and controlling terminal
- Process credentials (UIDs and GIDs)
- File Descriptors
- Signal dispositions
- Current working directory
- File mode creation (umask)
- Timers, Record locks (_fcntl()_), resource limits (_getrlinit()_), and more...

Attributes unique to a thread:
- Thread ID
- Signal mask
- Thread-specific data
- errno
- Capabilitiees
- Stack (more or less...)
- Scheduling policy + priority, and more...

### Pthreads API basics

- Traditional UNIX: errno is a process global variable. With Pthreads: errno is a per-thread variable
- Traditional UNIX APIs: return success/failure value and set errno. Most Pthreads APIS: return 0 on success or nonzero error number on failure (same number as errno values)
- When using POSIX threads, compile program with _cc -pthread_ to link program with libpthread library

### Thread creation and termination

Thread creation:
```c
#include <pthread.h>
int pthread_create(pthread_t *thread, const pthread_attr_t *attr, void *(*start)(void *), void *arg);
```
- _thread_ is used to return new thread's __thread ID__ (in POSIX, IDs are guaranteed __unique only within process__)
- _attr_ defines __attributes__ for new thread
	- Specify NULL __to get default__ attributes
- New thread starts execution by calling the function _start_ (_arg_ is passed as an argument to start)

Thread termination:
-  Threads normally terminate in one of two ways:
	- by performing a return __from the start function__
	- by __calling pthread_exit()__
- Also: __all__ threads in a process immediately terminate if:
	- __any thread__ in the process __calls exit()__ 
	- the main thread does a __return from main()__

```c
#include <pthread.h>
int pthread_exit(void *retval);
```  
- Equivalent to return from _start_ function but can be done __anywhere__ in thread
- _retval_ is thread "return value" (analogous to process exit status)

### Threading implementation models

- Terminology: __kernel scheduling entity (KSE)__ are entities (e.g threads and processes) that kernel scheduler schedules to run on CPU (in Linux kernel speak, KSE == "task")
- __M:1 threading implementation__: many threads run in context of single KSE (process), implementation purely via user-space library, no real concurrency sine the kernel doesn't know about threads.
- __1:1 threading implementation__: each thread corresponds to one KSE, true concurrency, bad performance
- __M:N threading implementation__: multiple threads mapped onto smaller number of KSEs, true concurrency without overwhelming the scheduler but user-space implemantation is trickier
- in 2003, Ingo Molnar __rewrote scheduler__ (__O(1) scheduler__": scheduling in constant time regardless of number of KSEs) and Ulrich Drepper wrote new __1:1 pthreads implementation__ for glibc
- Result was __NPTL__ (Native POSIX Threads for Linux), supported by Linux since version 2.6.0 (Dec 2003), can run thousands of threads without impacting scheduler, almost fully POSIX compliant

### Thread IDs

### Joining and detaching threads

### Thread attributes

### Signals and threads

### Threads and process control
 

## Threads: Synchronization

## IPC: Introduction and Overview

## Pipes and FIFOs

## Sockets: Concepts and UNIX Domain

## UNIX Domain Sockets: ANcillary Data

## Sockets: Internet Domain

## TCP/IP Overview

## Raw Sockets

## Alternative I/O Models

## POSIX IPC

## POSIX Semaphores

## POSIX Shared Memory

## Memory Mappings

## File Sealing and memfd

## POSIX Message Queues