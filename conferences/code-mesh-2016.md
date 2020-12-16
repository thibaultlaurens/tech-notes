# CODE MESH 2016

## Keynote: SpaceMonads

By Conor McBride - Computer & Information Sciences Lecturer @ University of Strathclyde - [link](https://www.codemesh.io/codemesh2016/conor-mcbride)

Livehacking in **Agda**, I'll show how space (in this case, rectangular spaces on your screen) has a **monadic structure**, and build something a little bit like a window-manager before your very eyes (apart from the bits that are behind other windows, which will, of course, remain out of sight). On the way, I'll need to refine some standard testing machinery to produce evidence about what is being tested, and demonstrate that Tony Hoare basically understood monads for dependent types before I was born. The video of this talk will scupper a homework I was thinking of setting my fourth-years, but I don't care.

Takeaway:

- [Agda](https://github.com/agda/agda): a dependently typed programming language
- [Quickcheck](https://hackage.haskell.org/package/QuickCheck): a library for random testing of program properties

## Conflict Resolution for Eventual Consistency

By Martin Kleppmann - Insufferable Distributed Systems Nut - [link](https://www.codemesh.io/codemesh2016/martin-kleppmann)

What do collaborative editors like Google Docs, the calendar app on your phone, and multi-datacenter database clusters have in common?

Answer: They all need to cope with network interruptions, and still work offline. They all allow state to be updated concurrently in several different places, and asynchronously propagate changes to other nodes. If data is concurrently changed on different nodes, you get conflicts that need to be resolved.

There are different approaches to handling those conflicts: some systems let the user manually resolve them; some systems choose one version as the winner and throw away the other versions; and some systems try to merge concurrent updates automatically. For example, Google Docs uses an algorithm called **Operational Transform** (OT) to perform this merge, while Riak uses **Conflict-Free Replicated Datatypes** (CRDTs) to achieve a similar thing.

In this talk we will explore these algorithms for automatic merging. They start out quite simple, but as we shall see, they soon become fascinatingly mind-bending once you start trying to do more ambitious things. For example, if you wanted to write your own spreadsheet app or graphics software that allows several users to edit the same document concurrently, how would you go about doing that?

Takeaway:

- [Operational Transform](https://en.wikipedia.org/wiki/Operational_transformation): a technology for supporting a range of collaboration functionalities in advanced collaborative software systems.
- [Conflict-Free Replicated Datatypes](https://en.wikipedia.org/wiki/Conflict-free_replicated_data_type): a data structure which can be replicated across multiple computers in a network, where the replicas can be updated independently and concurrently without coordination between the replicas, and where it is always mathematically possible to resolve inconsistencies that might come up.

## New Problems, New Paradigms

By Mark Priestley - Writer, historian, amateur Rubyist - [link](https://www.codemesh.io/codemesh2016/mark-priestley)

Why are new programming languages developed? When do new languages give rise to new programming paradigms? This talk will explore these questions by looking at the early history of Lisp, the first "alternative" language.

Takeway:

- 1930s: [λ-calculus](https://en.wikipedia.org/wiki/Lambda_calculus): a formal system in mathematical logic for **expressing computation based on function abstraction and application** using variable binding and substitution. It is a universal model of computation that can be used to simulate any Turing machine.
- 1956: [Information Processing Language](https://en.wikipedia.org/wiki/Information_Processing_Language) (IPL), includes features intended to help with programs that perform simple problem solving actions such as lists, dynamic memory allocation, data types, recursion, functions as arguments, generators, and cooperative multitasking. IPL invented the concept of **list processing**, albeit in an assembly-language style.
- 1957: [Fortran](https://en.wikipedia.org/wiki/Fortran), a general-purpose, compiled imperative programming language that is especially suited to **numeric computation** and scientific computing.
- 1958: [Lisp](https://lisp-lang.org/) pioneered many ideas in computer science, including tree data structures, automatic storage management, dynamic typing, conditionals, higher-order functions, **recursion**, the self-hosting compiler, and the read–eval–print loop. **Linked lists** are one of Lisp's major data structures, and Lisp source code is made of lists. Thus, Lisp programs can manipulate source code as a data structure, giving rise to the macro systems that allow programmers to create new syntax or new domain-specific languages embedded in Lisp.

## A Brief History of Distributed Programming: RPC

By Caitie McCaffrey - Backend Brat & Distributed Systems Diva @ Twitter - [link](https://www.codemesh.io/codemesh2016/caitie-mccaffrey)

While many of the distributed systems we operate today are built with language like Java and Go, distributed programming has a long history of innovation and adoption of its ideas. This include innovations seen all throughout the various fields of computing: novel type systems for dynamic languages; the concept of the promise, now a standard programming technique in web development; and unified models of programming when data lives across nodes. Some of these ideas had major impact, while some fell incredibly short. Many technically superior ideas were not adopted simply because they were too “research” focused.

During this talk, we will present the history of RPC and why RPC may not be the best abstraction for building your next distributed application.

Takeways:

- **Concurrent** (Nodejs, Golang..) vs **Distributed** (Erlang) programming languages
- [Cloud Haskell](https://haskell-distributed.github.io/): a library for distributed concurrency in Haskell. A generic network transport API, libraries for sending static closures to remote nodes, a rich API for distributed programming and a set of platform libraries modelled after Erlang’s Open Telecom Platform.
- 1970s: RPC RFCs and proposals (1974: **Procedure Call Paradigm** (PCP))
- 1980s: RPC implementations
- 1989: RFC 1094 - NFS: **Network File System** Protocol Specification (soft vs hard mouting)
- 1990s: CORBA (**Common Object Request Broker Architecture**) as an alternative model of remote method invocation (**RMI**)
- 1994: [A Note on Distributed System](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.41.7628), two path forward: Treat all objects as local or treat all objects as remote.
- Today: Modern RPC frameworks: [Finagle](https://twitter.github.io/finagle/) and [gRPC](https://grpc.io/).
- Future: Lasp, CALM, Spores

## Web Programming without Errors, and Coding without Typing

By Jessica Kerr - Infrastructure Developer @ Stripe - [link](https://www.codemesh.io/codemesh2016/jessica-kerr)

This session demonstrates two new ways of programming.

First, Elm is a purely functional programmingl language for the browser, with strict immutability, types, semantic versioning -- and it is kind, with a focus on developer experience. The language leads to the Elm Architecture, a declarative event-based model that can teach us clean ways to think about processing in any language.
Elm code is very explicit. Compared to frameworks that do magical wiring, this can require more typing. Sometimes I wish I had a pair to do the grunt work for me, and now I do!

Atomist Editors translate an intention into a pull request, modifying my code in place, leaving me to express the business logic. The wiring is done for me, without sacrificing clarity. You'll see my Editors writing Elm, but you can make Editors operate on any language!

Elm plus Atomist: front-end development with zero runtime exceptions, clear code, clean architecture, and much joy.

Takeways:

- [Elm](https://elm-lang.org/)
- [Atomist](https://atomist.com/)

## Distributed Consensus: Making Impossible Possible

By Heidi Howard - PhD Student in Distributed Consensus - [link](https://www.codemesh.io/codemesh2016/heidi-howard)

In this talk, we explore how to construct resilient distributed systems on top of unreliable components.

Starting, almost two decades ago, with Leslie Lamport’s work on organising parliament for a Greek island. We will take a journey to today’s datacenters and the systems powering companies like Google, Amazon and Microsoft. Along the way, we will face interesting impossibility results, machines acting maliciously and the complexity of today’s networks.

Ultimately, we will discover how to reach agreement between many parties and from this, how to construct new fault-tolerance systems that we can depend upon everyday.

Takeways:

- Paper: **Flexible Paxos**: Reaching agreement without Majorities
- Consensus: Reaching agreement in an **asynchronous** distributed system in the face of **crash failure**.
- The Key ideas from distributed consensus come from the paper **The part-Time Parliement** bye Leslie Lamport ([Paxos](<https://en.wikipedia.org/wiki/Paxos_(computer_science)>)).
- Another famous consensus algorithm: [Raft](https://raft.github.io/) a more understandable version of Paxos (and a little bit different as well).
- **Quorum**: the minimum number of votes that a distributed transaction has to obtain in order to be allowed to perform an operation in a distributed system.
- **Repliation** quorum vs **Leader election** quorum.
- Flexible paxos (no majority) is: Replication quorum + Leader election quorum = Number of nodes + 1
- So for 6 nodes you can do replication with 2 and election with 5 (fast replication and slow/resilient election)

## Checmate: Lying, Cheating, and Winning with Containers in Networking

By Sargun Dhillon - Distributed Systems Specialist @ Mesosphere - [link](https://www.codemesh.io/codemesh2016/sargun-dhillon)

Containers have become ubiquitous in modern infrastructure. Containers have become the de facto mechanism of deploying and operating production software in recent years. Containerizaton technology has resulted in a fundamental paradigm shift in multitenant computing. Unfortunately, networking in containers never caught up with this modern mechanism. As opposed to manipulating the tenant's perspective of the system using the OS, containers are still using virtualization techniques. In this talk, we present Checmate, a system that is resident to the Linux kernel, that implements microsegmentation and load balancing of containers with nearly undetectable overhead. This system is powered by a control plane in Erlang, with a custom compiler to ease the creation of new Checmate rules. These components work together to provide a modern approach to container networking.

Takeway:

- [Berkeley Packet Filter](https://en.wikipedia.org/wiki/Berkeley_Packet_Filter) (BPF): Provides a raw interface to data link layers, permitting raw link-layer packets to be sent and received. BPF supports filtering packets, allowing a userspace process to supply a filter program that specifies which packets it wants to receive.
- Checmate and Checmate's control plane as an alternative to the way the container networking works today.
