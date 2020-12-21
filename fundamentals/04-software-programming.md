# Software Programming

## Programming concepts

- [Programming Concepts](https://thecodeboss.dev/2014/10/programming-concepts-the-stack-and-the-heap/) \(faire toute la serie\)

### The Stack and the Heap

### Compiled and Interpreted languages

### Concurrency

### Static vs Dynamic type checking

### Type Introspection and Reflection

### Core functionnal Programming Concepts

### Garbage Collection

## Git

Git is a **distributed version-control system** for tracking changes in any set of files, originally designed for coordinating work among programmers cooperating on source code during software development. Its goals include speed, data integrity, and support for distributed, non-linear workflows. It was created by **Linus Torvalds in 2005** for development of the Linux kernel. ([wikipedia](https://en.wikipedia.org/wiki/Git))

### Basics

#### Objects

- All commits are stored as a **tree** like data structure internally by git. That means there can be two or more children commits of a given commit.
- Everything in git is an **object**. Newly created files are stored as an object. Changes to file are stored as an objects and even commits are objects.
- All the objects are stored in the `.git/objects/` directory.

#### References

There are multiple ways to **reference to a version** of the code (except by commit id)

- a branch reference, stored in `.git/refs/heads` (ex: `.git/refs/heads/master` would point to a commit object).
- `HEAD`: a reference to the current checked out commit, stored in a file at `.git/HEAD` (ex: on master branch, `.git/HEAD` would point to `.git/refs/heads/master`)
- `HEAD~1`: a reference to the previous commit

#### Branches

- From a commit, multiple branches can be created and branches can also be merged. Using branches, there can exist multiple lines of histories and we can checkout to any of them and work on it.
- Internally, git is just **a tree of commits**. Branch names are pointers to those commits in the tree. We use various git commands to work with the tree structure and references.
- **Merges** options: directly merge the branch (creates a merge commit -> ugly history) or **rebase** (take the branch and "put its commits on top of another one" -> clean history)

#### More

- **Squash**:
- **Amend**:
- **Stash**:
- **Reset**:

### References

#### Hashes

The most direct way to reference a commit is via its **SHA-1 hash**. This acts as the unique ID for each commit. To find the commit hash of an indirect reference: `git rev-parse [ref]`.

#### Refs

A ref is an indirect way of referring to a commit. It can be seen as a user-friendly alias for a commit hash. Tha's how git represents branches and tags internally. Refs are stored as normal text files in the `.git/refs` directory.

```
.git/refs
├── heads/
│   └── master
├── remotes/
│   └── origin/
│       ├── HEAD
│       └── master
└── tags/
```

- The `.git/refs/heads` directory defines all the local branches. Files matche the name of a branch, and inside the file is a commit hash of the tip of the branch.
- The `.git/refs/tags` works the same way but contains tags instead of branches.
- The`.git/refs/remote` contains all the remotes as sub-directories (like **origin**) with all the remote branches.

#### Special Refs

In addition to the `.git/refs` directory, there are a few special refs that reside in the top-level `.git` directory. These files contain different content depending on their type and the state of the repository. The **HEAD** ref can contain either a **symbolic ref** (a reference to another ref) or a commit hash.

- **HEAD**: The currently checked-out commit/branch.
- **FETCH_HEAD**: The most recently fetched branch from a remote repo.
- **ORIG_HEAD**: A backup reference to HEAD before drastic changes to it.
- **MERGE_HEAD**: The commit(s) that you’re merging into the current branch with git merge.
- **CHERRY_PICK_HEAD**: The commit that you’re cherry-picking.

#### Relative Refs

- We can also refer to commits relative to another commit. The `~` character lets you reach **parent commits** (ex: `git show HEAD~2` displays the grandparent of HEAD). The `~` character will always follow the **first parent**.
- To follow a **different parent**, use the `^` character. For a merge commit, `git show HEAD^2` will show the parent commit from the branch that was merged.
- We can use more than one `^` character to move **more than one generation**. For a merge commit, `git show HEAD^2^1` will show the grandparent of HEAD that rests on the second parent.

![relative-refs](../.gitbook/assets/git-relative-refs.svg)

#### Refspecs

A refspec **maps a branch in the local repository to a branch in a remote repository**. It is specified as `[+]<src>:<dst>` (the optional `+` sign forces the remote repository to perform a non-fast-forward update). It allows us to manage remote branches using local git commands and to configure some advanced git push and git fetch behavior (ex: to delete a remote branch).

#### Reflog

The reflog is git’s **safety net**. It records almost every change made in your repository, regardless of whether you committed a snapshot or not. You can think of it as a chronological history of everything you’ve done in your local repo. To view the reflog: `git reflog`.

### Collaboration

#### Worflows

When working with a team on a Git managed project, it’s important to make sure the team is all in agreement on how the flow of changes will be applied.A

- Centralized Worflow
- Feature branch Worflow
- Gitflow
- GitHub flow
- Forking Workflow

![gitflow](../.gitbook/assets/git-gitflow.svg)

### Miscellaneous

- **Hooks**: Scripts that run automatically every time a particular event occurs in a git repository. They let you customize Git’s internal behavior and trigger customizable actions at key points in the development life cycle. They are stored in `.git/hooks`. Hooks are local to a git repository, and are **not copied over** to the new repository when doing a `git clone`.
- **Submodules** (a pointer to a specific commit in another repository, easier to push into) vs **subtrees** (a copy of a repository that is pulled into a parent repository, easier to pull)
- **git cherry-pick**: Enables arbitrary Git commits to be picked by reference and appended to the current working HEAD. Cherry picking is the act of picking a commit from a branch and applying it to another.
- **Shallow clone**: Copy only recent revisions (pull down only the latest n commits of the repo’s history) with `git pull --depth [depth] [remote-url]`
- **git gc**: Clean up orphaned or inaccessible commits and compress group of similar objects into "packs" (`./git/objects/pack`). GC runs automatically on `pull`, `merge`, `rebase` and `commit` commands.
- **git prune**: Child command of `git gc` that cleans up unreachable or orphaned git objects.
- **LFS** (Large File Storage): A git extension that reduces the impact of large files in your repository. Large files are replaced with **tiny pointer files** and downloaded lazily, during the checkout process rather than during cloning or fetching.

### Resources

- [Documentation](https://git-scm.com/doc)
- [School of SRE](https://linkedin.github.io/school-of-sre/git/git-basics/)
- [Learn Git](https://www.atlassian.com/git/tutorials/learn-git-with-bitbucket-cloud)
- [A successful Git branching model](https://nvie.com/posts/a-successful-git-branching-model/)
- [GitHub flow](https://guides.github.com/introduction/flow/)

## Languages

### Erlang / Elixir

Resources:

- High level concepts of Erlang: [The Zen of Erlang](https://ferd.ca/the-zen-of-erlang.html)
- Learning tutorial: [Learn You Some Erlang for Great Good!](https://learnyousomeerlang.com/introduction#about-this-tutorial)
- How to write systems using Erlang: [Programming Rules and Conventions](http://www.erlang.se/doc/programming_rules.shtml)
- [Erlang Coding Standards & Guidelines](https://github.com/inaka/erlang_guidelines)
- Quick syntax introduction: [Erlang/Elixir Syntax: A Crash Course](https://elixir-lang.org/crash-course.html)
- Community:[ ](https://github.com/christopheradams/elixir_style_guide)[Elixir Style Guide](https://github.com/christopheradams/elixir_style_guide)

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
- [Google Style Guide](http://google.github.io/styleguide/pyguide.html)
- [What the f\*ck Python!](https://github.com/satwikkansal/wtfpython)
- [Python behind the scenes](https://tenthousandmeters.com/tag/python-behind-the-scenes/)

### Javascript

Resources:

- [ECMAScript 6 features](https://github.com/lukehoban/es6features)
- [AirBnb style guide](https://github.com/airbnb/javascript).
- [The modern JavaScript tutorial](https://javascript.info/)

## Best practices

### Design Pattern

### SOLID Principles

- [Single-responsibility principle](https://en.wikipedia.org/wiki/Single-responsibility_principle): Every module, class or function in a computer program should have responsibility over a single part of that program's functionality, which it should encapsulate.
- [Open–closed principle](https://en.wikipedia.org/wiki/Open%E2%80%93closed_principle): Software entities \(classes, modules, functions, etc.\) should be open for extension, but closed for modification.
- [Liskov substitution principle](https://en.wikipedia.org/wiki/Liskov_substitution_principle): If S is a subtype of T, then objects of type T may be replaced with objects of type S without altering any of the desirable properties of the program.
- [Interface segregation principle](https://en.wikipedia.org/wiki/Interface_segregation_principle): No client should be forced to depend on methods it does not use \(split interfaces that are very large into smaller and more specific ones\).
- [Dependency inversion principle](https://en.wikipedia.org/wiki/Dependency_inversion_principle): High-level modules should not depend on low-level modules. Both should depend on abstractions. Abstractions should not depend on details. Details \(concrete implementations\) should depend on abstractions.

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

## Templates

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
