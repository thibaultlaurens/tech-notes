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

## Software Development Models & Architecture

- https://medium.com/@melsatar/software-development-life-cycle-models-and-methodologies-297cfe616a3a
- https://en.wikipedia.org/wiki/Systems\_development\_life\_cycle"
- https://en.wikipedia.org/wiki/Software\_development\_process\#Waterfall\_development"

### Systems Development Life Cycle

- System Investigation
- Analysis
- Design
- Environments
- Testing
- Training and transition
- Operation and maintenance
- Evaluation

### Software Development Process

- Agile development
- Incremental development
- Rapid application development \(RAD\)
- Spiral development
- Waterfall Model
- V-Shaped Model
- Evolutionary Prototyping

## Software Requirements

## Software Testing and Debugging

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

## Architectural Decision Records

### ADR Best Practices

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

### [MADR](https://adr.github.io/madr) Template

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

- [Software Engineering/](https://www.geeksforgeeks.org/software-engineering/)
- [ADR GitHub organization](https://adr.github.io/)
- [Architecture decision record](https://github.com/joelparkerhenderson/architecture_decision_record)
