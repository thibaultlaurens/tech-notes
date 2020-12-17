# Software Programming

## Algorithms & Data structures

### [Grokking Algorithms Review](https://docs.tlaurens.xyz/books/grokking-algorithms)

**TLDR**:

* Big O notation: constant, linear, logarithmic, linearithmic, square root, quadratic, cubic, polynomial, exponential, factorial
* Data structures: arrays, linked lists, hash tables, stacks, queues, graphs, sets
* Design: Tail recursion and Divide and conquer
* Search algorithms: linear search and binary search
* Sorting algorithms: insertion sort and selection sort \(simple sorts\), merge sort and quicksort \(efficient sorts\)
* Graph algorithms: Breadth-first search, Dijkstra’s algorithm, Bellman-Ford algorithm
* Greedy algorithms and NP-complete problems
* Dynamic Programming
* K-nearest neighbors \(KNN\)

### Indexing

* Binary Search Trees
* AVL Trees
* Red-Black Trees
* Splay Trees
* Open Hash Tables \(Closed Addressing\)
* Closed Hash Tables \(Open Addressing\)
* Closed Hash Tables, using buckets
* Trie \(Prefix Tree, 26-ary Tree\)
* Radix Tree \(Compact Trie\)
* Ternary Search Tree \(Trie with BST of children\)
* B Trees
* B+ Trees

### Sorting

* Bucket Sort
* Counting Sort
* Radix Sort
* Heap Sort

### Heap-like data structures

* Heaps
* Binomial Queues
* Fibonacci Heaps
* Leftist Heaps
* Skew Heaps

### Graphs algorithms

* Depth-First Search
* Connected Components
* Prim's Minimum Cost Spanning Tree
* Topological Sort \(Using Indegree array\)
* Topological Sort \(Using DFS\)
* Floyd-Warshall \(all pairs shortest paths\)
* Kruskal Minimum Cost Spanning Tree Algorithm

### Dynamic programming

* Calculating nth Fibonacci number
* Making Change
* Longest Common Subsequence

Resources:

* [https://www.bigocheatsheet.com/](https://www.bigocheatsheet.com/)
* [https://www.cs.usfca.edu/~galles/visualization/Algorithms.html](https://www.cs.usfca.edu/~galles/visualization/Algorithms.html)

## Programming concepts

* [Programming Concepts](https://thecodeboss.dev/2014/10/programming-concepts-the-stack-and-the-heap/) \(faire toute la serie\)

### The Stack and the Heap

### Compiled and Interpreted languages

### Concurrency

### Static vs Dynamic type checking

### Type Introspection and Reflection

### Core functionnal Programming Concepts

### Garbage Collection

## Programming Paradigms

* [Wikipedia](https://en.wikipedia.org/wiki/Programming_paradigm)
* [Programming Paradigms](https://cs.lmu.edu/~ray/notes/paradigms/)
* [Introduction of Programming Paradigms](https://www.geeksforgeeks.org/introduction-of-programming-paradigms/)
* [A must know for all programmers](https://hackr.io/blog/programming-paradigms)

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

## Best practices

### SOLID Principles

* [Single-responsibility principle](https://en.wikipedia.org/wiki/Single-responsibility_principle): Every module, class or function in a computer program should have responsibility over a single part of that program's functionality, which it should encapsulate.
* [Open–closed principle](https://en.wikipedia.org/wiki/Open%E2%80%93closed_principle): Software entities \(classes, modules, functions, etc.\) should be open for extension, but closed for modification.
* [Liskov substitution principle](https://en.wikipedia.org/wiki/Liskov_substitution_principle): If S is a subtype of T, then objects of type T may be replaced with objects of type S without altering any of the desirable properties of the program.
* [Interface segregation principle](https://en.wikipedia.org/wiki/Interface_segregation_principle): No client should be forced to depend on methods it does not use \(split interfaces that are very large into smaller and more specific ones\).
* [Dependency inversion principle](https://en.wikipedia.org/wiki/Dependency_inversion_principle): High-level modules should not depend on low-level modules. Both should depend on abstractions. Abstractions should not depend on details. Details \(concrete implementations\) should depend on abstractions.

### [The Twelve-Factor App](https://12factor.net/)

* **Codebase**: One codebase tracked in revision control, many deploys
* **Dependencies**: Explicitly declare and isolate dependencies
* **Config**: Store config in the environment
* **Backing services**: Treat backing services as attached resources
* **Build, release, run**: Strictly separate build and run stages
* **Processes**: Execute the app as one or more stateless processes
* **Port binding**: Export services via port binding
* **Concurrency**: Scale out via the process model
* **Disposability**: Maximize robustness with fast startup and graceful shutdown
* **Dev/prod parity**: Keep development, staging, and production as similar as possible
* **Logs**: Treat logs as event streams
* **Admin processes**: Run admin/management tasks as one-off processes

### Self documenting Makefile

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

## Git

* [https://linkedin.github.io/school-of-sre/git/git-basics/](https://linkedin.github.io/school-of-sre/git/git-basics/)

## Languages

### Erlang / Elixir

Resources:

* High level concepts of Erlang: [The Zen of Erlang](https://ferd.ca/the-zen-of-erlang.html)
* Learning tutorial: [Learn You Some Erlang for Great Good!](https://learnyousomeerlang.com/introduction#about-this-tutorial)
* How to write systems using Erlang: [Programming Rules and Conventions](http://www.erlang.se/doc/programming_rules.shtml)
* [Erlang Coding Standards & Guidelines](https://github.com/inaka/erlang_guidelines)
* Quick syntax introduction: [Erlang/Elixir Syntax: A Crash Course](https://elixir-lang.org/crash-course.html)
* Community:[ ](https://github.com/christopheradams/elixir_style_guide)[Elixir Style Guide](https://github.com/christopheradams/elixir_style_guide)

### Golang

[Go Proverbs](https://go-proverbs.github.io/):

* Don't communicate by sharing memory, share memory by communicating.
* Concurrency is not parallelism.
* Channels orchestrate; mutexes serialize.
* The bigger the interface, the weaker the abstraction.
* Make the zero value useful.
* interface{} says nothing.
* Gofmt's style is no one's favorite, yet gofmt is everyone's favorite.
* A little copying is better than a little dependency.
* Syscall must always be guarded with build tags.
* Cgo must always be guarded with build tags.
* Cgo is not Go.
* With the unsafe package there are no guarantees.
* Clear is better than clever.
* Reflection is never clear.
* Errors are values.
* Don't just check errors, handle them gracefully.
* Design the architecture, name the components, document the details.
* Documentation is for users.
* Don't panic.

Resources:

* Tips for writing clear, idiomatic Go code: [Effective Go](https://golang.org/doc/effective_go.html)
* Common comments made during reviews of Go code: [CodeReviewComments](https://github.com/golang/go/wiki/CodeReviewComments)
* Small supplement to CodeReviewComments: [Idiomatic Go](https://dmitri.shuralyov.com/idiomatic-go#use-consistent-spelling-of-certain-words)
* Real world advice for writing maintainable Go programs: [Practical Go](https://dave.cheney.net/practical-go/presentations/qcon-china.html)
* Language Design in the Service of Software Engineering: [Go at Google](https://talks.golang.org/2012/splash.article)
* [Idiomatic Go](https://dmitri.shuralyov.com/idiomatic-go#use-consistent-spelling-of-certain-words)
* The Dos and Don'ts of writing Go code at Uber: [Uber Go Style Guide](https://github.com/uber-go/guide/blob/master/style.md)
* Programming in an industrial context: [Go for Industrial Programming](https://peter.bourgon.org/go-for-industrial-programming/)
* Best practices from 2016: [Go best practices, six years in](https://peter.bourgon.org/go-best-practices-2016/)
* Common good practices for go packages: [Style guideline for Go packages](https://rakyll.org/style-packages/)
* [Network Programming with Go](https://tumregels.github.io/Network-Programming-with-Go/)
* Collection of Technical Interview Questions solved with Go: [go-interview](https://github.com/shomali11/go-interview/blob/master/README.md)

### Python

[The Zen of Python](https://www.python.org/dev/peps/pep-0020/)

* Beautiful is better than ugly.
* Explicit is better than implicit.
* Simple is better than complex.
* Complex is better than complicated.
* Flat is better than nested.
* Sparse is better than dense.
* Readability counts.
* Special cases aren't special enough to break the rules.
* Although practicality beats purity.
* Errors should never pass silently.
* Unless explicitly silenced.
* In the face of ambiguity, refuse the temptation to guess.
* There should be one-- and preferably only one --obvious way to do it.
* Although that way may not be obvious at first unless you're Dutch.
* Now is better than never.
* Although never is often better than _right_ now.
* If the implementation is hard to explain, it's a bad idea.
* If the implementation is easy to explain, it may be a good idea.
* Namespaces are one honking great idea -- let's do more of those!

Resources:

* [PEP8](https://www.python.org/dev/peps/pep-0008/)
* [Google Style Guide](http://google.github.io/styleguide/pyguide.html)
* [What the f\*ck Python!](https://github.com/satwikkansal/wtfpython)
* [Python behind the scenes](https://tenthousandmeters.com/tag/python-behind-the-scenes/)

### Javascript

Resources:

* [ECMAScript 6 features](https://github.com/lukehoban/es6features)
* [AirBnb style guide](https://github.com/airbnb/javascript).
* [The modern JavaScript tutorial](https://javascript.info/)
