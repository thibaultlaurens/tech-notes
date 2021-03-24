# Software Programming

## Programming Concepts (TODO)

- [Programming Concepts](https://thecodeboss.dev/2014/10/programming-concepts-the-stack-and-the-heap/) \(faire toute la serie\)

### The Stack And The Heap

Both the stack and the heap refer to different locations where memory is managed, but with significantly different strategies.

#### The Stack

The stack is a region of RAM that gets created on every thread that your application is running on. It works in a **LIFO** (Last In, First Out) manner, meaning that as soon as you allocate ("push") memory on to the stack, that chunk of memory will be the first to be deallocated ("popped"). Every time a function declares a new variable, it is "pushed" onto the stack, and after that variable falls out of scope (such as when the function closes), that variable will be deallocated from the stack automatically. Once a stack variable is freed, that region of memory becomes available for other stack variables.

Due to the pushing and popping nature of the stack, memory management is very logical and is able to be handled completely by the CPU; this makes it very quick, especially since each byte in the stack tends to be reused very frequently which means it tends to be **mapped to the processor’s cache**.

However, there are some cons to this form of strict management. The size of the stack is a fixed value, and allocating more onto the stack than it can hold will result in a **stack overflow**. The size of the stack is decided when the thread is created, and each variable has a maximum size that it can occupy based on its data type; this prevents certain variables such as integers from ever growing beyond a certain value, and forces more complex data types such as arrays to specify their size prior to runtime since the stack won’t let them be resized. Variables allocated on the stack also are always **local** in nature because they are always next in line to be popped (unless more variables are pushed prior to the popping of earlier variables).

Overall, the stack really exceeds in managing memory in the most efficient way possible – but what if you need data structures that can be dynamic, such as a dynamically sized array, or what if you need global variables? This is where the heap comes into play.

#### The Heap

The heap is a memory store also in RAM that allows for **dynamic memory allocation**, and does not work on a stack-like basis; it’s more just a hub of storage for you to define your variables. Once you allocate a memory location on the heap to store a variable, that variable can be **accessed at any point in time** not only throughout just the thread, but throughout the application’s entire life. This is how you can define global variables. Once an application ends, all of the allocated memory locations are reclaimed by the CPU. The heap size is set on application startup, but unlike the stack there are no size restrictions on the heap (aside from the physical limitations of your machine), which means it can get ever larger as you allocate more memory to it. This is what allows you to create variables that can be dynamically resized, since the heap itself is dynamic in size.

You interact with the heap via **references** (pointers), which are variables whose values are the address of another variable, such as a memory location. By creating a pointer, you 'point' at a memory location on the heap, which is what signifies the initial location of your variable and tells the program where to access the value. Due to the dynamic nature of the heap, it is **completely unmanaged by the CPU** aside from initial allocation and heap resizing; in non-garbage collected languages such as C and C++, this requires you as the developer to manage memory and to manually free memory locations when they are no longer needed. Failing to do so can create memory leaks and cause memory to become fragmented, which will cause reads from the heap to take longer and makes it difficult to continuously allocate more memory onto the heap.

Compared to the stack, the heap is **slower to access** because variables are scattered across memory instead of always sitting at the top of the stack. Improper memory management of the heap can also slow down reading from the heap; however, this shouldn’t detract from its importance – you absolutely need it to create any type of variable dynamically, or global variables.

#### Final Thoughts

The importance of the stack and the heap really comes into play with **non-garbage collected languages** where you need to manage memory yourself – and while modern languages do abstract away the need for this, they’re all still doing it under the scenes. Different languages use the stack and the heap differently; C and C++ allocate to the stack automatically, and you as the developer manually have to allocate and deallocate from the heap, where more modern languages such as Go and Java allocate to both the stack and the heap automatically, and have a garbage collector that handles heap deallocation on its own. Languages like Ruby and Python allocate everything on the heap and don’t use a stack at all.

### Compiled And Interpreted Languages

### Concurrency

### Static vs Dynamic Type Checking

### Type Introspection and Reflection

### Core functionnal Programming Concepts

### Garbage Collection

## Programming Paradigms

- [Wikipedia](https://en.wikipedia.org/wiki/Programming_paradigm)
- [Programming Paradigms](https://cs.lmu.edu/~ray/notes/paradigms/)
- [Introduction of Programming Paradigms](https://www.geeksforgeeks.org/introduction-of-programming-paradigms/)
- [A must know for all programmers](https://hackr.io/blog/programming-paradigms)

### Imperative

### Declarative

### Structured

### Procedural

### Functional

### Function-Level

### Event-Driven

### Flow-Driven

### Logic

### Constaint

### Aspect-Oriented

### Reflective

### Array

## Programming Best Practices

### GoF Design Patterns

[**Creational patterns**](https://en.wikipedia.org/wiki/Creational_pattern) provide the capability to create objects based on a required criterion and in a controlled way:

- **Abstract Factory**: Allows the creation of objects without specifying their concrete type.
- **Builder**: Uses to create complex objects.
- **Factory Method**: Creates objects without specifying the exact class to create.
- **Prototype**: Creates a new object from an existing object.
- **Singleton**: Ensures only one instance of an object is created.

[**Structural patterns**](https://en.wikipedia.org/wiki/Structural_pattern) are about organizing different classes and objects to form larger structures and provide new functionality:

- **Adapter**: Allows for two incompatible classes to work together by wrapping an interface around one of the existing classes.
- **Bridge**: Decouples an abstraction so two classes can vary independently.
- **Composite**: Takes a group of objects into a single object.
- **Decorator**: Allows for an object’s behavior to be extended dynamically at run time.
- **Facade**: Provides a simple interface to a more complex underlying object.
- **Flyweight**: Reduces the cost of complex object models.
- **Proxy**: Provides a placeholder interface to an underlying object to control access, reduce cost, or reduce complexity.

[**Behavioral patterns**](https://en.wikipedia.org/wiki/Behavioral_pattern) are about identifying common communication patterns between objects and realize these patterns:

- **Chain of Responsibility**: Delegates commands to a chain of processing objects.
- **Command**: Creates objects which encapsulate actions and parameters.
- **Interpreter**: Implements a specialized language.
- **Iterator**: Accesses the elements of an object sequentially without exposing its underlying representation.
- **Mediator**: Allows loose coupling between classes by being the only class that has detailed knowledge of their methods.
- **Memento**: Provides the ability to restore an object to its previous state.
- **Observer**: Is a publish/subscribe pattern which allows a number of observer objects to see an event.
- **State**: Allows an object to alter its behavior when its internal state changes.
- **Strategy**: Allows one of a family of algorithms to be selected on-the-fly at run-time.
- **Template Method**: Defines the skeleton of an algorithm as an abstract class, allowing its sub-classes to provide concrete behavior.
- **Visitor**: Separates an algorithm from an object structure by moving the hierarchy of methods into one object.

### Coding Principles

- **Keep It Stupid Simple** (KISS): Keep your code very simple.
- **Don't Repeat Yourself** (DRY): Every repetitive behavior in the code should be extracted for later reuse.
- **You Aren't Gonna Need It** (YAGNI): Do not leave any code that's meant only for future extendability.
- **Single Level of Abstraction Principle** (SLAP): Functions should do just one thing (), and they should do it well (don´t mix different levels of abstraction).

[**SOLID**](https://www.digitalocean.com/community/conceptual_articles/s-o-l-i-d-the-first-five-principles-of-object-oriented-design):

- **Single-responsibility principle** (SRP): Every module, class or function in a computer program should have responsibility over a single part of that program's functionality, which it should encapsulate.
- **Open–closed principle** (OCP): Software entities \(classes, modules, functions, etc.\) should be open for extension, but closed for modification.
- **Liskov substitution principle** (LSP): If S is a subtype of T, then objects of type T may be replaced with objects of type S without altering any of the desirable properties of the program.
- **Interface segregation principle** (ISP): No client should be forced to depend on methods it does not use \(split interfaces that are very large into smaller and more specific ones\).
- **Dependency inversion principle** (DIP): High-level modules should not depend on low-level modules. Both should depend on abstractions. Abstractions should not depend on details. Details \(concrete implementations\) should depend on abstractions.

### [The Twelve-Factor App](https://12factor.net/)

- **Codebase**: One codebase tracked in revision control, many deploys
- **Dependencies**: Explicitly declare and isolate dependencies
- **Config**: Store config in the environment
- **Backing services**: Treat backing services as attached resources
- **Build, release, run**: Strictly separate build and run stages
- **Processes**: Execute the app as one or more stateless processes
- **Port binding**: Export services via port binding
- **Concurrency**: Scale out via the process model
- **Disposability**: Maximize robustness with fast startup and graceful shutdown
- **Dev/prod parity**: Keep development, staging, and production as similar as possible
- **Logs**: Treat logs as event streams
- **Admin processes**: Run admin/management tasks as one-off processes

### [Semantic Versioning](https://semver.org/)

In the world of software management there exists a dreaded place called "dependency hell":

- If the dependency specifications are too tight, you are in danger of version lock (the inability to upgrade a package without having to release new versions of every dependent package).
- If dependencies are specified too loosely, you will inevitably be bitten by version promiscuit.

The solution: given a version number MAJOR.MINOR.PATCH, increment the:

1. **MAJOR** version when you make incompatible API changes,
2. **MINOR** version when you add functionality in a backwards compatible manner, and
3. **PATCH** version when you make backwards compatible bug fixes.

Additional labels for pre-release and build metadata are available as extensions to the **MAJOR.MINOR.PATCH** format.

[Regex](https://regex101.com/r/vkijKf/1/) to check a SemVer string: `^(0|[1-9]\d*)\.(0|[1-9]\d*)\.(0|[1-9]\d*)(?:-((?:0|[1-9]\d*|\d*[a-zA-Z-][0-9a-zA-Z-]*)(?:\.(?:0|[1-9]\d*|\d*[a-zA-Z-][0-9a-zA-Z-]*))*))?(?:\+([0-9a-zA-Z-]+(?:\.[0-9a-zA-Z-]+)*))?$`

## Programming Languages

### Erlang / Elixir

#### Resources

- High level concepts of Erlang: [The Zen of Erlang](https://ferd.ca/the-zen-of-erlang.html)
- Learning tutorial: [Learn You Some Erlang for Great Good!](https://learnyousomeerlang.com/introduction#about-this-tutorial)
- How to write systems using Erlang: [Programming Rules and Conventions](http://www.erlang.se/doc/programming_rules.shtml)
- [Erlang Coding Standards & Guidelines](https://github.com/inaka/erlang_guidelines)
- Quick syntax introduction: [Erlang/Elixir Syntax: A Crash Course](https://elixir-lang.org/crash-course.html)
- Community [Elixir Style Guide](https://github.com/christopheradams/elixir_style_guide)

### Golang

#### [Go Proverbs](https://go-proverbs.github.io/)

- Don't communicate by sharing memory, share memory by communicating.
- Concurrency is not parallelism.
- Channels orchestrate; mutexes serialize.
- The bigger the interface, the weaker the abstraction.
- Make the zero value useful.
- interface{} says nothing.
- Gofmt's style is no one's favorite, yet gofmt is everyone's favorite.
- A little copying is better than a little dependency.
- Syscall must always be guarded with build tags.
- Cgo must always be guarded with build tags.
- Cgo is not Go.
- With the unsafe package there are no guarantees.
- Clear is better than clever.
- Reflection is never clear.
- Errors are values.
- Don't just check errors, handle them gracefully.
- Design the architecture, name the components, document the details.
- Documentation is for users.
- Don't panic.

#### Resources

- Tips for writing clear, idiomatic Go code: [Effective Go](https://golang.org/doc/effective_go.html)
- Common comments made during reviews of Go code: [CodeReviewComments](https://github.com/golang/go/wiki/CodeReviewComments)
- Small supplement to CodeReviewComments: [Idiomatic Go](https://dmitri.shuralyov.com/idiomatic-go#use-consistent-spelling-of-certain-words)
- Real world advice for writing maintainable Go programs: [Practical Go](https://dave.cheney.net/practical-go/presentations/qcon-china.html)
- Language Design in the Service of Software Engineering: [Go at Google](https://talks.golang.org/2012/splash.article)
- [Idiomatic Go](https://dmitri.shuralyov.com/idiomatic-go#use-consistent-spelling-of-certain-words)
- The Dos and Don'ts of writing Go code at Uber: [Uber Go Style Guide](https://github.com/uber-go/guide/blob/master/style.md)
- Programming in an industrial context: [Go for Industrial Programming](https://peter.bourgon.org/go-for-industrial-programming/)
- Best practices from 2016: [Go best practices, six years in](https://peter.bourgon.org/go-best-practices-2016/)
- Common good practices for go packages: [Style guideline for Go packages](https://rakyll.org/style-packages/)
- [Network Programming with Go](https://tumregels.github.io/Network-Programming-with-Go/)
- Collection of Technical Interview Questions solved with Go: [go-interview](https://github.com/shomali11/go-interview/blob/master/README.md)
- [Darker Corners of Go](https://rytisbiel.com/2021/03/06/darker-corners-of-go/)

### Python

#### [The Zen of Python](https://www.python.org/dev/peps/pep-0020/)

- Beautiful is better than ugly.
- Explicit is better than implicit.
- Simple is better than complex.
- Complex is better than complicated.
- Flat is better than nested.
- Sparse is better than dense.
- Readability counts.
- Special cases aren't special enough to break the rules.
- Although practicality beats purity.
- Errors should never pass silently.
- Unless explicitly silenced.
- In the face of ambiguity, refuse the temptation to guess.
- There should be one-- and preferably only one --obvious way to do it.
- Although that way may not be obvious at first unless you're Dutch.
- Now is better than never.
- Although never is often better than _right_ now.
- If the implementation is hard to explain, it's a bad idea.
- If the implementation is easy to explain, it may be a good idea.
- Namespaces are one honking great idea -- let's do more of those!

#### Resources

- [PEP8](https://www.python.org/dev/peps/pep-0008/)
- [Google Python Style Guide](http://google.github.io/styleguide/pyguide.html)
- [What the f\*ck Python!](https://github.com/satwikkansal/wtfpython)
- [Python behind the scenes](https://tenthousandmeters.com/tag/python-behind-the-scenes/)

### JavaScript

#### Resources

- [ECMAScript 6 features](https://github.com/lukehoban/es6features)
- [AirBnb style guide](https://github.com/airbnb/javascript)
- [The modern JavaScript tutorial](https://javascript.info/)
- [Google JavaScript Style Guide](https://google.github.io/styleguide/jsguide.html)

### Bash

#### Resources

- [Google Shell Style Guide](https://google.github.io/styleguide/shellguide.html)

## Templates

### Self Documenting Makefile

Avoid documentation of Make targets in a Readme.md or something similar: the Makefiles get updated, not the documentation. Add documentation for each target of the Makefile and view it as a make target \(eg. make help\).

Requirements: `make` and `awk`

```text
.DEFAULT_GOAL:=help
SHELL:=/bin/bash

.PHONY: help deps clean build watch

help:  ## Display this help
    @awk 'BEGIN {FS = ":.*##"; printf "\nUsage:\n  make \033[36mtarget\033[0m \033[36m\033[0m\n\nTargets:\n"} /^[a-zA-Z_-]+:.*?##/ { printf "  \033[36m%-10s\033[0m %s\n", $$1, $$2 }' $(MAKEFILE_LIST)

deps:  ## Check dependencies
    $(info Checking and getting dependencies)

clean: ## Cleanup the project folders
    $(info Cleaning up things)

build: clean deps ## Build the project
    $(info Building the project)

watch: clean deps ## Watch file changes and build
    $(info Watching and building the project)
```

Output:

```text
$ make

Usage:
  make target

Targets:
  help        Display this help
  deps        Check dependencies
  clean       Cleanup the project folders
  build       Build the project
  watch       Watch file changes and build
```

### Architectural Decision Records

#### ADR Best Practices

Characteristics of a good [ADR](https://github.com/joelparkerhenderson/architecture_decision_record):

- **Point in Time** - Identify when the AD was made
- **Rationality** - Explain the reason for making the particular AD
- **Immutable record** - The decisions made in a previously published ADR should not be altered
- **Specificity** - Each ADR should be about a single AD

Characteristics of good **context**:

- Explain your organization's situation and business priorities
- Include rationale and considerations based on social and skills makeups of your teams

Characteristics of good **consequences**:

- Right approach - "We need to start doing X instead of Y"
- Wrong approach - Do not explain the AD in terms of "Pros" and "Cons" of having made the particular AD

A new ADR may take the place of a previous ADR: when an AD is made that **replaces or invalidates** a previous ADR, a new ADR should be created.

#### [MADR](https://adr.github.io/madr) Template

```
# [Short title of solved problem and solution] [#ADR_NUMBER]

- Status: [proposed | rejected | accepted | deprecated | … | superseded by [ADR-0005](0005-example.md)] <!-- optional -->
- Deciders: [list everyone involved in the decision] <!-- optional -->
- Date: [YYYY-MM-DD when the decision was last updated] <!-- optional -->

Technical Story: [description | ticket/issue URL] <!-- optional -->

## Context and Problem Statement

[Describe the context and problem statement, e.g., in free form using two to three sentences. You may want to articulate the problem in form of a question.]

## Decision Drivers <!-- optional -->

- [driver 1, e.g., a force, facing concern, …]
- [driver 2, e.g., a force, facing concern, …]
- … <!-- numbers of drivers can vary -->

## Considered Options

- [option 1]
- [option 2]
- … <!-- numbers of options can vary -->

## Decision Outcome

Chosen option: "[option 1]", because [justification. e.g., only option, which meets k.o. criterion decision driver | which resolves force force | … | comes out best (see below)].

### Positive Consequences <!-- optional -->

- [e.g., improvement of quality attribute satisfaction, follow-up decisions required, …]
- …

### Negative Consequences <!-- optional -->

- [e.g., compromising quality attribute, follow-up decisions required, …]
- …

## Pros and Cons of the Options <!-- optional -->

### [option 1]

[example | description | pointer to more information | …] <!-- optional -->

- Good, because [argument a]
- Good, because [argument b]
- Bad, because [argument c]
- … <!-- numbers of pros and cons can vary -->

### [option n]

...

## Links <!-- optional -->

- [Link type] [Link to ADR] <!-- example: Refined by [ADR-0005](0005-example.md) -->
- … <!-- numbers of links can vary -->

```
