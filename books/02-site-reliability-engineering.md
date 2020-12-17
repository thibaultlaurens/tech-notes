---
description: How Google runs production systems.
---

# Site Reliability Engineering

* [Google SRE book review](https://danluu.com/google-sre-book/)

## 1. Introduction

### The Sysadmin Approach to Service Management

* Assemble existing components and deploy them to produce a service
* Respond to events and updates as they occur
* Pros:
  * Easy to implement because it’s standard
  * Large talent pool to hire from
  * Lots of available software
* Cons
  * Manual intervention for change management and event handling
  * Size of the team need to scale with the load on system / service
  * Conflict between OPS \(the service has to be stable\) vs DEV \(the service needs new features and updates\)

### Goole's Approach to Service Management: Site Reliability Engineering

* Operations is done the "software engineer" way, with automation instead of manual labor
* Candidates should be able to pass the dev recruitment test \(and may have some additional skills that are rare among devs like L1 - L3 networking or UNIX system internals\).
* Results: SREs will be bored to do tasks by hand and will have the skillset to automate them
* To avoid manual labor trap: **50% cap on the amount of "ops" work** for SREs \(upper bound, actual amount of ops work is expected to be much lower\)
* Pros
  * Cheaper to scale
  * Circumvents devs/ops split
* Cons
  * Hard to hire for
  * Require management support

### Tenets of SRE

An SRE team is responsible for the **availability, latency, performance, efficiency, change management, monitoring, emergency response, and capacity planning** of their services.

**Ensuring a durable focus on engineering:**

* 50% ops cap means that extra ops work is redirected to product teams on overflow
* Provides feedback mechanism to product teams as well as keeps load down
* Target max 2 events per 8-12 hour on-call shift
* Postmortems for all serious incidents, even if they didn’t trigger a page
* Blameless postmortems

**Maximum change velocity without violating a service's SLO:**

* Error budget: 100% is the wrong reliability target for basically everything
* Going from 5 9s to 100% reliability isn’t noticeable to most users and requires tremendous effort
* Set a goal that acknowledges the trade-off and leaves an error budget
* Error budget can be spent on anything: launching features, etc.
* Goal of SRE team isn’t "zero outages", SRE and product devs are incentive aligned to spend the error budget to get maximum feature velocity

**Monitoring:**

* Monitoring should never require a human to interpret any part of the alerting domain
* Three valid kinds of monitoring output
  * **Alerts**: human needs to take action immediately
  * **Tickets**: human needs to take action eventually
  * **Logging**: no action needed \(Note that for example graphs are a type of log\)

**Emergency Response:**

* Reliability is a function of **MTTF** \(Mean Time To Failure\) and **MTTR** \(Mean Time To Recovery\)
* For evaluating responses, we care about MTTR
* Humans add latency, systems that don’t require humans to respond will have higher availability due to lower MTTR
* Having a "playbook" \(documentation of best practices\) produces 3x lower MTTR
* Having hero generalists who can respond to everything works, but having playbooks works better

**Change management:**

* 70% of outages are due to changes in a live system. Mitigation: implement progressive rollouts, monitoring and rollback
* Remove humans from the loop, avoid standard human problems on repetitive tasks

**Demand forecasting and capacity planning**

**Provisioning**

**Efficiency and performance**

## 2. The Production Environment at Google, from the Viewpoint of an SRE

