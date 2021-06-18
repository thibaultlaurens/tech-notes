---
description: Michael Kerrisk - man7.org
---

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
