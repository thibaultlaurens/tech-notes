---
description: How Google runs production systems.
---

# Site Reliability Engineering

- [Google SRE book review](https://danluu.com/google-sre-book/)

## 1. Introduction

### The Sysadmin Approach to Service Management

- Assemble existing components and deploy them to produce a service
- Respond to events and updates as they occur
- Pros:
  - Easy to implement because it’s standard
  - Large talent pool to hire from
  - Lots of available software
- Cons
  - Manual intervention for change management and event handling
  - Size of the team need to scale with the load on system / service
  - Conflict between OPS \(the service has to be stable\) vs DEV \(the service needs new features and updates\)

### Goole's Approach to Service Management: Site Reliability Engineering

- Operations is done the "software engineer" way, with automation instead of manual labor
- Candidates should be able to pass the dev recruitment test \(and may have some additional skills that are rare among devs like L1 - L3 networking or UNIX system internals\).
- Results: SREs will be bored to do tasks by hand and will have the skillset to automate them
- To avoid manual labor trap: **50% cap on the amount of "ops" work** for SREs \(upper bound, actual amount of ops work is expected to be much lower\)
- Pros
  - Cheaper to scale
  - Circumvents devs/ops split
- Cons
  - Hard to hire for
  - Require management support

### Tenets of SRE

An SRE team is responsible for the **availability, latency, performance, efficiency, change management, monitoring, emergency response, and capacity planning** of their services.

**Ensuring a durable focus on engineering:**

- 50% ops cap means that extra ops work is redirected to product teams on overflow
- Provides feedback mechanism to product teams as well as keeps load down
- Target max 2 events per 8-12 hour on-call shift
- Postmortems for all serious incidents, even if they didn’t trigger a page
- Blameless postmortems

**Maximum change velocity without violating a service's SLO:**

- Error budget: 100% is the wrong reliability target for basically everything
- Going from 5 9s to 100% reliability isn’t noticeable to most users and requires tremendous effort
- Set a goal that acknowledges the trade-off and leaves an error budget
- Error budget can be spent on anything: launching features, etc.
- Goal of SRE team isn’t "zero outages", SRE and product devs are incentive aligned to spend the error budget to get maximum feature velocity

**Monitoring:**

- Monitoring should never require a human to interpret any part of the alerting domain
- Three valid kinds of monitoring output
  - **Alerts**: human needs to take action immediately
  - **Tickets**: human needs to take action eventually
  - **Logging**: no action needed \(Note that for example graphs are a type of log\)

**Emergency Response:**

- Reliability is a function of **MTTF** \(Mean Time To Failure\) and **MTTR** \(Mean Time To Recovery\)
- For evaluating responses, we care about MTTR
- Humans add latency, systems that don’t require humans to respond will have higher availability due to lower MTTR
- Having a "playbook" \(documentation of best practices\) produces 3x lower MTTR
- Having hero generalists who can respond to everything works, but having playbooks works better

**Change management:**

- 70% of outages are due to changes in a live system. Mitigation: implement progressive rollouts, monitoring and rollback
- Remove humans from the loop, avoid standard human problems on repetitive tasks

**Demand forecasting and capacity planning**

**Provisioning**

**Efficiency and performance**

## 2. The Production Environment at Google, from the Viewpoint of an SRE

### Hardware

Terminology:

- **Machine**: A piece of hardware (or perhaps a VM).
- **Server**: A piece of software that implements a service.

The topology of a Google datacenter:

- Tens of machine are placed in a **rack**.
- Racks stand in a **row**.
- One or more rows form a **cluster**.
- Usually a **datacenter** building house multiple clusters.
- Multiple datacenter buildings that are located close together form a **campus**.

### System Software That "Organizes" the Hardware

- **Managing Machines** with [Borg](https://research.google/pubs/pub43438/), a distributed cluster operating system.
- **Storage** with many layers: the lowest layer **D** is a fileserver running on all machines, a layer on top of D **Colossus** creates a cluster-wide fileystem and several databases like services built on top of Colossus: [Bigtable](https://research.google/pubs/pub27898/) (NoSQL), [Spanner](https://research.google/pubs/pub39966/) (SQL), **Blobstore**
- **Networking**: with [OpenFlow](https://en.wikipedia.org/wiki/OpenFlow), Bandwidth Enforcer (BwE) and Global Software Load Balancer (GSLB)

### Other System Software

- **Lock Service** with [Chubby](https://research.google/pubs/pub27897/)
- **Monitoring and Alerting** with Borgmon
- **Sotfware Infrastructure** with a http server on every servers for diagnostics and statistics, RPC calls with **protocol buffers** (Stubby or gRPC)

### Our Development Environment

Appart froma a few groups that have their own open source repositories (Android, Chrome), engineers work from a single shared repository (a [monorepo](https://research.google/pubs/pub45424/)).

## 3. Embracing risk

Extreme reliability (100%) comes at a cost: maximizing stability limits how fast new features can be developed and how quickly products can be delivered to users, and dramatically increases their costs.
Also, users typically don't notice the difference between high reliability vs extreme reliability: if a user is on a smartphone with 99% reliability, they can’t tell the difference between 99.99% and 99.999% reliability.

### Managing Risk

Reliability isn’t linear in cost. It can easily cost 100x more to get one additional increment of reliability. Goal: make systems reliable enough, but not too reliable!
The costliness has two dimensions:

- Cost associated with redundant machine/compute resources.
- Cost of building out features for reliability as opposed to "normal" features.

### Measuring Service Risk

Standard practice: identify metrics to represent the property of a system to optimize. For most services: **unplanned downtime** (the service availability, measured un number of "nines").

- **Time based availability = uptime / (uptime + downtime)** (problematic for a globally distributed service. What does uptime really mean?).
- **Aggregate availability = successful request / total requests** (not all requests are equal, but aggregate availability is an ok first order approximation).

### Risk Tolerance of Services

- Work with Product Owner to translate business objectives into explicit objectives.
- Identify risk tolerance of consumer and infrastructure services (target level of availability, types of failures, costs).
- Ex: consumer serving data from Bigtable need low latency and high reliability when teams using bigtable as a backing store for offline analysis need more throughput than reliability.

### Motivation for Error Budgets

An error budget provides a common incentive that allows both product development and SRE to focus on finding the right balance between innovation and reliability.

## 4. Service Level Objectives

### Service Level Terminology

- **Indicators**: (SLI) a carefully defined quantitative measure of some aspect of the level of service that is provided (request latency, error rate, system throughput, availability).
- **Objectives**: (SLO) a target value or range of values for a service level that is measured by an SLI (SLI <= SLO or lower SLO <= SLI <= upper SLO).
- **Agreements**: (SLA) an explicit or implicit contract with your users that includes consequences of meeting (or missing) the SLOs they contain.

### Indicators in Practice

What do you and your users care about?

- Too many indicators and its hard to pay attention / too few indicators and you might ignore important behavior.
- Different classes of services should have different indicators.
- User-facing: availability, latency, throughput.
- Storage: latency, availability, durability.
- Big data: throughput, end-to-end latency.
- All systems care about correctness.

Metric aggregation:

- Use distributions over averages in most cases (ex: to avoid hiding tail latencies).
- User studies show that people usually prefer slower average with better tail latency.
- Standardize on common definitions: aggregation intervals, regions, measurements frequency, how data is acquired etc.

### Objectives in Practice

Defining Objectives:

Choosing targets:

- Don’t pick target based on current performance (current performance may require heroic effort).
- Keep it simple
- Avoid absolutes (it's unreasonable to talk about "infinite" scale or "always" available)
- Have a few SLOs as possible (just enough to provide good coverage)
- Perfection can wait (can always redefine SLOs over time)
- SLOs set expectations (keep a safety margin and don't overachieve)

### Agreements in Practice

Crafting an SLA requires business and legal teams to pick appropriate consequences and penalties for a breach. The SRE role is to help them understand the likelihood and difficulty of meeting the SLOs containedd in the SLA. Be conservative in what your advertise to users.
