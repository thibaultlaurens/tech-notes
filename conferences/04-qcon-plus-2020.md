# QCON PLUS 2020

## Languages of Infra

More than just Infrastructure as a Service, today we have libraries, languages, and platforms that help us define our infra. Languages of Infra explore languages and libraries being used today to build modern cloud native architectures.

### History of Infra as Code

By Andrew Clay Shafer - VP Transformation @RedHat - [Link](https://plus.qconferences.com/plus2020/presentation/history-infra-code)

A language is a structured system of communication. Both our human and computer languages enable, shape, and constrain the concepts we can effectively express. A whimsical look at the co-evolution of infrastructure and code starting from the beginning of time to the present with a look to the future. We'll walk through the progression of 'Infrastructure as Code' in theory and practice, some problems these developments solved and also some problems they revealed. What can we express today? What do we wish we could express? What will we express tomorrow?

Takeway:

- Infrastructure as Code:
  - Use all our software tricks: software development lifecycle, versionning, testing.
  - Be wary of the software pitfalls.
- Everything is a software built on top of silicon, so treat it as such.
- Timeline from 1990 to 2010: **CFEngine -&gt; bcfg2 -&gt; Puppet -&gt; Chef -&gt; SaltStack -&gt; Ansible**.
- Control Loops: from **Current State** to **Desired State**.
- Check [Pulumi](https://www.pulumi.com/) and [OpenShift](https://www.openshift.com/).

### Security and the Language of Intent

By Tracy Holmes - Developer Advocate @HashiCorp - [Link](https://plus.qconferences.com/plus2020/presentation/terraform-security)

Infrastructure as code empowers developers and operators to scale systems and maximize availability, but what about improving security? The language of security can be difficult to remember and implement under delivery pressure. In this talk, I’ll discuss why the language of security for infrastructure is often lost in translation and how policy as code can help. By using tools such as HashiCorp Sentinel, you can use policy as code to communicate and translate the security intentions you want and expect in your infrastructure.

Takeway:

- Exemple: making a database secure can mean a lot of things: secrets, lock subnets and ports, low priviledges, encryption, ACL..
- Benefits of **Policy as Code**: Sandboxing, Codification, Version control, Testing, Automation, Balance dev experience and security
- [**Hashicopr Sentinel**](https://www.hashicorp.com/sentinel): use policy as code to communicate and translate the security intentions you want and expect in your infrastructure.
- Sentinel policy enforcement is only available in TF Cloud or TF Enterprise.
- Open soutce alternative to Sentinal: OPA \([**Open Policy Agent**](https://www.openpolicyagent.org/)\)

## Architecting for Confidence: Building Resilient Systems

For any complex system, there is a wide array of activities that can increase system reliability and operator confidence. Each activity contributes in a different way.

If your system is safety-sensitive, you may invest heavily in pre-production testing strategies. If you want to holistically understand the effect of a change on individual users, you may use a sticky canary. If you don’t know your resource limits or bottlenecks, a load test could be useful. To validate design decisions around reliability mechanisms that don’t get exercised regularly, you may run chaos experiments. All these activities converge to build a stronger system that holds up to the pressures of production, but eventually your operators will have to engage to triage outages. When they do, it’s important they are comfortable doing so.

### A Sticky Situation: How Netflix Gains Confidence in Changes

By Haley Tucker - Senior Software Engineer, Resilience Team @Netflix

- How do you know whether a change will affect end users in a negative way?
- Canary deployments: Introduce a new service into the environment, users are randomly routed to that service, compare the performance of that service vs the current production build.
- Problem: this doesn’t really tell us anything about what the end users are experiencing, it focuses on service-level metrics.
- Netflix ChAP \(**Chaos Automation Platform**\) as a canary \(experiment\) platform.
- **Sticky Canaries**: Users are allocated for the duration of the experiment and can be filtered \(by location, devices etc.\).
- **Fault Injection**: Test how a new release behave under pressure.
- **Early Shutoff**: Automatically terminate experiment when customer impact is detected.
- **Canary Analysis**: Automatically generates reports and graphs at the end of the experiment.
- Benefits of Sticky Canaries: reduce experiment duration, reduce time to detect issues, deploy with confidence.
- Use cases: migrations, data changes, api changes.. \(backward compatibility are only assumptions in complex systems\)
- Can't be applied to: low volume services, no production traffic, services not directly related to KPIs

Takeway:

- Build hooks into your platform to enable the types of experiments you need.
- Provide guard rails for testing in production.
- Monitor customer KPIs - not proxy metrics.

Links:

- [Principles of chaos engineering](https://principlesofchaos.org/)
- [ChAP: Chaos Automation Platform](https://netflixtechblog.com/chap-chaos-automation-platform-53e6d528371f)

### User Simulation for Rapid Outage Mitigation

### Architecting Resilient Data

By Jim Walker - VP Product Marketing @CockroachDB

- Our applications all fail at some point in time. It is unavoidable. What if it is the database ?
- The costly impacts of database downtime: customer loss, reputation impact, team stress, lost revenue potential..
- RTO \(**Recovery Time Objective**\): The amount of time an application can be down without causing significant damage ?
- RPO \(**Recovey Point Objective**\): The amount of data that can be lost before significant damage occurs.
- Limitations of active/passive \(primary/secondary\) strategies: costs, complexity \(especially true with sharding\), backups, synchronization/conflict issues..
- Distributed SQL and active-active data try to bring the best of both SQL \(transactions\) and NoSQL \(resilience\) world.

## Resurgence of Functional Programming

What was once a paradigm shift in how we thought of programming languages is now main stream in nearly all modern languages. Hear how software shops are infusing concepts like pure functions and immutablity into their architectures and design choices.

### The Functional Evolution of Object-Oriented Programming

## Paths to Production: Deployment Pipelines as a Competitive Advantage

Enabling developers to push to production at ever increasing velocity has become a competitive advantage. Paths to production examines how some of software’s most well known shops supercharge developers and keep their companies competitive by balancing speed and safety.

### Safe and Fast Deploys at Planet Scale

### Paving the Road to Production

By Graham Jenson Infrastructure Tech Lead @Coinbase

- The journey of Ops at Coinbase, from day one to now with exponential growth.
- 1st stage: startup - YOLO deploy in Heroku and Bob the admin, but Bob is a blocker.
- 2nd stage: AWS, docker, open culture, deploy first day, move fast and break things.
- 3rd stage: Use proper automation and deployment tools. Had to build it \(CodeFlow\) to fit the special company need but also because such tools did not exist yet.
- 4th stage: The only way to scale is to document everything \(think 100+ projects\), build more custom tool for specific developments/deployments, finally build a framework to keep it all consistent.
- 5th stage: 4th stage was not enough so Monorepo + Bazel + custom CLI \(500+ projects to maintains\)
- Tomorrow: Time to split the organization.
- Conclusion: Iterate and improve ops/deployments continuously, try to keep it consistent, don't build one road \(to production\) per car \(projects\). Instead, try to build a highway where everyone can drive \(be consistent or you won't scale\).

Links:

- [Bazel](https://bazel.build/)
