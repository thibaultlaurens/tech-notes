# B - Threads and IPC

Michael Kerrisk - man7.org

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
