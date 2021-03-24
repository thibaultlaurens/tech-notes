# Software Engineering

**Software Engineering** is a systematic approach to the design, development, operation, and maintenance of a software system.

## Objectives

- **Maintainability:** The software should be able to evolve to meet changing requirements.
- **Correctness:** Requirements specified in the **SRS** should be correctly implemented.
- **Reusability:** The different modules of the product can easily be reused to develop new products.
- **Testability:** The software facilitates both the establishment of test criteria and the evaluation of the software with respect to those criteria.
- **Reliability:** The program can be expected to perform its desired function over an arbitrary time period.
- **Portability:** The software can be transferred from one computer system or environment to another.
- **Adaptability:** The software allows differing system constraints and user needs to be satisfied by making changes to the software.

## Software Development Models

### Systems Development Life Cycle

SDLC phases defined by the US Department of Justice:

- **Initiation**: The initiation of a system (or project) begins when a business need or opportunity is identified. A Project Manager should be appointed to manage the project. This business need is documented in a **Concept Proposal**. After the Concept Proposal is approved, the System Concept Development Phase begins.
- **System Concept Development**: Once a business need is approved, the approaches for accomplishing the concept are reviewed for **feasibility and appropriateness**. The **Systems Boundary** Document identifies the scope of the system and requires Senior Official approval and funding before beginning the Planning Phase.
- **Planning**: The concept is further developed to describe **how the business will operate** once the approved system is implemented. To ensure the products and /or services provide the required capability on-time and within budget, **project resources, activities, schedules, tools, and reviews are defined**. Additionally, security certification and accreditation activities begin with the identification of system security requirements and the completion of a high level vulnerability assessment.
- **Requirements Analysis**: Functional user requirements are formally defined and delineate the requirements in terms of **data, system performance, security, and maintainability requirements** for the system. All requirements are defined to a level of detail sufficient for systems design to proceed. All requirements need to be **measurable and testable** and relate to the business need or opportunity identified in the Initiation Phase.
- **Design**: The physical characteristics of the system are designed during this phase. **The operating environment is established, major subsystems and their inputs and outputs are defined, and processes are allocated to resources. Everything requiring user input or approval must be documented and reviewed by the user**. The physical characteristics of the system are specified and a detailed design is prepared. Subsystems identified during design are used to create a detailed structure of the system. Each subsystem is partitioned into one or more design units or modules. **Detailed logic specifications are prepared for each software module**.
- **Development**: The detailed specifications produced during the design phase are **translated into hardware, communications, and executable software**. Software shall be unit tested, integrated, and retested in a systematic manner. Hardware is assembled and tested.
- **Integration and Test**: The various components of the system are integrated and systematically tested. The user tests the system to ensure that the **functional requirements are satisfied** by the developed or modified system. Prior to installing and operating the system in a production environment, the system must undergo certification and accreditation activities.
- **Implementation**: The system or system modifications are installed and made operational in a production environment. The phase is initiated after the system has been tested and accepted by the user. This phase continues until the system is operating in production in accordance with the defined user requirements.
- **Operations and Maintenance**: The system operation is ongoing. The system is **monitored for continued performance** in accordance with user requirements, and needed system modifications are incorporated. The operational system is periodically assessed through In-Process Reviews to determine how the system can be made more efficient and effective. Operations continue as long as the system can be effectively adapted to respond to an organization’s needs. When modifications or changes are identified as necessary, the system may reenter the planning phase.
- **Disposition**: The disposition activities ensure the **orderly termination** of the system and **preserve the vital information about the system** so that some or all of the information may be reactivated in the future if necessary. Particular emphasis is given to proper **preservation of the data processed by the system**, so that the data is effectively migrated to another system or archived in accordance with applicable records management regulations and policies, for potential future access.

### Software Development Process

- **Agile development**: A group of software development methodologies based on **iterative development**, where requirements and solutions evolve via collaboration between self-organizing cross-functional teams. It uses iterative development as a basis but advocates a lighter and more people-centric viewpoint than traditional approaches. Agile processes fundamentally incorporate iteration and the continuous feedback that it provides to successively refine and deliver a software system.
- **Incremental development**: Various methods are acceptable for **combining linear and iterative systems development** methodologies, with the primary objective of each being to reduce inherent project risk by breaking a project into smaller segments and providing more ease-of-change during the development process. (ex: series of mini-Waterfalls for each parts of the system VS initial software concept, requirements analysis, and design of architecture and system core are defined via Waterfall, followed by incremental implementation etc.)
- **Rapid application development \(RAD\)**: Favors iterative development and the rapid construction of **prototypes** instead of large amounts of up-front planning. The "planning" of software developed using RAD is interleaved with writing the software itself. The lack of extensive pre-planning generally allows software to be written much faster, and makes it easier to change requirements.
- **Spiral development**: Combines some key aspect of the waterfall model and rapid prototyping methodologies, in an effort to combine advantages of top-down and bottom-up concepts. It provided emphasis in a key area many felt had been neglected by other methodologies: deliberate **iterative risk analysis**, particularly suited to large-scale complex systems.
- **Waterfall Model**: A sequential development approach, in which development is seen as flowing steadily downwards (like a waterfall) through several phases.
- **V-Shaped Model**: May be considered an extension of the waterfall model. Instead of moving down in a linear way, the process steps are bent upwards after the coding phase, to form the typical V shape. The V-Model demonstrates the relationships between each phase of the development life cycle and its associated phase of testing.
- Evolutionary Prototyping

### Agile Manifesto

- **Individuals and interactions** over processes and tools.
- **Working software** over comprehensive documentation.
- **Customer collaboration** over contract negotiation.
- **Responding to change** over following a plan.

## Software Requirements (TODO)

## Software Testing (TODO)

- https://en.wikipedia.org/wiki/Software\_testing

### The Seven Principles Of Software Testing

- **Testing shows presence of defects:** The goal of software testing is to make the software fail. It can ensure that defects are present but it can not prove that software is defects free. Testing can reduce the number of defects but not removes all defects.
- **Exhaustive testing is not possible:** The software can never test at every test cases \(in all possible inputs, valid or invalid, and pre-conditions\). It can test only some test cases and assume that software is correct and will produce the correct output in every test cases.
- **Early Testing:** To find the defect in the software, early test activity shall be started. The defect detected in early phases of **SDLC** are less expensive.
- **Defect clustering:** In a project, a small number of the module can contain most of the defects. The **Pareto Principle** applied to testing states that 80% of software defect comes from 20% of modules.
- **Pesticide paradox:** Repeating the same test cases again and again will not find new bugs.
- **Testing is context dependent:** Testing approach depends on context of software developed. Different types of software need to perform different types of testing.
- **Absence of errors fallacy:** If a built software is 99% bug-free but it does not follow the user requirement then it is unusable.

### Testing Approach

**Static, Dynamic and passive testing:**

**The "box" approach:**

- White box testing
- Black box testing
- Grey box testing

### Testing Levels

- Unit testing
- Integration testing
- System testing
- Acceptance testing

### Testing Types

- Smoke testing
- Regression testing
- Acceptance testing
- Alpha / Beta testing
- Performance testing
- Usability testing
- Security testing
- A/B testing

## Programming Concepts (TODO)

- [Programming Concepts](https://thecodeboss.dev/2014/10/programming-concepts-the-stack-and-the-heap/) \(faire toute la serie\)

### The Stack And The Heap

### Compiled And Interpreted Languages

### Concurrency

### Static vs Dynamic Type Checking

### Type Introspection and Reflection

### Core functionnal Programming Concepts

### Garbage Collection

## Best Practices

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

## Languages

### Erlang / Elixir

Resources:

- High level concepts of Erlang: [The Zen of Erlang](https://ferd.ca/the-zen-of-erlang.html)
- Learning tutorial: [Learn You Some Erlang for Great Good!](https://learnyousomeerlang.com/introduction#about-this-tutorial)
- How to write systems using Erlang: [Programming Rules and Conventions](http://www.erlang.se/doc/programming_rules.shtml)
- [Erlang Coding Standards & Guidelines](https://github.com/inaka/erlang_guidelines)
- Quick syntax introduction: [Erlang/Elixir Syntax: A Crash Course](https://elixir-lang.org/crash-course.html)
- Community [Elixir Style Guide](https://github.com/christopheradams/elixir_style_guide)

### Golang

[Go Proverbs](https://go-proverbs.github.io/):

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

Resources:

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

[The Zen of Python](https://www.python.org/dev/peps/pep-0020/)

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

Resources:

- [PEP8](https://www.python.org/dev/peps/pep-0008/)
- [Google Python Style Guide](http://google.github.io/styleguide/pyguide.html)
- [What the f\*ck Python!](https://github.com/satwikkansal/wtfpython)
- [Python behind the scenes](https://tenthousandmeters.com/tag/python-behind-the-scenes/)

### JavaScript

Resources:

- [ECMAScript 6 features](https://github.com/lukehoban/es6features)
- [AirBnb style guide](https://github.com/airbnb/javascript)
- [The modern JavaScript tutorial](https://javascript.info/)
- [Google JavaScript Style Guide](https://google.github.io/styleguide/jsguide.html)

### Bash

Resources:

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

Characteristics of a good ADR:

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

## Resources

- [US Department of Justice SDLC](https://www.justice.gov/archive/jmd/irm/lifecycle/ch1.htm#para1.2)
- [Agile Manifesto](https://agilemanifesto.org/)
- [Software Engineering/](https://www.geeksforgeeks.org/software-engineering/)
- [ADR GitHub organization](https://adr.github.io/)
- [Architecture decision record](https://github.com/joelparkerhenderson/architecture_decision_record)
