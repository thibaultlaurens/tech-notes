# Software Engineering

**Software Engineering** is a systematic approach to the design, development, operation, and maintenance of a software system.

## Objectives

- **Maintainability:** The software should be able to evolve to meet changing requirements.
- **Correctness:** Requirements specified in the **SRS** (Software Requirements Specification) should be correctly implemented.
- **Reusability:** The different modules of the product can easily be reused to develop new products.
- **Testability:** The software facilitates both the establishment of test criteria and the evaluation of the software with respect to those criteria.
- **Reliability:** The program can be expected to perform its desired function over an arbitrary time period.
- **Portability:** The software can be transferred from one computer system or environment to another.
- **Adaptability:** The software allows differing system constraints and user needs to be satisfied by making changes to the software.

## Systems Development Life Cycle

SDLC phases defined by the US Department of Justice:

### Initiation

- A business need or opportunity is identified.
- A Project Manager is appointed.
- The business need is documented in a **Concept Proposal**.

### System Concept Development

- Review of the **feasibility and appropriateness** of the concept.
- A **Systems Boundary Document** identifies the scope of the system.
- Senior Official approval is required.

### Planning

- Describe **how the business will operate** once the system is implemented.
- To ensure the products provide the required capability on-time and within budget, **project resources, activities, schedules, tools, and reviews are defined**.
- Security certification and accreditation activities begin with the identification of system security requirements and the completion of a high level vulnerability assessment.

### Requirements Analysis

- **Functional user requirements** are formally defined and delineate the requirements in terms of **data, system performance, security, and maintainability requirements** for the system.
- All requirements are defined to a level of detail sufficient for systems design to proceed.
- All requirements need to be **measurable and testable** and relate to the business need or opportunity identified in the Initiation phase.

### Design

- The operating environment is established, major subsystems and their inputs and outputs are defined.
- **Everything requiring user input or approval must be documented and reviewed by the user**.
- The physical characteristics of the system are specified and a detailed design is prepared.
- Subsystems identified during design are used to create a detailed structure of the system.
- Each subsystem is partitioned into one or more design units or modules.
- **Detailed logic specifications are prepared for each software module**.

### Development

- The detailed specifications produced during the design phase are **translated into hardware, communications, and executable software**.
- Software shall be unit tested, integrated, and retested in a systematic manner.
- Hardware is assembled and tested.

### Integration and Test

- The various components of the system are integrated and systematically tested.
- The user tests the system to ensure that the **functional requirements are satisfied** by the developed or modified system.
- The system must undergo certification and accreditation activities.

### Operations and Maintenance

- The system or system modifications are installed and made operational in a production environment.
- The system is **monitored for continued performance** in accordance with user requirements, and needed system modifications are incorporated.
- The operational system is periodically assessed through In-Process Reviews to determine how the system can be made more efficient and effective.

### Disposition

- Ensure the **orderly termination** of the system and **preserve the vital information about the system** so that some or all of the information may be reactivated in the future if necessary.
- Particular emphasis is given to proper **preservation of the data processed by the system**.

## Software Development Processes

### Agile development

A group of software development methodologies based on **iterative development**, where requirements and solutions evolve via collaboration between self-organizing cross-functional teams. It uses iterative development as a basis but advocates a lighter and more people-centric viewpoint than traditional approaches. Agile processes fundamentally incorporate iteration and the continuous feedback that it provides to successively refine and deliver a software system.

### Incremental development

Various methods are acceptable for **combining linear and iterative systems development** methodologies, with the primary objective of each being to reduce inherent project risk by breaking a project into smaller segments and providing more ease-of-change during the development process. (ex: series of mini-Waterfalls for each parts of the system VS initial software concept, requirements analysis, and design of architecture and system core are defined via Waterfall, followed by incremental implementation etc.)

### Rapid application development \(RAD\)

Favors iterative development and the rapid construction of **prototypes** instead of large amounts of up-front planning. The "planning" of software developed using RAD is interleaved with writing the software itself. The lack of extensive pre-planning generally allows software to be written much faster, and makes it easier to change requirements.

### Spiral development

Combines some key aspect of the waterfall model and rapid prototyping methodologies, in an effort to combine advantages of top-down and bottom-up concepts. It provided emphasis in a key area many felt had been neglected by other methodologies: deliberate **iterative risk analysis**, particularly suited to large-scale complex systems.

### Waterfall Model

A sequential development approach, in which development is seen as flowing steadily **downwards** (like a waterfall) through several phases.

### V-Shaped Model

May be considered an extension of the waterfall model. Instead of moving down in a linear way, the process steps are bent upwards after the coding phase, to form the typical V shape. The V-Model demonstrates the relationships between each phase of the development life cycle and its **associated phase of testing**.

## Agile Manifesto

- **Individuals and interactions** over processes and tools.
- **Working software** over comprehensive documentation.
- **Customer collaboration** over contract negotiation.
- **Responding to change** over following a plan.

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

## Resources

- [US Department of Justice SDLC](https://www.justice.gov/archive/jmd/irm/lifecycle/ch1.htm#para1.2)
- [Agile Manifesto](https://agilemanifesto.org/)
- [Software Engineering/](https://www.geeksforgeeks.org/software-engineering/)
