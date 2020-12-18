# QCON PLUS 2020

## Keynote: The SRE as a Diplomat

_Johnny Boursiquot - SRE @Salesforce/Heroku_

No two organizations implement the practices of Site Reliability Engineering in the same manner and that fact is seldom recognized when rolling out an SRE function for the first time. While there exists a through-line of best practices, those that take on the task of championing SRE within their organization know that, even as a mandate, the implementation is one that requires close collaboration between engineers, operators, and leadership. As Site Reliability Engineering finds itself at the cross-roads of the needs of these stakeholders, the job becomes akin to that of the diplomat who must carefully initiate and facilitate strategic agreements that drive all parties towards the safe creation and maintenance of scalable and reliable software systems.

This talk explores the following ideas:

- The unintended consequences of certain service ownership and operational models.
- When SRE is seen as an "outside", unwanted influence, and how to build trust with those teams.
- The "Forward Deployed SRE" model as a bridge between individual teams and the operational excellence engineering leaders seek when adopting (and sometimes, mandating) SRE practices.
- What then, makes a great Site Reliability Engineer? We explore the technical but more importantly, the non-technical attributes that someone should have when taking on this critical role.

Takeaway:

- Total ownership model: build **self sufficient team**, they build it, they deploy it, they are responsible for it
- **Forward deployed SREs** balance immediate operationnal needs and long term operational excellence of the entire org
- SRE qualities: **operationally-minded, takes on more ownership, empathetic, catalyst for change, teacher and mentor, diplomat**
- Advices: Figure out asap where the organization is on its **journey to ops excellence** (SLO? Observability? Error budget? Release cadence under control?)

## Languages of Infra

More than just Infrastructure as a Service, today we have libraries, languages, and platforms that help us define our infra. Languages of Infra explore languages and libraries being used today to build modern cloud native architectures.

### History of Infra as Code

_Andrew Clay Shafer - VP Transformation @RedHat_

A language is a structured system of communication. Both our human and computer languages enable, shape, and constrain the concepts we can effectively express. A whimsical look at the co-evolution of infrastructure and code starting from the beginning of time to the present with a look to the future. We'll walk through the progression of 'Infrastructure as Code' in theory and practice, some problems these developments solved and also some problems they revealed. What can we express today? What do we wish we could express? What will we express tomorrow?

Takeaway:

- Infrastructure as Code: use all our software tricks (software development lifecycle, versionning, testing) but be wary of the software pitfalls.
- **Everything is a software built on top of silicon**, so treat your infrastructure as such.
- Timeline from 1990 to 2010: **CFEngine -&gt; bcfg2 -&gt; Puppet -&gt; Chef -&gt; SaltStack -&gt; Ansible**.
- Control Loops: from **Current State** to **Desired State**.

### Security and the Language of Intent

_Tracy Holmes - Developer Advocate @HashiCorp_

Infrastructure as code empowers developers and operators to scale systems and maximize availability, but what about improving security? The language of security can be difficult to remember and implement under delivery pressure. In this talk, I’ll discuss why the language of security for infrastructure is often lost in translation and how policy as code can help. By using tools such as HashiCorp Sentinel, you can use policy as code to communicate and translate the security intentions you want and expect in your infrastructure.

Takeaway:

- Exemple: making a database secure can mean a lot of things: secrets, lock subnets and ports, low priviledges, encryption, ACL..
- Benefits of **Policy as Code**: Sandboxing, Codification, Version control, Testing, Automation, Balance dev experience and security.
- [**Hashicopr Sentinel**](https://www.hashicorp.com/sentinel): use policy as code to communicate and translate the security intentions you want and expect in your infrastructure.
- Sentinel policy enforcement is only available in TF Cloud or TF Enterprise.
- Open soutce alternative to Sentinal: **OPA** ([**Open Policy Agent**](https://www.openpolicyagent.org/))

## Architecting for Confidence: Building Resilient Systems

For any complex system, there is a wide array of activities that can increase system reliability and operator confidence. Each activity contributes in a different way.

If your system is safety-sensitive, you may invest heavily in pre-production testing strategies. If you want to holistically understand the effect of a change on individual users, you may use a sticky canary. If you don’t know your resource limits or bottlenecks, a load test could be useful. To validate design decisions around reliability mechanisms that don’t get exercised regularly, you may run chaos experiments. All these activities converge to build a stronger system that holds up to the pressures of production, but eventually your operators will have to engage to triage outages. When they do, it’s important they are comfortable doing so.

### A Sticky Situation: How Netflix Gains Confidence in Changes

_Haley Tucker - Senior Software Engineer, Resilience Team @Netflix_

How do you know whether a change will affect end users in a negative way? As interactions in distributed systems grow increasingly complex, it can be challenging to get an answer to this question.
One approach is to use a canary in which we introduce a new service into the environment, users are randomly routed to that service, and we compare the performance of that service to the current production build. However, this doesn’t really tell us anything about what the end users are experiencing -- it focuses on service-level metrics. In reality, a service may be happily serving successful requests, yet the end user is not able to use your product.
As a result, it can be useful to have a methodology which enables teams to observe the full impact of a change on end users. In this talk, I will demonstrate how Netflix uses sticky canaries to fulfill this need and I will highlight use cases where we have employed this methodology successfully. I will also cover the key platform features and tools to include when implementing sticky canaries.

Takeaway:

- [Principles of chaos engineering](https://principlesofchaos.org/)
- **Netflix ChAP** ([Chaos Automation Platform](https://netflixtechblog.com/chap-chaos-automation-platform-53e6d528371f)) as a canary \(experiment\) platform.
- **Sticky Canaries**: Users are allocated for the duration of the experiment and can be filtered \(by location, devices etc.\).
- **Fault Injection**: Test how a new release behaves under pressure.
- **Early Shutoff**: Automatically terminate experiment when customer impact is detected.
- **Canary Analysis**: Automatically generates reports and graphs at the end of the experiment.
- Benefits of Sticky Canaries: **reduce experiment duration, reduce time to detect issues, deploy with confidence**.
- Use cases: migrations, data changes, api changes.. (**backward compatibility are only assumptions in complex systems**)
- Can't be applied to: low volume services, no production traffic, services not directly related to KPIs

Conclusion:

- Build hooks into your platform to enable the types of experiments you need.
- Provide guard rails for testing in production.
- **Monitor customer KPIs - not proxy metrics.**

### Architecting Resilient Data

_Jim Walker - VP Product Marketing @CockroachDB_

Our applications all fail at some point in time. It is unavoidable. Over the past few decades we’ve employed techniques to limit the impact of these moments through often complex and costly active/passive backup strategies. There has to be a better way. In this talk, Jim Walker from Cockroach Labs will walk through the concept of an active-active, always-on database that is rooted in the fundamental principles of distributed systems.

Takeaway:

- The costly impacts of database downtime: **customer loss, reputation impact, team stress, lost revenue potential..**
- RTO \(**Recovery Time Objective**\): The amount of time an application can be down without causing significant damage ?
- RPO \(**Recovey Point Objective**\): The amount of data that can be lost before significant damage occurs.
- Limitations of active/passive \(primary/secondary\) strategies: costs, complexity \(especially true with sharding\), backups, synchronization/conflict issues..
- **Distributed SQL and active-active data** try to bring the best of both SQL \(transactions\) and NoSQL \(resilience\) world.

## Paths to Production: Deployment Pipelines as a Competitive Advantage

Enabling developers to push to production at ever increasing velocity has become a competitive advantage. Paths to production examines how some of software’s most well known shops supercharge developers and keep their companies competitive by balancing speed and safety.

### Safe and Fast Deploys at Planet Scale

_Mathias Schwarz Software Engineer @Uber_

Can you write code, review, test, verify, and ship it safely to millions of users, all in the same day? Absolutely!
Every week thousands of Uber engineers push out several thousand changes to millions of users. This means that during working hours, some part of the Uber system starts upgrading every single minute and that the system never runs one single version across the host fleet.
In this talk, we will explore the lessons we learned as we scaled from a small engineering team using a single datacenter to thousands of engineers that continuously deploy changes across multiple cloud platforms, with a focus on maintaining fast and reliable delivery of software changes.

Takeaway:

- Uber: **4000 microservices in production** deployed in private DCs and public cloud (Google and Amazon)
- **58k builds / week** and **5k deploys / week**
- Infra abstractions for deployments: **DCs -> Regions -> Zones -> Servers**
- Importent deploy system features: **consistent builds, zero downtime, outage prevention**
- 2016: [μDeploy](https://eng.uber.com/micro-deploy-code/) + [uMonitor](https://eng.uber.com/observability-at-scale/) + white and black box custom testing tools
- Today: "Up": **declarative deployments** (region placement, capacity, canaries, auto-scalling, dependencies) by developers built with a **continuous evaluation loop** to dynamically balance microservices accross zones

### Paving the Road to Production

_Graham Jenson Infrastructure Tech Lead @Coinbase_

"Paved roads" are the paths walked by developers to get their code into production. They are a contract that core teams (like infrastructure and security) have with developers about features and support they will receive if they tread a common path. The benefits of staying on a paved road for a developer is that they get a lot of functionality (like security, logging, metrics) out-of-the-box. For core teams, paved roads are a point of focus where even small improvements can have a big effect.
In this talk, I will share my experience of creating "paved roads" and deploy pipelines at Coinbase for the past 5 years. Describing how these roads look and have scaled as the company grew from 10 to 500 engineers. I will also talk about the advantages of having a paved road, how to build new paved roads, and how applications might be moved onto one. I am hoping that this talk will convince you to pave your own roads to production.

Takeaway:

- The journey of Ops at Coinbase, from day one to now with exponential growth.
- 1st stage: startup - **YOLO deploy** with Heroku and Bob the admin, but Bob is a blocker.
- 2nd stage: AWS, docker, open culture, deploy first day, **move fast and break things**.
- 3rd stage: **Use proper automation and deployment tools**. Had to build it \(CodeFlow\) to fit the special company need but also because such tools did not exist yet.
- 4th stage: **The only way to scale is to document everything** \(think 100+ projects\), build more custom tool for specific developments/deployments, finally **build a framework** to keep it all consistent.
- 5th stage: 4th stage was not enough so **Monorepo + [Bazel](https://bazel.build/)** + custom CLI \(500+ projects to maintains\)
- Tomorrow: Time to **split the organization**.
- Conclusion: Iterate and **improve ops/deployments continuously**, try to keep it consistent, don't build one road \(to production\) per car \(projects\). Instead, try to **build a highway** where everyone can drive \(be consistent, or you won't scale\).

## Operating Microservices

Building and operating distributed systems is hard, and microservices are no different. Learn strategies for not just building a service but operating them at scale.

### From Monolith to Microservices

_Sha Ma - VP of Software Engineering @GitHub_

Due to its low overhead and centralized management, companies often start building products under a monolithic architecture. But as team sizes grow and product use cases become more complicated, this often slows down software development and adds unnecessary friction in the deployment and troubleshooting processes.  
In this talk, we aim to take a practical approach to software architecture decisions. We will be taking a deeper look at GitHub’s historical and current state, go over some internal and external factors, and discuss practical consideration points in how we started to tackle this migration. Then we will walk through some key concepts and best practices of implementing a microservices architecture that you can apply as you think about this transformation for your organization.

Takeaway:

- Github: Ruby everywhere, 12+ years old monolithic codebase, highly scaled, performant (1 billion API calls everyday), get the job done.
- From 1k to 2k developers in 18 months (70% full remote accross the world) -> time to split the monolith.
- monolith pros: **infra, code, architecture and org is simpler**.
- microservices pros: **system ownership, smaller components, separation of concerns, separate scalling**.
- Hybrid state for a loooooong time to do it proprely (trying to avoid the **distributed monolith**).
- **Separation of data** is key: functional groups (schema domains), partition keys, query rewrite.
- Start by **extracting the core services**, then authentication and authorization componants.
- Adjust and adapt monitoring, CI/CD tools and practices, everything.. along the way.
- Sizing correctly a microservice is key.
- New problem: **async service to service communication**.

### Solving Mysteries Faster with Observability

_Elizabeth Carretto - Senior Software Engineer @Netflix_

Investigating production issues in a microservice architecture can make you feel like a detective, combing through evidence and gathering clues to reconstruct the scene of a crime, all while the clock is ticking. You hop from log store to dashboard, digging for details as you strive to unravel what really happened. All this time spent investigating is expensive, for engineers as well as customers -- and even then, finding an issue is not the same as resolving it!
Edgar is a tool used and built by Netflix engineers to quickly investigate and solve production issues. Edgar starts with distributed tracing, which shows a request’s path through a complex system. But the request’s path is only a small part of the data available about a request. Dozens of dashboards hold their own insights on what happened, and it takes time for engineers to jump between individual dashboards. Edgar strives to get all this data in one place, supplementing traces with additional context like log correlation, metadata about services, and intelligent analysis.

Takeaway:

- Observability alone (logs, metrics and traces) is not enough: we need **metadata** to help understand the context of the incident.
- [Edgar](https://netflixtechblog.com/edgar-solving-mysteries-faster-with-observability-e1a76302c71f) Killer features: **correlation**, **playback**, **integration with dev tools**

## Security in a State of Insecurity

The pandemic has forced society and the infosec industry to adapt to challenging and sudden behavioral, situational, and technological changes. In the Security in a State of Insecurity track, we’ll explore how attackers have taken advantage of this unplanned situation, the unique ways companies have shifted and adapted to these changes, and the lessons learned therein.

### Failing Fast: The Impact of Bias When Speeding Up Application Security

_Laura Bell - Founder and CEO of @Safestack_

There is a lot of talk these days about going faster with security, DevSecOps and making security part of your lifecycle. What if _you_ are the reason this might be a pathway to failing fast at security? In this talk, we will explore how bias impacts how we secure our development lifecycles and examine 3 common biases that lead to big issues in this space. By looking at mistakes teams make when embracing application security and how bias plays into them, we can learn to avoid them and make security a key part of moving faster.

Takeaway:

- **Seniority Bias**: "We can only go faster if we only use experienced engineers"
- **Tool Bias**: "We can only go faster if we buy this tool"
- **Recency Bias**: "We can only go faster if we do this thing I read about last week"
