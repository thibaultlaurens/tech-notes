---
description: The big ideas behind reliable, scalable and maintainable systems
---

# Designing Data-Intensive Applications

# Part I. Foundations of Data Systems

## 1. Reliable, Scalable, and Maintainable Applications

### Thinking About Data Systems

A data-intensive application is typically built from standard building blocks that provide commonly needed functionality:

- Store data so that they, or another application, can find it again later (**databases**)
- Remember the result of an expensive operation, to speed up reads (**caches**)
- Allow users to search data by keyword or filter it in various ways (**search indexes**)
- Send a message to another process, to be handled asynchronously (**stream processing**)
- Periodically crunch a large amount of accumulated data (**batch processing**)

If you are designing a data system or service, a lot of tricky questions arise:

- How do you ensure that the data remains correct and complete, even when things go wrong internally ?
- How do you provide consistently good performance to clients, even when parts of your system are degraded ?
- How do you scale to handle an increase in load ?
- What does a good API for the service look like ?

In this book, we focus on three concerns that are important in most software systems:

- **Reliability**: The system should continue to work correctly (performing the correct function at the desired level of performance) even in the face of adversity (hardware or software faults, and even human error).
- **Scalability**: As the system grows (in data volume, traffic volume, or complexity), there should be reasonable ways of dealing with that growth.
- **Maintainability**: Over time, many different people will work on the system (engineering and operations, both maintaining current behavior and adapting the system to new use cases), and they should all be able to work on it productively

### Reliability

Expectations:

- The application performs the function that the user expected.
- It can tolerate the user making mistakes or using the software in unexpected ways.
- Its performance is good enough for the required use case, under the expected load and data volume.
- The system prevents any unauthorized access and abuse.

Faults:

- A **fault** is usually defined as one component of the system deviating from its spec, whereas a **failure** is when the system as a whole stops providing the required service to the user.
- It is impossible to reduce the probability of a fault to zero; therefore it is usually best to design **fault-tolerance mechanisms that prevent faults from causing failures**.
- Fault-tolerance should cover hardware, software and configuration errors.

### Scalability

Describing Load:

- Load can be described with a few numbers which we call **load parameters**.
- Perhaps the average case is what matters for you, or perhaps your bottleneck is dominated by a small number of extreme cases.
- When you increase a load parameter and keep the system resources (CPU, memory, network bandwidth, etc.) unchanged, how is the performance of your system affected ?
- When you increase a load parameter, how much do you need to increase the resources if you want to keep performance unchanged ?

Describing Performance:

- In a batch processing system, we usually care about **throughput** (the number of records we can process per second, or the total time it takes to run a job on a dataset of a certain size) vs in online systems, what’s usually more important is the service’s **response time**.
- Side note: latency and response time are often used synonymously, but they are not the same. **Latency** is the duration that a request is waiting to be handled vs response time is what the client sees.
- We need to think of response time not as a single number, but as a distribution of values that we can measure. The average (arithmetic mean) is not a very good metric, we should use the **median or P50** (half of user requests are served in less than the P50)
- To figure out how bad our outliers are, we can look at higher percentiles: the 95th, 99th, and 99.9th percentiles (abbreviated **p95, p99, and p999**). High percentiles of response times, also known as **tail latencies**, are important because they directly affect users’ experience of the service.
- Reducing response times at very high percentiles is difficult because they are easily affected by random events outside of your control, and the benefits are diminishing.
- Percentiles are often used in **service level objectives (SLOs)** and **service level agreements (SLAs)**, contracts that define the expected performance and availability of a service.
- **Head-of-line blocking**: When a number of slow requests hold up the processing of subsequent requests
- **Tail latency amplification**: When making calls in parallel, the end-user request still needs to wait for the slowest of the parallel calls to complete.
- Note: averaging percentiles, e.g., to reduce the time resolution or to combine data from several machines, is **mathematically meaningless**. The right way of aggregating response time data is to add the histograms.

Approaches for Coping with Load:

- You will need to rethink your architecture on every order of magnitude load increase.
- Scaling up (vertical scaling, moving to a more powerful machine) and scaling out (horizontal scaling, distributing the load across multiple smaller machines).
- Distributing load across multiple machines is also known as a **shared-nothing architecture**.
- Some systems are **elastic** whereas other systems are scaled manually. An elastic system can be useful if load is highly unpredictable, but manually scaled systems are simpler and may have fewer operational surprises.

### Maintainability

The majority of the cost of software is not in its initial development, but in its ongoing maintenance: fixing bugs, keeping its systems operational, investigating failures, adapting it to new platforms, modifying it for new use cases, repaying technical debt, and adding new features. We will pay particular attention to three design principles for software systems:

- **Operability**: Make it easy for operations teams to keep the system running smoothly.
- **Simplicity**: Make it easy for new engineers to understand the system, by removing as much complexity as possible from the system.
- **Evolvability**: Make it easy for engineers to make changes to the system in the future, adapting it for unanticipated use cases as requirements change.

## 2. Data Models and Query Languages
